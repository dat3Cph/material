---
title: Hotel API Security
description: Adding a security layer to the Hotel API
layout: default
nav_order: 4
grand_parent: Rest API Test and Security
parent: Exercises
permalink: /rest-test-security/exercises/hotel-security/
---

# Security Exercise

Below security exercise builds on the previous weeks Rest project. Either use the Hotel project from last week or create a new Rest project to your liking. Then apply Register, Login, Password hashing, and JWT security to the project as specified below.

## Assistance

- [video help for below code examples](https://cphbusiness.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=d329a3f7-1a16-41d9-9e92-b13200c2a4b0)
- [hashing passwords video](https://cphbusiness.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=9d3b7d78-48cc-4286-8ebb-b13200acb994)
- [Code snippets](../../setup/securityCode.md)
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
  - bcrypt link: <https://www.mindrot.org/projects/jBCrypt/>
  - `<dependency><groupId>org.mindrot</groupId><artifactId>jbcrypt</artifactId><version>${jbcrypt.version}</version></dependency>`
- Hint: Hash the password in the User constructor: `BCrypt.hashpw(userPass, BCrypt.gensalt());`
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

## Part 3 Protect Endpoints

- Create an endpoint that can only be accessed by authenticated users with a role of ADMIN.
  - The endpoint should return an error if the JWT token is invalid.
  - The endpoint should return an error if the JWT token is valid but the user doesn't have the ADMIN role.
  - The endpoint should return the protected resource if the JWT token is valid.
- Add more endpoints so that there are endpoints for only USER and only ADMIN roles and endpoints that are open to all users.

## Part 4 Testing

- Use Rest Assured, JUnit 5, and Hamcrest matchers to test all the finished endpoints.
  - Test protected Endpoints by storing a valid JWT token in a variable and use it in the test.
