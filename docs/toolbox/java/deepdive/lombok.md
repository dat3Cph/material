---
title: Lombok
description: Lombok in Java
layout: default
nav_order: 11
parent: Java
grand_parent: Toolbox
permalink: /toolbox/java/lombok/
---

# Project Lombok for Java

Lombok is a popular Java library that helps reduce boilerplate code by automatically generating common methods like getters, setters, constructors, `equals()`, `hashCode()`, and more, through simple annotations. It enhances developer productivity by simplifying the code and improving readability, allowing developers to focus more on business logic rather than repetitive coding tasks.

## Reference

You can read details about Lombok on the [official Project Lombok website](https://projectlombok.org/).

## Key Features of Lombok

1. **Automatic Generation of Getters and Setters**:
   - **@Getter and @Setter**: These annotations automatically generate getter and setter methods for the fields in a class. You can apply them at the class level to generate methods for all fields, or at the field level for specific fields.

   ```java
   import lombok.Getter;
   import lombok.Setter;

   @Getter
   @Setter
   public class User {
       private String username;
       private String email;
   }
   ```

2. **Constructors**:
   - **@NoArgsConstructor, @AllArgsConstructor, and @RequiredArgsConstructor**: These annotations generate constructors for your classes. `@NoArgsConstructor` generates a no-arguments constructor, `@AllArgsConstructor` generates a constructor with all fields, and `@RequiredArgsConstructor` generates a constructor for fields marked as `final` or annotated with `@NonNull`.

   ```java
   import lombok.AllArgsConstructor;
   import lombok.NoArgsConstructor;
   import lombok.RequiredArgsConstructor;

   @AllArgsConstructor
   @NoArgsConstructor
   @RequiredArgsConstructor
   public class User {
       private String username;
       private final String email;
   }
   ```

3. **Equals, HashCode, and ToString**:
   - **@EqualsAndHashCode**: This annotation generates `equals()` and `hashCode()` methods based on the fields in the class.
   - **@ToString**: Automatically generates a `toString()` method that includes all the fields of the class. You can customize which fields are included and how they are formatted.

   ```java
   import lombok.EqualsAndHashCode;
   import lombok.ToString;

   @EqualsAndHashCode
   @ToString
   public class User {
       private String username;
       private String email;
   }
   ```

4. **Data Classes**:
   - **@Data**: This is a convenient annotation that combines `@Getter`, `@Setter`, `@ToString`, `@EqualsAndHashCode`, and `@RequiredArgsConstructor` into a single annotation, making it ideal for creating simple data carrier classes.

   ```java
   import lombok.Data;

   @Data
   public class User {
       private String username;
       private String email;
   }
   ```

5. **Builder Pattern**:
   - **@Builder**: This annotation provides an easy way to implement the Builder pattern. It generates a builder class that allows you to construct complex objects step-by-step.

   ```java
   import lombok.Builder;

   @Builder
   public class User {
       private String username;
       private String email;
   }

   // Usage
   User user = User.builder()
                   .username("john_doe")
                   .email("john.doe@example.com")
                   .build();
   ```

6. **Val and Var**:
   - **@Val** and **@Var**: These annotations simplify variable declaration by automatically determining the type based on the initializer expression. `val` creates an immutable variable (like `final`), while `var` creates a mutable one.

   ```java
   import lombok.val;
   import lombok.var;

   public class Example {
       public void exampleMethod() {
           val name = "John Doe";  // final String name = "John Doe";
           var age = 30;            // int age = 30;
       }
   }
   ```

7. **Synchronized and Loggers**:
   - **@Synchronized**: A safer and cleaner alternative to Java's `synchronized` keyword.
   - **@Slf4j, @Log, @Log4j2, etc.**: Lombok provides various annotations to automatically generate logger instances, depending on the logging framework you use.

   ```java
   import lombok.Synchronized;
   import lombok.extern.slf4j.Slf4j;

   @Slf4j
   public class Example {
       @Synchronized
       public void safeMethod() {
           log.info("This method is thread-safe.");
       }
   }
   ```

## Benefits of Using Lombok

- **Reduced Boilerplate Code**: Lombok significantly reduces the amount of boilerplate code, such as getters, setters, constructors, and `toString()` methods, making your code cleaner and more readable.
- **Enhanced Productivity**: By automating repetitive tasks, Lombok allows developers to focus on the core logic and functionality of their applications.
- **Improved Readability**: With fewer lines of code, Lombok makes classes more concise and easier to understand.
- **Flexible and Customizable**: Lombok provides options to customize the generated code, allowing developers to tailor it to their specific needs.

## Considerations

- **IDE Support**: While Lombok is well-supported by most modern IDEs (like IntelliJ IDEA and Eclipse), it requires specific plugins to provide full support for its annotations. Without these plugins, IDEs might not recognize the generated methods and constructors, leading to false errors.
- **Compile-Time Dependency**: Lombok works during the compile phase, meaning that the generated code is not visible in the source files. This can make debugging or code analysis more challenging if developers are unfamiliar with Lombok.
- **Dependency**: Relying on Lombok introduces an additional dependency to your project, which might be a consideration in environments where minimal dependencies are preferred.

## Summary

Lombok is a powerful Java library designed to reduce boilerplate code by using simple annotations to automatically generate common methods and patterns. It improves productivity and code readability while ensuring that your classes remain concise. While it offers many benefits, developers should be mindful of IDE support, debugging considerations, and the added dependency when using Lombok in their projects.
