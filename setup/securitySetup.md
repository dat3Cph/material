# Security setup for 3rd semester backend

This page describes how to add a security layer for the Rest APIs. The security consists of these aspects:

1. Login authentication through the api
2. Hashing user passwords with jBCrypt, so all passwords stored in entities and in the database are no longer clear text.
3. Implementation of JWT (Json Web Tokens) in the backend
4. Implemention of user roles, so each endpoint can be protected and made accessable only for users with a particular role.

## How to add security to an existing API built in Javalin

We will use this repo as an example to begin with, and add the necessary dependencies, classes and methods to provide a decent level of security:

- [https://github.com/dat3Cph/3sem-javalin-rest-api](https://github.com/dat3Cph/3sem-javalin-rest-api) (take the restassured branch to start with - or use your own version with Rest Assured and test containers implemented).

## 1. Checking the pom.xml file

These dependencies are probably already present. But check anyway. 

```xml
<!--   Security     -->
<dependency>
    <!--  https://nimbusds.com/products/nimbus-jose-jwt   -->
    <groupId>com.nimbusds</groupId>
    <artifactId>nimbus-jose-jwt</artifactId>
    <version>9.0.1</version>
</dependency>
<dependency>
    <groupId>org.mindrot</groupId>
    <artifactId>jbcrypt</artifactId>
    <version>0.4</version>
</dependency>
```

In the properties section, these should also be there:

```xml
<!--  token    -->
<secret.key>841D8A6C80CBA4FCAD32D5367C18C53B</secret.key>
<issuer>cphbusiness.dk</issuer>
<token.expiration.time>3600000</token.expiration.time>
```

## 2. Add needed security classes

Create a package called `security` and add these three classes:

RouteRoles, an enum with user roles:

```Java
package dk.lyngby.security;

public enum RouteRoles implements io.javalin.security.RouteRole {
    ANYONE("anyone"), USER("user"), ADMIN("admin"), MANAGER("manager");

    private final String role;

    RouteRoles(String role) {
        this.role = role;
    }

    @Override
    public String toString() {
        return role;
    }
}
```

SignVerifyToken, helper methods for handling JWT:

```Java
package dk.lyngby.security;

import com.nimbusds.jose.*;
import com.nimbusds.jose.crypto.MACSigner;
import com.nimbusds.jose.crypto.MACVerifier;
import com.nimbusds.jwt.JWTClaimsSet;
import com.nimbusds.jwt.SignedJWT;
import dk.lyngby.dto.UserDTO;
import dk.lyngby.exception.AuthorizationException;

import java.text.ParseException;
import java.util.Date;


public class SignVerifyToken {

    private final String ISSUER, TOKEN_EXPIRE_TIME, SECRET_KEY;

    public SignVerifyToken(String ISSUER, String TOKEN_EXPIRE_TIME, String SECRET_KEY) {
        this.ISSUER = ISSUER;
        this.TOKEN_EXPIRE_TIME = TOKEN_EXPIRE_TIME;
        this.SECRET_KEY = SECRET_KEY;
    }

    public String signToken(String userName, String rolesAsString, Date date) throws JOSEException {
        JWTClaimsSet claims = createClaims(userName, rolesAsString, date);
        JWSObject jwsObject = createHeaderAndPayload(claims);
        return signTokenWithSecretKey(jwsObject);
    }

    private JWTClaimsSet createClaims(String username, String rolesAsString, Date date) {
        return new JWTClaimsSet.Builder()
                .subject(username)
                .issuer(ISSUER)
                .claim("username", username)
                .claim("roles", rolesAsString)
                .expirationTime(new Date(date.getTime() + Integer.parseInt(TOKEN_EXPIRE_TIME)))
                .build();
    }

    private JWSObject createHeaderAndPayload(JWTClaimsSet claimsSet) {
        return new JWSObject(new JWSHeader(JWSAlgorithm.HS256), new Payload(claimsSet.toJSONObject()));
    }

    private String signTokenWithSecretKey(JWSObject jwsObject) {
        try {
            JWSSigner signer = new MACSigner(SECRET_KEY.getBytes());
            jwsObject.sign(signer);
            return jwsObject.serialize();
        } catch (JOSEException e) {
            throw new RuntimeException("Signing failed", e);
        }
    }

    public SignedJWT parseTokenAndVerify(String token) throws ParseException, JOSEException, AuthorizationException {
        SignedJWT signedJWT = SignedJWT.parse(token);
        JWSVerifier verifier = new MACVerifier(SECRET_KEY.getBytes());

        if (!signedJWT.verify(verifier)) {
            throw new AuthorizationException(401, "Invalid token signature");
        }
        return signedJWT;
    }

    public UserDTO getJWTClaimsSet(JWTClaimsSet claimsSet) throws AuthorizationException {

        if (new Date().after(claimsSet.getExpirationTime()))
            throw new AuthorizationException(401, "Token is expired");

        String username = claimsSet.getClaim("username").toString();
        String roles = claimsSet.getClaim("roles").toString();
        String[] rolesArray = roles.split(",");

        return new UserDTO(username, rolesArray);
    }

}
```

TokenFactory: JWT main handler:

```Java
package dk.lyngby.security;

import com.fasterxml.jackson.core.JsonProcessingException;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.nimbusds.jose.JOSEException;
import com.nimbusds.jwt.JWTClaimsSet;
import com.nimbusds.jwt.SignedJWT;
import dk.lyngby.config.ApplicationConfig;
import dk.lyngby.dto.UserDTO;
import dk.lyngby.exception.ApiException;
import dk.lyngby.exception.AuthorizationException;
import lombok.AccessLevel;
import lombok.NoArgsConstructor;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.io.IOException;
import java.text.ParseException;
import java.util.*;

@NoArgsConstructor(access = AccessLevel.PRIVATE)
public class TokenFactory {

    // Singleton
    private static TokenFactory instance;

    // Properties
    private final String ISSUER = Objects.requireNonNull(getProperties())[0];
    private final String TOKEN_EXPIRE_TIME = Objects.requireNonNull(getProperties())[1];
    private final String SECRET_KEY = Objects.requireNonNull(getProperties())[2];

    // Logger
    private final Logger LOGGER = LoggerFactory.getLogger(TokenFactory.class);

    // SignToken class
    private final SignVerifyToken signature = new SignVerifyToken(ISSUER, TOKEN_EXPIRE_TIME, SECRET_KEY);

    public static TokenFactory getInstance() {
        if (instance == null) {
            instance = new TokenFactory();
        }
        return instance;
    }

    // Get properties from pom file
    private String[] getProperties() {
        try {
            String[] properties = new String[3];
            properties[0] = ApplicationConfig.getProperty("issuer");
            properties[1] = ApplicationConfig.getProperty("token.expiration.time");
            properties[2] = ApplicationConfig.getProperty("secret.key");
            return properties;
        } catch (IOException e) {
            LOGGER.error("Could not get properties", e);
        }
        return null;
    }

    public String[] parseJsonObject(String jsonString, Boolean tryLogin) throws ApiException {
        try {
            List<String> roles = Arrays.asList("user", "admin", "manager");

            ObjectMapper mapper = new ObjectMapper();
            Map json = mapper.readValue(jsonString, Map.class);
            String username = json.get("username").toString();
            String password = json.get("password").toString();
            String role = "";

            if (!tryLogin) {
                role = json.get("role").toString();
                if (!roles.contains(role)) throw new ApiException(400, "Role not valid");
            }

            return new String[]{username, password, role};

        } catch (JsonProcessingException | NullPointerException e) {
            throw new ApiException(400, "Malformed JSON Supplied");
        }
    }

    public String createToken(String userName, Set<String> roles) throws ApiException {

        try {
            StringBuilder res = new StringBuilder();
            for (String string : roles) {
                res.append(string);
                res.append(",");
            }

            String rolesAsString = !res.isEmpty() ? res.substring(0, res.length() - 1) : "";

            Date date = new Date();
            return signature.signToken(userName, rolesAsString, date);
        } catch (JOSEException e) {
            throw new ApiException(500, "Could not create token");
        }
    }

    public UserDTO verifyToken(String token) throws ApiException, AuthorizationException {
        try {
            SignedJWT signedJWT = signature.parseTokenAndVerify(token);
            JWTClaimsSet claimsSet = signedJWT.getJWTClaimsSet();
            return signature.getJWTClaimsSet(claimsSet);
        } catch (ParseException | JOSEException e) {
            throw new ApiException(401, e.getMessage());
        }
    }
}
```

Then we need to add an exception class:

```Java
package dk.lyngby.exception;

import lombok.Getter;

@Getter
public class AuthorizationException extends Exception {
    private final int statusCode;

    public AuthorizationException(int statusCode, String message) {
        super(message);
        this.statusCode = statusCode;
    }
}

```

## 3. User authentication (users and roles)

Next up, we need to add two entities. User and Role. So add these two classes in the `model` package:

Role entity:

```Java
package dk.lyngby.model;

import jakarta.persistence.*;
import lombok.Getter;
import lombok.NoArgsConstructor;

import java.io.Serial;
import java.io.Serializable;
import java.util.List;
import java.util.Objects;

@Entity
@Table(name = "roles")
@NamedQueries(@NamedQuery(name = "Role.deleteAllRows", query = "DELETE from Role"))
@Getter
@NoArgsConstructor
public class Role implements Serializable {

    @Serial
    private static final long serialVersionUID = 1L;

    @Id
    @Basic(optional = false)
    @Column(name = "role_name", length = 20)
    private String roleName;

    @ManyToMany(mappedBy = "roleList")
    private List<User> userList;

    public Role(String roleName) {
        this.roleName = roleName;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Role role = (Role) o;
        return Objects.equals(roleName, role.roleName);
    }

    @Override
    public int hashCode() {
        return Objects.hash(roleName);
    }
}
```

User entity: notice how the password is hashed in the constructor by `BCrypt.hashpw(userPassword, BCrypt.gensalt()`, and
how the password is verified by `BCrypt.checkpw(pw, userPassword)`:

```Java
package dk.lyngby.model;

import jakarta.persistence.*;
import lombok.Getter;
import lombok.NoArgsConstructor;
import org.mindrot.jbcrypt.BCrypt;

import java.io.Serial;
import java.io.Serializable;
import java.util.LinkedHashSet;
import java.util.Set;

@Entity
@Table(name = "users")
@NamedQueries(@NamedQuery(name = "User.deleteAllRows", query = "DELETE from User"))
@Getter
@NoArgsConstructor
public class User implements Serializable {

    @Serial
    private static final long serialVersionUID = 1L;

    @Id
    @Basic(optional = false)
    @Column(name = "user_name", length = 25)
    private String username;

    @Basic(optional = false)
    @Column(name = "user_password", length = 255, nullable = false)
    private String userPassword;

    @JoinTable(name = "user_roles", joinColumns = {
            @JoinColumn(name = "user_name", referencedColumnName = "user_name")}, inverseJoinColumns = {
            @JoinColumn(name = "role_name", referencedColumnName = "role_name")})
    @ManyToMany(fetch = FetchType.EAGER)
    private Set<Role> roleList = new LinkedHashSet<>();

    public User(String username, String userPassword) {
        this.username = username;
        this.userPassword = BCrypt.hashpw(userPassword, BCrypt.gensalt());
    }

    public Set<String> getRolesAsStrings() {
        if (roleList.isEmpty()) {
            return null;
        }
        Set<String> rolesAsStrings = new LinkedHashSet<>();
        roleList.forEach((role) -> {
            rolesAsStrings.add(role.getRoleName());
        });
        return rolesAsStrings;
    }
    public boolean verifyPassword(String pw) {
        return BCrypt.checkpw(pw, userPassword);
    }

    public void setUserPassword(String userPassword) {
        this.userPassword = BCrypt.hashpw(userPassword, BCrypt.gensalt());
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public void addRole(Role userRole) {
        roleList.add(userRole);
    }

}
```

Then add a UserDTO:

```Java
package dk.lyngby.dto;

import dk.lyngby.model.User;
import lombok.Getter;
import lombok.NoArgsConstructor;
import lombok.ToString;

import java.util.ArrayList;
import java.util.List;
import java.util.Set;

@Getter
@ToString
@NoArgsConstructor
public class UserDTO {

    private String username;
    private Set<String> roles;

    public UserDTO(String username, String[] roles) {
        this.username = username;
        this.roles = Set.of(roles);
    }

    public UserDTO(User user) {
        this.username = user.getUsername();
        this.roles = user.getRolesAsStrings();
    }

    public static List<UserDTO> toUserDTOList(List<User> users) {
        List<UserDTO> userDTOList =  new ArrayList<>();
        for (User user : users) {
            userDTOList.add(new UserDTO(user.getUsername(), user.getRolesAsStrings().toArray(new String[0])));
        }
        return userDTOList;

    }

    public String getUsername() {
        return username;
    }

    public Set<String> getRoles() {
        return roles;
    }

}
```

## 3. Routing with added roles

Next is adding routing for the authentication (routes package):

```Java
package dk.lyngby.routes;

import dk.lyngby.controller.impl.UserController;
import dk.lyngby.security.RouteRoles;
import io.javalin.apibuilder.EndpointGroup;

import static io.javalin.apibuilder.ApiBuilder.path;
import static io.javalin.apibuilder.ApiBuilder.post;

public class UserRoutes {
    private final UserController userController = new UserController();

    protected EndpointGroup getRoutes() {

        return () -> {
            path("/auth", () -> {
                post("/login", userController::login, RouteRoles.ANYONE);
                post("/register", userController::register, RouteRoles.ANYONE);
            });
        };
    }
}
```

Notice how anyone can access the `/login` and `register` endpoints. Which makes sense right?

Update Routes.java like this:

```Java
package dk.lyngby.routes;

import dk.lyngby.controller.impl.ExceptionController;
import dk.lyngby.exception.ApiException;
import dk.lyngby.exception.AuthorizationException;
import io.javalin.Javalin;
import io.javalin.apibuilder.EndpointGroup;
import io.javalin.http.Context;
import io.javalin.validation.ValidationException;
import org.hibernate.exception.ConstraintViolationException;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import static io.javalin.apibuilder.ApiBuilder.path;

public class Routes {

    private final ExceptionController exceptionController = new ExceptionController();
    private int count = 0;

    private final HotelRoute hotelRoute = new HotelRoute();
    private final RoomRoute roomRoute = new RoomRoute();
    private final UserRoutes userRoutes = new UserRoutes();

    private final Logger LOGGER = LoggerFactory.getLogger(Routes.class);

    private void requestInfoHandler(Context ctx) {
        String requestInfo = ctx.req().getMethod() + " " + ctx.req().getRequestURI();
        ctx.attribute("requestInfo", requestInfo);
    }

    public EndpointGroup getRoutes(Javalin app) {
        return () -> {
            app.before(this::requestInfoHandler);

            app.routes(() -> {
                path("/", userRoutes.getRoutes());
                path("/", hotelRoute.getRoutes());
                path("/", roomRoute.getRoutes());
            });

            app.after(ctx -> LOGGER.info(" Request {} - {} was handled with status code {}", count++, ctx.attribute("requestInfo"), ctx.status()));

            app.exception(ConstraintViolationException.class, exceptionController::constraintViolationExceptionHandler);
            app.exception(ValidationException.class, exceptionController::validationExceptionHandler);
            app.exception(ApiException.class, exceptionController::apiExceptionHandler);
            app.exception(AuthorizationException.class, exceptionController::exceptionHandlerNotAuthorized);
            app.exception(Exception.class, exceptionController::exceptionHandler);

        };
    }
}
```

This class has been seriously updated. Notice the exception handling that wasn't there before, and for that to work, we 
need to add the `UserController` in the `controller.impl` package:

```Java
package dk.lyngby.controller.impl;

import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.node.ObjectNode;
import dk.lyngby.config.HibernateConfig;
import dk.lyngby.dao.impl.UserDao;
import dk.lyngby.exception.ApiException;
import dk.lyngby.exception.AuthorizationException;
import dk.lyngby.model.User;
import dk.lyngby.security.TokenFactory;
import io.javalin.http.Context;
import jakarta.persistence.EntityManagerFactory;

import java.util.Set;

public class UserController {

    private final UserDao userDao;
    private final TokenFactory tokenFactory = TokenFactory.getInstance();

    public UserController() {
        EntityManagerFactory emf = HibernateConfig.getEntityManagerFactory();
        userDao = UserDao.getInstance(emf);
    }

    public void login(Context ctx) throws ApiException, AuthorizationException {
        String[] userInfos = getUserInfos(ctx, true);
        User user = getVerfiedOrRegisterUser(userInfos[0], userInfos[1], "", false);
        String token = getToken(userInfos[0], user.getRolesAsStrings());

        // Create response
        ctx.status(200);
        ctx.result(createResponse(userInfos[0], token));
    }

    public void register(Context ctx) throws ApiException, AuthorizationException {
        String[] userInfos = getUserInfos(ctx, false);
        User user = getVerfiedOrRegisterUser(userInfos[0], userInfos[1], userInfos[2], true);
        String token = getToken(userInfos[0], user.getRolesAsStrings());

        // Create response
        ctx.res().setStatus(201);
        ctx.result(createResponse(userInfos[0], token));
    }

    private String createResponse(String username, String token) {
        ObjectMapper mapper = new ObjectMapper();
        ObjectNode responseJson = mapper.createObjectNode();
        responseJson.put("username", username);
        responseJson.put("token", token);
        return responseJson.toString();
    }

    private String[] getUserInfos(Context ctx, boolean tryLogin) throws ApiException {
        String request = ctx.body();
        return tokenFactory.parseJsonObject(request, tryLogin);
    }

    private User getVerfiedOrRegisterUser(String username, String password, String role, boolean isCreate) throws AuthorizationException {
        return isCreate ? userDao.registerUser(username, password, role) : userDao.getVerifiedUser(username, password);
    }

    private String getToken(String username, Set<String> userRoles) throws ApiException {
        return tokenFactory.createToken(username, userRoles);
    }
}
```

And then we need a `UserDao` in the `dao/impl` package:

```Java
package dk.lyngby.dao.impl;

import dk.lyngby.dao.IDao;
import dk.lyngby.exception.AuthorizationException;
import dk.lyngby.model.Role;
import dk.lyngby.model.User;
import jakarta.persistence.EntityManager;
import jakarta.persistence.EntityManagerFactory;

import java.util.List;

public class UserDao implements IDao<User, String> {

    private static UserDao instance;
    private static EntityManagerFactory emf;

    public static UserDao getInstance(EntityManagerFactory _emf) {
        if (instance == null) {
            emf = _emf;
            instance = new UserDao();
        }
        return instance;
    }

    public User getVerifiedUser(String username, String password) throws AuthorizationException {

        try (EntityManager em = emf.createEntityManager()) {
            em.getTransaction().begin();
            User user = em.find(User.class, username);

            if (user == null || !user.verifyPassword(password)) {
                throw new AuthorizationException(401, "Invalid user name or password");
            }
            em.getTransaction().commit();
            return user;
        }
    }

    public User registerUser(String username, String password, String user_role) throws AuthorizationException {

        try (EntityManager em = emf.createEntityManager()) {
            em.getTransaction().begin();

            User user = new User(username, password);
            Role role = em.find(Role.class, user_role);

            if (role == null) {
                role = createRole(user_role);
            }

            user.addRole(role);
            em.persist(user);
            em.getTransaction().commit();
            return user;
        } catch (Exception e) {
            throw new AuthorizationException(400, "Username already exists");
        }
    }

    public Role createRole(String role) {
        try (EntityManager em = emf.createEntityManager()) {
            em.getTransaction().begin();
            Role newRole = new Role(role);
            em.persist(newRole);
            em.getTransaction().commit();
            return newRole;
        }
    }

    @Override
    public User read(String userName) {
        try (var em = emf.createEntityManager()) {
            em.getTransaction().begin();
            User user = em.find(User.class, userName);
            em.getTransaction().commit();
            return user;
        }
    }

    @Override
    public List<User> readAll() {
        try (var em = emf.createEntityManager()) {
            em.getTransaction().begin();
            List<User> users = em.createQuery("SELECT u FROM User u", User.class).getResultList();
            em.getTransaction().commit();
            return users;
        }
    }

    @Override
    public User create(User user) {
        throw new UnsupportedOperationException("Use register instead");
    }

    @Override
    public User update(String userName, User user) {
        try (var em = emf.createEntityManager()) {
            em.getTransaction().begin();
            User userToUpdate = em.find(User.class, userName);
            userToUpdate.setUsername(user.getUsername());
            userToUpdate.setUserPassword(user.getUserPassword());
            em.getTransaction().commit();
            return userToUpdate;
        }
    }

    @Override
    public void delete(String userName) {
        try (var em = emf.createEntityManager()) {
            em.getTransaction().begin();
            User user = em.find(User.class, userName);
            em.remove(user);
            em.getTransaction().commit();
        }
    }

    @Override
    public boolean validatePrimaryKey(String userName) {
        try (var em = emf.createEntityManager()) {
            em.getTransaction().begin();
            User user = em.find(User.class, userName);
            em.getTransaction().commit();
            return user != null;
        }
    }
}
```

The `ExceptionController` need an update:

```Java
package dk.lyngby.controller.impl;

import dk.lyngby.exception.ApiException;
import dk.lyngby.exception.AuthorizationException;
import dk.lyngby.exception.Message;
import dk.lyngby.exception.ValidationMessage;
import dk.lyngby.routes.Routes;
import io.javalin.http.Context;
import io.javalin.validation.ValidationError;
import io.javalin.validation.ValidationException;
import org.hibernate.exception.ConstraintViolationException;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Map;

public class ExceptionController {
    private final Logger LOGGER = LoggerFactory.getLogger(Routes.class);
    public void exceptionHandlerNotAuthorized(AuthorizationException e, Context ctx) {
        LOGGER.error(ctx.attribute("requestInfo") + " " + ctx.res().getStatus() + " " + e.getMessage());
        ctx.status(e.getStatusCode());
        ctx.json(new Message(e.getStatusCode(), e.getMessage()));
    }

    public void validationExceptionHandler(ValidationException e, Context ctx) {
        LOGGER.error(ctx.attribute("requestInfo") + " " + ctx.res().getStatus() + " " + ctx.body());

        Map<String, List<ValidationError<Object>>> errors = e.getErrors();
        List<ValidationError<Object>> errorList = new ArrayList<>();
        int statusCode = 0;

        if (errors.containsKey("id")) {
            errorList = errors.get("id");
            statusCode = 404;
        }

        if (errors.containsKey("REQUEST_BODY")) {
            errorList = errors.get("REQUEST_BODY");
            statusCode = 400;
        }

        String message = errorList.get(0).getMessage();
        Map<String, Object> args = errorList.get(0).getArgs();
        Object value = errorList.get(0).getValue();

        ctx.status(statusCode);
        ctx.json(new ValidationMessage(message, args, value));
    }

    public void constraintViolationExceptionHandler(ConstraintViolationException e, Context ctx) {
        LOGGER.error(ctx.attribute("requestInfo") + " " + ctx.res().getStatus() + " " + ctx.body());
        ctx.status(500);
        ctx.json(new Message(e.getErrorCode(), e.getSQLException().getMessage()));
    }

    public void apiExceptionHandler(ApiException e, Context ctx) {
        LOGGER.error(ctx.attribute("requestInfo") + " " + ctx.res().getStatus() + " " + e.getMessage());
        ctx.status(e.getStatusCode());
        ctx.json(new Message(e.getStatusCode(), e.getMessage()));
    }

    public void exceptionHandler(Exception e, Context ctx) {
        LOGGER.error(ctx.attribute("requestInfo") + " " + ctx.res().getStatus() + " " + e.getMessage());

        System.out.println("======================================");
        System.out.println(Arrays.toString(e.getStackTrace()));
        System.out.println("======================================");

        ctx.status(500);
        ctx.json(new Message(500, e.getMessage()));
    }
}
```

And for that to work, we need a multilined `ValidationMessage` in the `exception` package:

```Java
package dk.lyngby.exception;

import java.util.Map;

public record ValidationMessage(String message, Map<String, Object> args, Object value) {
}
```

## 4. Update the Hotel and Room routing with access roles

To add access control we first need to add an AccessController in the `controller/impl` package:

```Java
package dk.lyngby.controller.impl;

import dk.lyngby.dto.UserDTO;
import dk.lyngby.exception.ApiException;
import dk.lyngby.exception.AuthorizationException;
import dk.lyngby.security.RouteRoles;
import dk.lyngby.security.TokenFactory;
import io.javalin.http.Context;
import io.javalin.http.Handler;
import io.javalin.security.RouteRole;

import java.util.Set;

public class AccessManagerController {

    private final TokenFactory TOKEN_FACTORY = TokenFactory.getInstance();

    public void accessManagerHandler(Handler handler, Context ctx, Set<? extends RouteRole> permittedRoles) throws Exception {
        String path = ctx.path();
        boolean isAuthorized = false;

        if (path.equals("/api/v1/auth/login") || path.equals("/api/v1/auth/register") || path.equals("/api/v1/routes") || permittedRoles.contains(RouteRoles.ANYONE)) {
            handler.handle(ctx);
            return;
        } else {
            RouteRole[] userRole = getUserRole(ctx);
            for (RouteRole role : userRole) {
                if (permittedRoles.contains(role)) {
                    isAuthorized = true;
                    break;
                }
            }
        }

        if (isAuthorized) {
            handler.handle(ctx);
        } else {
            throw new AuthorizationException(401, "You are not authorized to perform this action");
        }
    }

    private RouteRole[] getUserRole(Context ctx) throws AuthorizationException, ApiException {
        String token = ctx.header("Authorization").split(" ")[1];
        UserDTO userDTO = TOKEN_FACTORY.verifyToken(token);

        if (userDTO == null) {
            throw new ApiException(401, "Invalid token");
        }

        return userDTO.getRoles().stream().map(r -> RouteRoles.valueOf(r.toUpperCase())).toArray(RouteRole[]::new);
    }

}
```

Then we need to update the routing for Hotel and Room with access roles:

```Java
package dk.lyngby.routes;

import dk.lyngby.controller.impl.HotelController;
import dk.lyngby.security.RouteRoles;
import io.javalin.apibuilder.EndpointGroup;

import static io.javalin.apibuilder.ApiBuilder.*;

public class HotelRoute {

    private final HotelController hotelController = new HotelController();

    protected EndpointGroup getRoutes() {

        return () -> {
            path("/hotels", () -> {
                post("/", hotelController::create, RouteRoles.ADMIN, RouteRoles.MANAGER);
                get("/", hotelController::readAll, RouteRoles.ANYONE);
                get("/{id}", hotelController::read, RouteRoles.USER, RouteRoles.ADMIN, RouteRoles.MANAGER);
                put("/{id}", hotelController::update, RouteRoles.ADMIN, RouteRoles.MANAGER);
                delete("/{id}", hotelController::delete, RouteRoles.ADMIN, RouteRoles.MANAGER);
            });
        };
    }
}
```

```Java
package dk.lyngby.routes;

import dk.lyngby.controller.impl.RoomController;
import dk.lyngby.security.RouteRoles;
import io.javalin.apibuilder.EndpointGroup;

import static io.javalin.apibuilder.ApiBuilder.*;

public class RoomRoute {

    private final RoomController roomController = new RoomController();

    protected EndpointGroup getRoutes() {

        return () -> {
            path("/rooms", () -> {
                post("/hotel/{id}", roomController::create, RouteRoles.ADMIN, RouteRoles.MANAGER);
                get("/", roomController::readAll, RouteRoles.ANYONE);
                get("/{id}", roomController::read, RouteRoles.ADMIN, RouteRoles.MANAGER);
                put("/{id}", roomController::update, RouteRoles.ADMIN, RouteRoles.MANAGER);
                delete("/{id}", roomController::delete, RouteRoles.ADMIN, RouteRoles.MANAGER);
            });
        };
    }
}
```

Finally, update the ApplicationConfig.java file in the `config` package to add the AccessManagerHandler and
some extra loggin:

```Java
package dk.lyngby.config;

import dk.lyngby.controller.impl.AccessManagerController;
import dk.lyngby.routes.Routes;
import io.javalin.Javalin;
import io.javalin.config.JavalinConfig;
import io.javalin.plugin.bundled.RouteOverviewPlugin;
import lombok.NoArgsConstructor;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.io.IOException;
import java.io.InputStream;
import java.util.Properties;

@NoArgsConstructor(access = lombok.AccessLevel.PRIVATE)
public class ApplicationConfig {

    private static final AccessManagerController ACCESS_MANAGER_HANDLER = new AccessManagerController();
    private static final Logger LOGGER = LoggerFactory.getLogger(ApplicationConfig.class);

    private static void configuration(JavalinConfig config) {
        config.routing.contextPath = "/api/v1"; // base path for all routes
        config.http.defaultContentType = "application/json"; // default content type for requests
        config.plugins.register(new RouteOverviewPlugin("/")); // enables route overview at /
        config.accessManager(ACCESS_MANAGER_HANDLER::accessManagerHandler);
    }

    public static void startServer(Javalin app, int port) {
        Routes routes = new Routes();
        app.updateConfig(ApplicationConfig::configuration);
        app.routes(routes.getRoutes(app));
        HibernateConfig.setTest(false);
        app.start(port);
    }

    public static void stopServer(Javalin app) {
        app.stop();
    }

    public static String getProperty(String propName) throws IOException
    {
        try (InputStream is = HibernateConfig.class.getClassLoader().getResourceAsStream("properties-from-pom.properties"))
        {
            Properties prop = new Properties();
            prop.load(is);
            return prop.getProperty(propName);
        } catch (IOException ex) {
            LOGGER.error("Could not read property from pom file. Build Maven!");
            throw new IOException("Could not read property from pom file. Build Maven!");
        }
    }
}
```

## 5. Try it out - add some .http files

First add a `auth.http` file in the `ressource/http` folder:

```console
### Register user/admin
POST {{url}}/auth/register
Content-Type: application/json

{
  "username": "admin",
  "password": "admin",
  "role": "admin"
}

> {% client.global.set("token", response.body.json.token); %}

### Register user/user
POST {{url}}/auth/register
Content-Type: application/json

{
  "username": "user",
  "password": "user",
  "role": "user"
}

### Register user_manager/manager
POST {{url}}/auth/register
Content-Type: application/json

{
  "username": "manager",
  "password": "manager",
  "role": "manager"
}

> {% client.global.set("token", response.body.token); %}

### Login as admin
POST {{url}}/auth/login
Content-Type: application/json

{
  "username": "admin",
  "password": "admin"
}

> {% client.global.set("token", response.body.token); %}

### Login as user
POST {{url}}/auth/login
Content-Type: application/json

{
  "username": "user",
  "password": "user"
}
> {% client.global.set("token", response.body.token); %}


### Login as manager
POST {{url}}/auth/login
Content-Type: application/json

{
  "username": "manager",
  "password": "manager"
}

> {% client.global.set("token", response.body.token); %}

###
```

Next update the `dev.http` file:

```Console
// Hotel API

GET {{url}}/hotels
Authorization: Bearer {{token}}

###

GET {{url}}/hotels/6
Authorization: Bearer {{token}}

###

POST {{url}}/hotels
Content-Type: application/json
Authorization: Bearer {{token}}

{
  "hotelName": "Radisson",
  "hotelAddress": "Sindelfingen",
  "hotelType": "BUDGET"
}

###

PUT {{url}}/hotels/200
Content-Type: application/json
Authorization: Bearer {{token}}

{
  "hotelName": "Scandic",
  "hotelAddress": "Lyngby Hovedgade",
  "hotelType": "BUDGET"
}

###

DELETE {{url}}/hotels/54
Authorization: Bearer {{token}}

###

// Room API

GET {{url}}/rooms
Authorization: Bearer {{token}}

###

GET {{url}}/rooms/100
Authorization: Bearer {{token}}

###

POST {{url}}/rooms/hotel/9
Content-Type: application/json
Authorization: Bearer {{token}}

{
  "roomNumber": 112,
  "roomPrice": 1150,
  "roomType": "SINGLE"
}
```

Finally, the time has come to give it a spin

