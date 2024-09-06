---
title: DTO and JSON
description: How to convert DTOs to JSON and vice versa
layout: default
parent: Data Integration
grand_parent: Toolbox
nav_order: 5
permalink: /toolbox/dataintegration/dto-conversions/
---

# DTO conversions using Jackson

## JSON to DTO

This page shows process of converting JSON to a DTO in Java using **Lombok** to simplify the DTO class.

### What is Lombok?

Lombok is a Java library that helps reduce boilerplate code by generating common methods like getters, setters, constructors, `toString()`, `equals()`, and `hashCode()` at compile time using annotations. This helps make DTOs cleaner and easier to maintain.

### 1. Adding Dependencies for Lombok and Jackson

If you're using **Maven**, add the following dependencies to your `pom.xml` file:

```xml
<!-- Jackson for JSON handling -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.13.0</version> <!-- or the latest version -->
</dependency>

<!-- Lombok for reducing boilerplate code -->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.20</version> <!-- or the latest version -->
    <scope>provided</scope>
</dependency>
```

### 2. Example JSON

Assume we have the following JSON that we want to map to a DTO:

```json
{
  "name": "Alice",
  "age": 30,
  "email": "alice@example.com"
}
```

### 3. DTO Class Using Lombok

Using Lombok, we can avoid manually writing getters, setters, constructors, and `toString()` methods by using appropriate Lombok annotations.

```java
import lombok.Data;

@Data
public class UserDTO {
    private String name;
    private int age;
    private String email;
}
```

### Lombok Annotations Explained

- **`@Data`:** This is a combination of several Lombok annotations:
  - `@Getter` and `@Setter` (generates getters and setters for all fields),
  - `@ToString` (generates a `toString()` method),
  - `@EqualsAndHashCode` (generates `equals()` and `hashCode()` methods),
  - `@RequiredArgsConstructor` (generates a constructor for `final` fields).

So the `UserDTO` class now automatically has all the necessary methods without having to manually write them.

### 4. Converting JSON to DTO Using Jackson and Lombok

You can now use **Jackson**'s `ObjectMapper` to convert the JSON string to the `UserDTO` object.

```java
import com.fasterxml.jackson.databind.ObjectMapper;

public class JsonToDtoWithLombokExample {
    public static void main(String[] args) {
        // Example JSON string
        String json = "{ \"name\": \"Alice\", \"age\": 30, \"email\": \"alice@example.com\" }";
        
        // Create ObjectMapper instance
        ObjectMapper objectMapper = new ObjectMapper();

        try {
            // Convert JSON string to UserDTO
            UserDTO user = objectMapper.readValue(json, UserDTO.class);
            
            // Print the UserDTO object
            System.out.println(user);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### 5. Explanation

- **`ObjectMapper.readValue(String content, Class<T> valueType)`**: This method reads the JSON string and converts it into a Java object of the specified class (`UserDTO` in this case).
- Thanks to Lombok, you don’t need to write getters, setters, or the `toString()` method in the `UserDTO` class.

### Output

When you run this code, it will print the `UserDTO` object:

```
UserDTO(name=Alice, age=30, email=alice@example.com)
```

### Customizing Field Names (Optional)

If the field names in the JSON are different from the DTO fields, you can use Jackson's `@JsonProperty` annotation to map them. Here’s an example:

```java
import com.fasterxml.jackson.annotation.JsonProperty;
import lombok.Data;

@Data
public class UserDTO {
    @JsonProperty("full_name")
    private String name;

    @JsonProperty("user_age")
    private int age;

    @JsonProperty("user_email")
    private String email;
}
```

In this case, the JSON would have fields like `"full_name"`, `"user_age"`, and `"user_email"`, but these would map to the `name`, `age`, and `email` fields of the DTO.

### Conclusion

Using Lombok reduces boilerplate code in your DTOs, making your code cleaner and easier to maintain. Combined with Jackson, it becomes very easy to convert JSON into DTOs in Java

## DTO to JSON

Converting a DTO (Data Transfer Object) to JSON in Java can be done using libraries like **Jackson**. This process is called **serialization**, where you convert a Java object into a JSON string.

Let’s walk through an example using **Jackson** and **Lombok**.

### 1. Adding Dependencies

If you're using Maven, ensure you have the following dependencies for **Jackson** and **Lombok**:

```xml
<!-- Jackson for JSON serialization -->
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.13.0</version> <!-- or the latest version -->
</dependency>

<!-- Lombok for reducing boilerplate code -->
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.20</version> <!-- or the latest version -->
    <scope>provided</scope>
</dependency>
```

### 2. DTO Class Using Lombok

Here’s an example of a simple DTO using Lombok's `@Data` annotation to avoid writing boilerplate code (like getters, setters, `toString()`, etc.).

```java
import lombok.Data;

@Data
public class UserDTO {
    private String name;
    private int age;
    private String email;
}
```

### 3. Converting DTO to JSON

Now, let's write the code to create a `UserDTO` object and convert it to a JSON string using **Jackson**.

```java
import com.fasterxml.jackson.databind.ObjectMapper;

public class DtoToJsonExample {
    public static void main(String[] args) {
        // Create a new UserDTO object
        UserDTO user = new UserDTO();
        user.setName("Alice");
        user.setAge(30);
        user.setEmail("alice@example.com");

        // Create an ObjectMapper instance
        ObjectMapper objectMapper = new ObjectMapper();

        try {
            // Convert the UserDTO object to a JSON string
            String json = objectMapper.writeValueAsString(user);
            
            // Print the JSON string
            System.out.println(json);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### Explanation

- **`ObjectMapper.writeValueAsString(Object value)`**: This method is used to convert a Java object (in this case, `UserDTO`) into a JSON string.
- The DTO `UserDTO` object is serialized into JSON format using Jackson.

### Output

When you run the program, it will print the following JSON string:

```json
{
  "name": "Alice",
  "age": 30,
  "email": "alice@example.com"
}
```

### Customizing the JSON Output

If you need to customize the field names in the generated JSON (for example, to match an API requirement), you can use Jackson’s `@JsonProperty` annotation in the DTO class.

```java
import com.fasterxml.jackson.annotation.JsonProperty;
import lombok.Data;

@Data
public class UserDTO {
    @JsonProperty("full_name")
    private String name;

    @JsonProperty("user_age")
    private int age;

    @JsonProperty("user_email")
    private String email;
}
```

Now, when you convert the DTO to JSON, the output will look like this:

```json
{
  "full_name": "Alice",
  "user_age": 30,
  "user_email": "alice@example.com"
}
```

### Conclusion

Converting a DTO to JSON in Java using **Jackson** is straightforward. By using **Lombok** for the DTO and **Jackson** for serialization, you can easily convert a Java object to a JSON string with minimal boilerplate code.
