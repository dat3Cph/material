# Security Exercise
Use an existing Rest project from last week or create a new one. Now add security and Rest Assured tests to the project.

## Part 1 Hashing Passwords
- Create a User Entity and a Role Entity with ManyToMany relationship between them
- Create a UserDAO that implements
  - `createUser(String username, String password)`
  - `getUserByUserName(String username)`
  - `getAllUsers()`
  - `getAllRoles()`
  - `addRoleToUser(String username, String roleName)`
  - `deleteUser(String username)`


## Part 2 Login Endpoint
- Create an endpoint that can handle a login request containing a username and password.
  - The endpoint should return a JWT token if the username and password are valid.
  - The endpoint should return an error if the username and password are invalid.
  - Update the UserDAO with methods:
  - `login(String username, String password)` that returns a JWT token if the username and password are valid.
  - `boolean authorize(String username, Set<? extends RouteRole> permittedRoles);`

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