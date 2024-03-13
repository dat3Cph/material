# Security Exercise
## Assistance
- [video help for below code examples](https://cphbusiness.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=d329a3f7-1a16-41d9-9e92-b13200c2a4b0)
- [hashing passwords video](https://cphbusiness.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=9d3b7d78-48cc-4286-8ebb-b13200acb994)
- [Code](../../setup/securityCode.md)
Use an existing Rest project from last week or create a new one. Now add security and Rest Assured tests to the project.

## Part 1 Hashing Passwords
- Create a User Entity and a Role Entity with ManyToMany relationship between them
- Let the User interface implement the following interface: 
```java
public interface ISecurityUser {
    Set<String>  getRolesAsStrings();
    boolean verifyPassword(String pw);
    void addRole(Role role);
    void removeRole(String role);
}
```
- Create a UserDAO that implements the following interface: 
```java
public interface ISecurityDAO {
    User getVerifiedUser(String username, String password) throws ValidationException;
    User createUser(String username, String password);
    Role createRole(String role);
    User addUserRole(String username, String role);
}
```
- Use bcrypt to hash the password before storing it in the database.
  - bcrypt link: https://www.mindrot.org/projects/jBCrypt/
  - `<dependency><groupId>org.mindrot</groupId><artifactId>jbcrypt</artifactId><version>${jbcrypt.version}</version></dependency>`
- Hint: Hash the password in the User constructor: ` BCrypt.hashpw(userPass, BCrypt.gensalt());`
- Hint: Verify the password in the verifyPassword method: `BCrypt.checkpw(password, this.password);`

## Part 2 Login and Register Endpoints
### The Process
#### Register
1. The user sends a register (POST) request to the server with a username and password.
2. The server checks if the username is taken.
3. If the username is taken, the server returns an error.
4. If the username is not taken, the server creates a user and returns a JWT token.
#### Login
5. The user sends a login (POST) request to the server with a username and password.
6. The server checks if the username and password are valid.
7. If the username and password are valid, the server returns a JWT token.
8. If the username and password are invalid, the server returns an error.
#### Authenticate
9. The user sends a request to a protected endpoint with the JWT token in the header ('Authorization': 'Bearer ' + token).
10. A `before` filter calls the `authenticate` method in the SecurityController and check if the token is valid
11. If it is valid the user is added to the context as an attribute and the request is passed on to the endpoint.
11. If the JWT token is valid, the server checks if the user has the required roles to access the endpoint.
12. If the JWT token is invalid or missing, the server returns an error.
13. If the user doesn't have the required roles, the server returns an error.

### Code snippets:
- ApplicationConfig -> checkSecurityRoles
```java
    // Adding below methods to ApplicationConfig, means that EVERY ROUTE will be checked for security roles. So open routes must have a role of ANYONE
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
- SecurityController -> authorize
```java
    public boolean authorize(UserDTO userDTO, Set<String> allowedRoles) {
        Set<String> userRoles = userDTO.getRoles();
        for (String role : allowedRoles) {
            if (userRoles.contains(role)) {
                return true;
            }
        }
        return false;
    }
```
- hint: allowedRoles are defined in the last arg to routes: get("/", ctx -> ctx.result("Hello World"), Role.ANYONE);
- verifyToken
```java
@Override
    public UserDTO verifyToken(String token) {
        boolean IS_DEPLOYED = (System.getenv("DEPLOYED") != null);
        String SECRET = IS_DEPLOYED ? System.getenv("SECRET_KEY") : Utils.getPropertyValue("SECRET_KEY","config.properties");

        try {
            if (tokenUtils.tokenIsValid(token, SECRET) && tokenUtils.tokenNotExpired(token)) {
                return tokenUtils.getUserWithRolesFromToken(token);
            } else {
                throw new NotAuthorizedException(403, "Token is not valid");
            }
        } catch (ParseException | JOSEException | NotAuthorizedException e) {
            e.printStackTrace();
            throw new ApiException(HttpStatus.UNAUTHORIZED.getCode(), "Unauthorized. Could not verify token");
        }
    }
```
- createToken
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
            TOKEN_EXPIRE_TIME = "1800000";
            SECRET_KEY = Utils.getPropertyValue("SECRET_KEY","config.properties");
        }
        return tokenUtils.createToken(user, ISSUER, TOKEN_EXPIRE_TIME, SECRET_KEY);
    }
```
- Utils.getPropertyValue
```java
public static String getPropertyValue(String propName, String ressourceName)  {
    // REMEMBER TO BUILD WITH MAVEN FIRST. Read the property file if not deployed (else read system vars instead)
    try (InputStream is = Utils.class.getClassLoader().getResourceAsStream(ressourceName)) { //"config.properties" or "properties-from-pom.properties"
        Properties prop = new Properties();
        prop.load(is);
        return prop.getProperty(propName);
    } catch (IOException ex) {
        ex.printStackTrace();
        throw new ApiException(500, String.format("Could not read property %s. Did you remember to build the project with MAVEN?", propName));
    }
}
```
- Pom.xml (In order for java to read the properties from the property file, we need to add the following plugin to the pom.xml). This will create a properties-from-pom.properties file in the target/classes folder.
```xml
<plugin>
    <!--  https://www.baeldung.com/java-accessing-maven-properties  -->
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>properties-maven-plugin</artifactId>
    <version>1.0.0</version>
    <executions>
        <execution>
            <phase>generate-resources</phase>
            <goals>
                <goal>write-project-properties</goal>
            </goals>
            <configuration>
                <outputFile>${project.build.outputDirectory}/properties-from-pom.properties</outputFile>
            </configuration>
        </execution>
    </executions>
</plugin>
```



- Create an endpoint that can handle a login request containing a username and password.
  - The endpoint should return a JWT token if the username and password are valid.
  - The endpoint should return an error if the username and password are invalid.
  - Create a UserController that implements the following interface:
```java
public interface ISecurityController {
    Handler login(); // to send username and password (use a UserDTO) and to get a token
    Handler register(); // to send username and password, create a user and return a JWT token or throw exception if username is taken
    Handler authenticate(); //  To check the users roles against the allowed roles for the endpoint (managed by javalins accessManager);
    boolean authorize(UserDTO userDTO, Set<String> allowedRoles); // to verify user roles used by the accessManager
    String createToken(UserDTO user) throws Exception; // used in login and register
    UserDTO verifyToken(String token) throws Exception; // used in authenticate
}
```

## Part 3 Protect Endpoints
- Create an endpoint that can only be accessed by authenticated users with a role of ADMIN.
  - The endpoint should return an error if the JWT token is invalid.
  - The endpoint should return an error if the JWT token is valid but the user doesn't have the ADMIN role.
  - The endpoint should return the protected resource if the JWT token is valid.
- Add more endpoints so that there are endpoints for only USER and only ADMIN roles and endpoints that are open to all users.

## Part 4 Testing
- Use Rest Assured, JUnit 5, and Hamcrest matchers to test all the finished endpoints.
  - Test protected Endpoints by storing a valid JWT token in a variable and use it in the test.
- 