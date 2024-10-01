---
title: Poems API Security
description: Adding a security layer to the Poems API
layout: default
nav_order: 6
grand_parent: Rest API Test and Security
parent: Exercises
permalink: /rest-test-security/exercises/poems-security/
---

# Security layer for Poems API (To do in class on Thursday)

In this exercise, you will add a security layer to the Poems API. The goal is to make sure that only authenticated users can access the API.
We will use JWT (JSON Web Tokens) to secure the API.
We will need to add registration and login endpoints to the API.

## Creating the User and Role entities

1. Create a User entity with the following fields:
    - id
    - username
    - password
    - roles (Set<Role>)
2. The User should also implement ISecurityUser with the following methods:

```java
boolean verifyPassword(String pw); // using BCrypt
void addRole(Role role);
```

3. When creating the User entity, the password should be hashed using BCrypt.

## Creating Security DAO that implements the following interface methods

```java
UserDTO getVerifiedUser(String username, String password) throws ValidationException;
User createUser(String username, String password);
```

## Security Controller

1. Create a SecurityController that implements the following interface:

```java
public interface ISecurityController {
    Handler login(); // to get a token
    Handler register(); // to get a user
    Handler authenticate(); // to use in a before filter to verify the token and unpack the user - add the user to the context.
    boolean authorize(UserDTO userDTO, Set<String> allowedRoles); // to verify user roles against "allowed roles"
    String createToken(UserDTO user) throws Exception;
    UserDTO verifyToken(String token) throws Exception;
}
```

## Security Filter

1. In the ApplicationConfig file, add a SecurityFilter, that looks to see if the user has the correct roles to access the endpoint:

```java
        app.beforeMatched(ctx -> { // Before matched is different from before, in that it is not called for 404 etc.
            if (ctx.routeRoles().isEmpty())
                return; // No roles needed for this route

            // 1. Get permitted roles
            Set<String> allowedRoles = ctx.routeRoles().stream().map(role -> role.toString().toUpperCase()).collect(Collectors.toSet());
            if (allowedRoles.contains("ANYONE")) {
                return;
            }

            // 2. Get user roles
            UserDTO user = ctx.attribute("user");

            // 3. Compare
            if (user == null)
                ctx.status(HttpStatus.FORBIDDEN)
                        .json(jsonMapper.createObjectNode()
                                .put("msg", "Not authorized. No username were added from the token"));

            if (!SecurityController.getInstance().authorize(user, allowedRoles)) {
                System.out.println("USER: " + user + " is not authorized. Needed roles are: " + allowedRoles);
                // throw new UnAuthorizedResponse(); // version 6 migration guide
                throw new ApiException(HttpStatus.FORBIDDEN.getCode(), "Unauthorized with roles: " + user.getRoles() + ". Needed roles are: " + allowedRoles);
            }
```

## Create the security routes

1. Create the following routes:

    - POST /register        // Open for everyone
    - POST /login           // Open for everyone
    - GET /poems            // only for users with the role USER
    - GET /poems/{id}       // only for users with the role USER
    - POST /poems           // only for users with the role ADMIN
    - PUT /poems/{id}       // only for users with the role ADMIN
    - DELETE /poems/{id}    // only for users with the role ADMIN
