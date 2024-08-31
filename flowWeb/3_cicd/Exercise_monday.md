# Exercise JWT implementation
## Implement JWT in the Hotel API
1. Implement User and Role entities
2. Implement PasswordHashing
3. Implement Javalin security routes for `login` and `register`
4. Update the UserDAOs createUser method to add a `user`role to the user when registering
5. Create a Security Controller that implements the following interface: 
```java
    Handler register(); // creates a new User
    Handler login(); // logs in a user and returns a token
    String createToken(UserDTO user); // creates a token based on the UserDTO, sercret and expiration time
    boolean authorize(UserDTO user, Set<String> allowedRoles); // checks if the user has the required roles
    Handler authenticate(); // checks if the token is valid and adds the user (with roles) to the context
    UserDTO verifyToken(String token); 
    boolean tokenIsValid(String token, String secret) throws ParseException, JOSEException, NotAuthorizedException;
    boolean tokenNotExpired(String token) throws ParseException, NotAuthorizedException;
    UserDTO getUserWithRolesFromToken(String token) throws ParseException;
    int timeToExpire(String token) throws ParseException, NotAuthorizedException;
```
6. Check that you can login and receive a token
7. Create a new route in the Hotel API that requires a token to access (e.g. `get("/api/hotels", getHoltels, Role.USER)`).
8. Add a `before` filter to the route that uses the `authenticate` method from the SecurityController to check if the token is valid and adds the user to the context
9. In the ApplicationConfig create a new method that can extend the configuration with an accessManager that checks if the user has the required roles and allows access to the route for `Role.ANYONE`
8. Test that you can access the route with a valid token and that you cannot access the route with an invalid token
9. Create a method in the UserDAO to add a new role to a user
10. Create a new user and give them a `admin` role.
11. Make a new endpoint that requires the `admin` role to access
12. Test that you can access the route only with a token that has the `admin` role (not the user role)
13. Create RestAssured tests for the new routes (both login and register plus the new routes that require a token for both `user` and `admin` roles).

