# Code snippets for setting up JWT security
- [video help for below code examples](https://cphbusiness.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=d329a3f7-1a16-41d9-9e92-b13200c2a4b0)
- [hashing passwords video](https://cphbusiness.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=9d3b7d78-48cc-4286-8ebb-b13200acb994)

## POM.xml dependencies for security code below
```xml
<dependency>
    <groupId>com.nimbusds</groupId>
    <artifactId>nimbus-jose-jwt</artifactId>
    <version>9.10</version>
</dependency>
<dependency>
    <groupId>org.mindrot</groupId>
    <artifactId>jbcrypt</artifactId>
    <version>0.4</version>
</dependency>
```
- The `nimbuds-jose-jwt` dependency is used for creating and verifying JWT tokens and the `jbcrypt` dependency is used for hashing passwords.

## Security Routes
```java
public static EndpointGroup getSecurityRoutes() {
    return ()->{
        path("/auth", ()->{
            post("/login", securityController.login(),Role.ANYONE);
            post("/register", securityController.register(),Role.ANYONE);
        });
    };
}
```
## Register
- Register a new user with username and password
```java
 @Override
public Handler register() {
    return (ctx) -> {
        ObjectNode returnObject = objectMapper.createObjectNode();
        try {
            UserDTO userInput = ctx.bodyAsClass(UserDTO.class);
            User created = securityDAO.createUser(userInput.getUsername(), userInput.getPassword());

            String token = createToken(new UserDTO(created));
            ctx.status(HttpStatus.CREATED).json(new TokenDTO(token, userInput.getUsername()));
        } catch (EntityExistsException e) {
            ctx.status(HttpStatus.UNPROCESSABLE_CONTENT);
            ctx.json(returnObject.put("msg", "User already exists"));
        }
    };
}
```
## Login
- Logging is an handler that takes a username and password and returns a JWT token
```java
@Override
public Handler login() {
    return (ctx) -> {
        ObjectNode returnObject = objectMapper.createObjectNode(); // for sending json messages back to the client
        try {
            UserDTO user = ctx.bodyAsClass(UserDTO.class);
            System.out.println("USER IN LOGIN: " + user);

            User verifiedUserEntity = securityDAO.getVerifiedUser(user.getUsername(), user.getPassword());
            String token = createToken(new UserDTO(verifiedUserEntity));
            ctx.status(200).json(new TokenDTO(token, user.getUsername()));

        } catch (EntityNotFoundException | ValidationException e) {
            ctx.status(401);
            System.out.println(e.getMessage());
            ctx.json(returnObject.put("msg", e.getMessage()));
        }
    };
}
```
- `getVerifiedUser` returns the validated user from the database (including roles)
```java
@Override
public User getVerifiedUser(String username, String password) throws ValidationException {
    try (EntityManager em = getEntityManager()) {
        List<User> users = em.createQuery("SELECT u FROM User u").getResultList();
        users.stream().forEach(user -> System.out.println(user.getUsername() + " " + user.getPassword()));
        User user = em.find(User.class, username);
        if (user == null)
            throw new EntityNotFoundException("No user found with username: " + username); //RuntimeException
        user.getRoles().size(); // force roles to be fetched from db
        if (!user.verifyPassword(password))
            throw new ValidationException("Wrong password");
        return user;
    }
}
```
- `SecurityController -> createToken` is a method that setup data for the token
```java
@Override
public String createToken(UserDTO user) {
    String ISSUER;
    String TOKEN_EXPIRE_TIME;
    String SECRET_KEY;

    if (System.getenv("DEPLOYED") != null) {
        ISSUER = System.getenv("ISSUER");
        TOKEN_EXPIRE_TIME = System.getenv("TOKEN_EXPIRE_TIME");
        SECRET_KEY = System.getenv("SECRET_KEY");
    } else {
        ISSUER = "Thomas Hartmann";
        TOKEN_EXPIRE_TIME = "1800000"; // 30 minutes in milliseconds
        SECRET_KEY = Utils.getPropertyValue("SECRET_KEY","config.properties");
    }
    return tokenUtils.createToken(user, ISSUER, TOKEN_EXPIRE_TIME, SECRET_KEY);
}
- and `Utils.createToken` is a method that creates a JWT token from a user
```java
 public String createToken(UserDTO user, String ISSUER, String TOKEN_EXPIRE_TIME, String SECRET_KEY){
        // https://codecurated.com/blog/introduction-to-jwt-jws-jwe-jwa-jwk/
    try {
        JWTClaimsSet claimsSet = new JWTClaimsSet.Builder()
                .subject(user.getUsername())
                .issuer(ISSUER)
                .claim("username", user.getUsername())
                .claim("roles", user.getRoles().stream().reduce((s1, s2) -> s1 + "," + s2).get())
                .expirationTime(new Date(new Date().getTime() + Integer.parseInt(TOKEN_EXPIRE_TIME)))
                .build();
        Payload payload = new Payload(claimsSet.toJSONObject());

        JWSSigner signer = new MACSigner(SECRET_KEY);
        JWSHeader jwsHeader = new JWSHeader(JWSAlgorithm.HS256);
        JWSObject jwsObject = new JWSObject(jwsHeader, payload);
        jwsObject.sign(signer);
        return jwsObject.serialize();

    } catch (JOSEException e) {
        e.printStackTrace();
        throw new ApiException(500, "Could not create token");
    }
}
```
## Create Token
- The 




## Making requests with JWT
- Now that we can register a new user, login a user with username and password and get a token, we can access a protected endpoint with the token:
```java
public static EndpointGroup getSecuredRoutes(){
    return ()->{
        path("/protected", ()->{
            before(securityController.authenticate());
            get("/user_demo",(ctx)->ctx.json(jsonMapper.createObjectNode().put("msg",  "Hello from USER Protected")),Role.USER);
            get("/admin_demo",(ctx)->ctx.json(jsonMapper.createObjectNode().put("msg",  "Hello from ADMIN Protected")),Role.ADMIN);
        });
    };
}
public enum Role implements RouteRole { ANYONE, USER, ADMIN }
```
- If the token is valid and the user has the correct role, the user will be able to access the protected endpoint. If not, the user will get a 403 Forbidden response.
- The fourth line in the above code snippet is a `before` filter that checks if the user is authenticated and has the correct role. If not, the user will get a 403 Forbidden response.
- The `securityController.authenticate` method: 
```java
@Override
public Handler authenticate() {
    // To check the users roles against the allowed roles for the endpoint (managed by javalins accessManager)
    // Checked in 'before filter' -> Check for Authorization header to find token.
    // Find user inside the token, forward the ctx object with userDTO on attribute
    // When ctx hits the endpoint it will have the user on the attribute to check for roles (ApplicationConfig -> accessManager)
    ObjectNode returnObject = objectMapper.createObjectNode();
    return (ctx) -> {
        if(ctx.method().toString().equals("OPTIONS")) {
            ctx.status(200);
            return;
        }
        String header = ctx.header("Authorization");
        if (header == null) {
            ctx.status(HttpStatus.FORBIDDEN).json(returnObject.put("msg", "Authorization header missing"));
            return;
        }
        String token = header.split(" ")[1];
        if (token == null) {
            ctx.status(HttpStatus.FORBIDDEN).json(returnObject.put("msg", "Authorization header malformed"));
            return;
        }
        UserDTO verifiedTokenUser = verifyToken(token);
        if (verifiedTokenUser == null) {
            ctx.status(HttpStatus.FORBIDDEN).json(returnObject.put("msg", "Invalid User or Token"));
        }
        System.out.println("USER IN AUTHENTICATE: " + verifiedTokenUser);
        ctx.attribute("user", verifiedTokenUser);
    };
}
```
- The above code checks for the `Authorization` header and verifies the token. If the token is valid, the user will be added to the context as an attribute and the request will be passed on to the endpoint. If the token is invalid or missing, the user will get a 403 Forbidden response.
- Finally the roles are checked in the `ApplicationConfig`:
```java
public ApplicationConfig checkSecurityRoles() {
    // Check roles on the user (ctx.attribute("username") and compare with permittedRoles using securityController.authorize()
    app.updateConfig(config -> {

        config.accessManager((handler, ctx, permittedRoles) -> {
            // permitted roles are defined in the last arg to routes: get("/", ctx -> ctx.result("Hello World"), Role.ANYONE);

            Set<String> allowedRoles = permittedRoles.stream().map(role -> role.toString().toUpperCase()).collect(Collectors.toSet());
            if(allowedRoles.contains("ANYONE") || ctx.method().toString().equals("OPTIONS")) {
                // Allow requests from anyone and OPTIONS requests (preflight in CORS)
                handler.handle(ctx);
                return;
            }

            UserDTO user = ctx.attribute("user");
            System.out.println("USER IN CHECK_SEC_ROLES: "+user);
            if(user == null)
                ctx.status(HttpStatus.FORBIDDEN)
                        .json(jsonMapper.createObjectNode()
                                .put("msg","Not authorized. No username were added from the token"));

            if (SecurityController.getInstance().authorize(user, allowedRoles))
                handler.handle(ctx);
            else
                throw new ApiException(HttpStatus.FORBIDDEN.getCode(), "Unauthorized with roles: "+allowedRoles);
        });
    });
    return appConfig;
}
```
- In the above method the roles are checked against the user and the allowed roles for the endpoint. If the user has the correct role, the request will be passed on to the endpoint. If not, the user will get a 403 Forbidden response.
- The list of permitted roles comes from the last argument to the `get` method in the `getSecuredRoutes` method above.
