---
title: DTO
layout: default
parent: Design patterns
nav_order: 4
permalink: /toolbox/designpatterns/dto/
grand_parent: Toolbox
---

# DTO (Data Transfer Object) Pattern

A DTO, or Data Transfer Object, is a simple object used to transfer data between different layers or parts of an application. It is often used to encapsulate the data and send it over the network or between application layers without exposing the internal implementation details of the objects. DTOs typically contain only fields and getter/setter methods, without any business logic.

## Why Use DTOs?

- **Separation of Concerns**: DTOs separate the data structure used in different layers, preventing tight coupling between them.
- **Network Efficiency**: DTOs can reduce the amount of data sent over the network by including only the necessary fields.
- **Encapsulation**: DTOs hide the internal structure and implementation of the underlying domain objects.

## Example of a DTO in Java

Let's say we have a `User` entity in our application with fields like `id`, `username`, `password`, `email`, etc. We want to expose a simplified version of this entity to the client, containing only the `username` and `email`. For this purpose, we create a `UserDTO`.

### Step 1: Define the `User` entity

```java
public class User {
    private Long id;
    private String username;
    private String password;
    private String email;

    // Constructors, getters, and setters

    public User(Long id, String username, String password, String email) {
        this.id = id;
        this.username = username;
        this.password = password;
        this.email = email;
    }

    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getPassword() {
        return password;
    }

    public void setPassword(String password) {
        this.password = password;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```

### Step 2: Define the `UserDTO`

```java
public class UserDTO {
    private String username;
    private String email;

    // Constructors, getters, and setters

    public UserDTO(String username, String email) {
        this.username = username;
        this.email = email;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }
}
```

### Step 3: Using the `UserDTO`

Imagine a scenario where we want to return user information from a service layer without exposing sensitive fields like `password`. We can convert the `User` entity to a `UserDTO` and return it to the client.

```java
public class UserService {

    public UserDTO getUserById(Long id) {
        // Normally, you would fetch this from the database
        User user = new User(id, "john_doe", "secretPassword", "john.doe@example.com");

        // Convert User to UserDTO
        UserDTO userDTO = new UserDTO(user.getUsername(), user.getEmail());

        return userDTO;
    }
}
```

### Step 4: Example Usage

```java
public class Main {
    public static void main(String[] args) {
        UserService userService = new UserService();
        UserDTO userDTO = userService.getUserById(1L);

        System.out.println("Username: " + userDTO.getUsername());
        System.out.println("Email: " + userDTO.getEmail());
    }
}
```

### Output

```
Username: john_doe
Email: john.doe@example.com
```

### Summary

In this example, the `UserDTO` is a simplified version of the `User` entity that only contains the data we want to expose. This separation ensures that we don't inadvertently expose sensitive information, such as the user's password, to the client. DTOs play an important role in clean architecture, helping to maintain the separation between different layers of an application.

## Security Considerations

A DTO (Data Transfer Object) can indeed help enhance security in several ways. By carefully designing and using DTOs, you can control and limit the exposure of sensitive data and ensure that only the necessary information is shared across different layers or systems.

### Ways DTO Enhances Security

1. **Data Exposure Control**:
   - **Selective Data Transfer**: DTOs allow you to include only the necessary fields that should be exposed to the client or other systems. For example, if your domain model includes sensitive information like passwords, social security numbers, or internal IDs, you can omit these fields from the DTO. This prevents accidental exposure of sensitive data through APIs or other communication channels.

2. **Encapsulation**:
   - **Hiding Internal Structures**: DTOs help to abstract the internal representation of data from the outside world. The underlying domain objects, which might contain complex relationships or sensitive business logic, are not exposed directly. This limits the risk of exposing internal system details that could be exploited by attackers.

3. **Validation and Sanitization**:
   - **Input Validation**: When data is received from an external source, such as a client application, it can first be mapped to a DTO. This mapping process provides an opportunity to validate and sanitize the incoming data, ensuring it meets the necessary criteria before it’s passed further into the system. For example, you can ensure that certain fields are not null, or that strings are of a certain length.
   - **Output Sanitization**: Similarly, when sending data out of your system, the use of a DTO allows you to ensure that the data is properly formatted and sanitized before it leaves your application.

4. **Minimizing Attack Surface**:
   - **Limited Data Availability**: By using DTOs to define the specific data sent over a network or exposed to a client, you reduce the attack surface. Attackers cannot access data that is not included in the DTO, even if they manage to intercept the data transfer.

5. **Prevention of Overposting/Underposting Attacks**:
   - **Overposting Protection**: Overposting occurs when an attacker sends more data than the application expects or needs, potentially altering sensitive fields. By defining a DTO with only the fields that should be updated, you can prevent attackers from manipulating other fields that are part of the underlying entity but not exposed via the DTO.
   - **Underposting Protection**: Similarly, by requiring specific fields in a DTO, you can ensure that essential data is not omitted by the client (underposting), which could otherwise lead to incomplete or invalid operations.

### Example Scenario

Imagine you have an API that allows users to update their profiles. The `User` entity might contain sensitive fields like `password`, `role`, or `accountStatus`, but these fields should not be updatable by the user through the API. By using a `UserProfileDTO`, you can expose only the fields the user is allowed to update, such as `username`, `email`, and `phoneNumber`.

```java
public class UserProfileDTO {
    private String username;
    private String email;
    private String phoneNumber;

    // Getters and Setters
}
```

By mapping the incoming data to this DTO, you ensure that the sensitive fields in the `User` entity cannot be altered via the API, thereby enhancing the security of the application.

### Summary on security

In summary, DTOs contribute to enhanced security by controlling data exposure, encapsulating internal structures, enabling validation and sanitization, minimizing the attack surface, and preventing certain types of attacks like overposting and underposting. When properly used, DTOs are an effective tool in safeguarding sensitive information and enforcing security best practices in software development.
