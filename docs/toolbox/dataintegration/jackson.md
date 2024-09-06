---
title: Jackson
description: What is Jackson and how to use it
layout: default
parent: Data Integration
grand_parent: Toolbox
nav_order: 6
permalink: /toolbox/dataintegration/jackson/
---

# What is Jackson?

**Jackson** is a popular Java library that is used for converting Java objects to and from JSON (JavaScript Object Notation). It is a powerful, flexible, and efficient library that is widely used in Java-based applications, especially for handling JSON data in RESTful APIs.

## Key Features of Jackson

1. **Serialization and Deserialization**

- **Serialization**: Converting Java objects into JSON format.
- **Deserialization**: Converting JSON strings into Java objects.
- Jackson makes it easy to perform both operations with minimal configuration.

2. **Annotations Support**

    - Jackson provides several annotations (e.g., `@JsonProperty`, `@JsonIgnore`) that allow you to control the serialization and deserialization behavior. These annotations can be used to map JSON fields to Java class fields, ignore certain fields, handle custom field names, and more.

3. **Data Binding**

    - **Simple Data Binding**: Jackson can map basic JSON data (like strings, numbers, booleans, lists, maps) directly to Java objects like `List`, `Map`, `String`, etc.
    - **Full Data Binding**: Jackson can map complex JSON data into custom Java objects (i.e., POJOs – Plain Old Java Objects), allowing fine control over how data is handled.

4. **Streaming API**

    - Jackson offers a streaming API for reading and writing JSON. It allows for parsing large JSON documents without holding the entire document in memory, which is useful when working with huge datasets.

5. **Tree Model**

    - Jackson provides a tree model (using `JsonNode`) that allows you to represent JSON data in a tree structure. This is useful when the structure of the JSON is unknown or if you want to manipulate the data more flexibly before binding it to a Java object.

6. **Custom Serializers and Deserializers**

    - Jackson allows the creation of custom serializers and deserializers to handle special cases where the default behavior is not sufficient. This is particularly useful when dealing with complex data structures or legacy systems.

## How Jackson Works

Jackson uses an object mapper, the `ObjectMapper` class, as the core tool for working with JSON data. Here’s an example of how Jackson performs serialization and deserialization:

### 1. **Serialization (Converting Java Object to JSON)**

Serialization involves converting a Java object into a JSON string.

**Example**:

```java
import com.fasterxml.jackson.databind.ObjectMapper;

public class SerializationExample {
    public static void main(String[] args) {
        try {
            ObjectMapper objectMapper = new ObjectMapper();

            // Create a Java object
            User user = new User();
            user.setName("Alice");
            user.setAge(30);
            user.setEmail("alice@example.com");

            // Convert Java object to JSON string
            String jsonString = objectMapper.writeValueAsString(user);

            // Print JSON output
            System.out.println(jsonString);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

class User {
    private String name;
    private int age;
    private String email;

    // Getters and Setters
}
```

**Output**:

```json
{
  "name": "Alice",
  "age": 30,
  "email": "alice@example.com"
}
```

### 2. **Deserialization (Converting JSON to Java Object)**

Deserialization is the reverse process, where a JSON string is converted into a Java object.

**Example**:

```java
import com.fasterxml.jackson.databind.ObjectMapper;

public class DeserializationExample {
    public static void main(String[] args) {
        try {
            ObjectMapper objectMapper = new ObjectMapper();

            // JSON string
            String jsonString = "{\"name\":\"Alice\",\"age\":30,\"email\":\"alice@example.com\"}";

            // Convert JSON string to Java object
            User user = objectMapper.readValue(jsonString, User.class);

            // Print Java object
            System.out.println("Name: " + user.getName());
            System.out.println("Age: " + user.getAge());
            System.out.println("Email: " + user.getEmail());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

**Output**:

```
Name: Alice
Age: 30
Email: alice@example.com
```

## Common Jackson Annotations

1. **`@JsonProperty`**: Used to specify the property name in JSON for a field.
2. **`@JsonIgnore`**: Used to exclude a field from serialization and deserialization.
3. **`@JsonFormat`**: Used to specify the format of date and time fields.
4. **`@JsonCreator`**: Used to define a constructor or factory method to instantiate an object during deserialization.
5. **`@JsonInclude`**: Controls the inclusion of properties in the JSON output (e.g., ignore `null` values).

## Jackson vs. Other JSON Libraries

- **Gson**: Another popular Java library for JSON processing. Gson is simpler but lacks some of the advanced features that Jackson provides (e.g., streaming API, support for more complex use cases).
- **JSON-P**: Java’s official JSON Processing API, which is lower-level and more verbose compared to Jackson, but can be useful in certain specific scenarios.

## Use Cases for Jackson

1. **REST APIs**: Jackson is widely used in Spring Boot and other Java-based frameworks for serializing and deserializing data to/from JSON in REST APIs.
2. **Configuration Files**: Jackson can be used to parse configuration files in JSON format.
3. **Data Storage and Retrieval**: Jackson is often used to convert data to JSON for storage in databases or for transferring data between services.

## Conclusion

## Common Jackson Annotations

Jackson provides a wide range of annotations to control the serialization and deserialization of Java objects to and from JSON. Here are some of the most commonly used Jackson annotations:

### 1. **`@JsonProperty`**

This annotation is used to specify the name of a field in the JSON that maps to the field in the Java object. It is helpful when the field name in the Java class doesn't match the JSON field name.

- **Example**:

  ```java
  public class User {
      @JsonProperty("full_name")
      private String name;

      @JsonProperty("user_age")
      private int age;

      // getters and setters
  }
  ```

- **JSON**:

  ```json
  {
    "full_name": "John Doe",
    "user_age": 30
  }
  ```

### 2. **`@JsonIgnore`**

This annotation is used to ignore a specific field during the serialization and deserialization process.

- **Example**:

  ```java
  public class User {
      private String name;

      @JsonIgnore
      private String password;

      // getters and setters
  }
  ```

- The `password` field will be ignored in both serialization and deserialization.

### 3. **`@JsonIgnoreProperties`**

This annotation can be used at the class level to ignore multiple properties during serialization or deserialization.

- **Example**:

  ```java
  @JsonIgnoreProperties({"password", "email"})
  public class User {
      private String name;
      private String password;
      private String email;

      // getters and setters
  }
  ```

- In this example, `password` and `email` will not be included when serializing/deserializing.

### 4. **`@JsonInclude`**

This annotation controls the inclusion of properties during serialization based on their value (e.g., ignoring `null` or empty values).

- **Example**:

  ```java
  public class User {
      private String name;

      @JsonInclude(JsonInclude.Include.NON_NULL)
      private String email;

      // getters and setters
  }
  ```

- In this case, the `email` field will only be serialized if it is not `null`.

### 5. **`@JsonFormat`**

This annotation is used to define the format for date and time fields during serialization and deserialization.

- **Example**:

  ```java
  public class Event {
      @JsonFormat(shape = JsonFormat.Shape.STRING, pattern = "yyyy-MM-dd HH:mm:ss")
      private LocalDateTime eventDate;

      // getters and setters
  }
  ```

- **JSON**:

  ```json
  {
    "eventDate": "2022-12-31 14:30:00"
  }
  ```

### 6. **`@JsonCreator`**

This annotation is used to specify a constructor or factory method that Jackson should use for deserialization when working with immutable objects or objects that don’t have a default constructor.

- **Example**:

  ```java
  public class User {
      private String name;
      private int age;

      @JsonCreator
      public User(@JsonProperty("name") String name, @JsonProperty("age") int age) {
          this.name = name;
          this.age = age;
      }

      // getters
  }
  ```

- This tells Jackson to use the annotated constructor to create an object and map the `name` and `age` fields from the JSON.

### 7. **`@JsonValue`**

This annotation is used when you want a class to be serialized/deserialized as a single value (e.g., an enum or wrapper object).

- **Example**:

  ```java
  public enum Status {
      ACTIVE("active"),
      INACTIVE("inactive");

      private String value;

      Status(String value) {
          this.value = value;
      }

      @JsonValue
      public String getValue() {
          return value;
      }
  }
  ```

- **JSON**:

  ```json
  "active"
  ```

### 8. **`@JsonSetter`**

This annotation is used to specify a setter method for a field during deserialization. It allows Jackson to map JSON properties to Java fields even when the setter method has a different name.

- **Example**:

  ```java
  public class User {
      private String name;

      @JsonSetter("full_name")
      public void setName(String name) {
          this.name = name;
      }

      // getter
  }
  ```

- This ensures that the JSON property `full_name` is deserialized into the `name` field.

### 9. **`@JsonAnySetter` and `@JsonAnyGetter`**

These annotations are useful when you want to deserialize/serialize dynamic properties that aren’t predefined in your class.

- **Example**:

  ```java
  public class User {
      private Map<String, Object> additionalProperties = new HashMap<>();

      @JsonAnySetter
      public void setAdditionalProperty(String key, Object value) {
          this.additionalProperties.put(key, value);
      }

      @JsonAnyGetter
      public Map<String, Object> getAdditionalProperties() {
          return additionalProperties;
      }
  }
  ```

- **JSON**:

  ```json
  {
    "name": "Alice",
    "age": 25,
    "address": "123 Main St"
  }
  ```

- Any properties not explicitly mapped (like `address`) will be placed into the `additionalProperties` map.

### 10. **`@JsonDeserialize` and `@JsonSerialize`**

These annotations allow you to customize the deserialization and serialization process by specifying custom deserializer/serializer classes.

- **Example**

  ```java
  public class User {
      @JsonDeserialize(using = CustomDateDeserializer.class)
      private LocalDate dateOfBirth;

      // getters and setters
  }

  public class CustomDateDeserializer extends JsonDeserializer<LocalDate> {
      @Override
      public LocalDate deserialize(JsonParser p, DeserializationContext ctxt) throws IOException {
          return LocalDate.parse(p.getText(), DateTimeFormatter.ofPattern("dd-MM-yyyy"));
      }
  }
  ```

- This allows you to control how specific fields are serialized/deserialized.

### Conclusion

These are some of the most commonly used Jackson annotations. They provide flexibility and control over how JSON is mapped to Java objects, allowing you to tailor the serialization and deserialization process according to your needs.
