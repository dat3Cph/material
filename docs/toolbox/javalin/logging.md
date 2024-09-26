---
title: Logging
description: Logging in Javalin with SLF4J and Logback
layout: default
nav_order: 1
grand_parent: Toolbox
parent: Javalin
has_children: false
permalink: /toolbox/javalin/logging/
---

# Logging in Javalin with SLF4J and Logback

Here's a small tutorial on how to set up logging in a Javalin-based Java program using Java 17, SLF4J, and Logback. This guide will walk you through creating a basic Javalin application and configuring logging with SLF4J and Logback.

### Step 1: Setting Up Your Project

Ensure you have Maven installed and create a new Maven project called `loggingdemo` with the following `pom.xml` to set up dependencies for Javalin, SLF4J, and Logback:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>dat</groupId>
    <artifactId>loggingdemo</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>


    <dependencies>
        <!-- Javalin Web Framework -->
        <dependency>
            <groupId>io.javalin</groupId>
            <artifactId>javalin</artifactId>
            <version>6.3.0</version>
        </dependency>

        <!-- SLF4J API -->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>2.0.16</version>
        </dependency>

        <!-- Logback Classic (SLF4J implementation) -->
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>1.5.7</version>
        </dependency>
    </dependencies>
</project>
```

### Step 2: Create the Logback Configuration File

Create a `logback.xml` file in the `src/main/resources` directory to configure Logback. Here is a simple configuration:

```xml
<configuration>

    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <appender name="FILE" class="ch.qos.logback.core.FileAppender">
        <file>logs/javalin-app.log</file>
        <append>true</append>
        <encoder>
            <pattern>%d{yyyy-MM-dd HH:mm:ss} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>

    <root level="info">
        <appender-ref ref="CONSOLE" />
        <appender-ref ref="FILE" />
    </root>

    <!-- Adjust log levels for specific packages if needed -->
    <logger name="app" level="debug" />
</configuration>

```

### Step 3: Create a Basic Javalin Application

Here's a basic Javalin application that demonstrates how to use logging with SLF4J and a little errorhandling with Javalin.

```java
package dat;

import io.javalin.Javalin;
import io.javalin.http.HttpStatus;
import io.javalin.http.InternalServerErrorResponse;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.Map;

public class Main {
    // Create a logger instance for this class
    private static final Logger logger = LoggerFactory.getLogger(Main.class);
    private static final Logger debugLogger = LoggerFactory.getLogger("app");

    public static void main(String[] args) {
        // Initialize Javalin
        Javalin app = Javalin.create(config -> {
            config.showJavalinBanner = false; // Disable default Javalin banner
        }).start(7070);

        // Set up routes
        app.get("/", ctx -> {
            logger.info("Handling request to /");
            ctx.result("Hello, Javalin with Logging!");
        });

        app.get("/error", ctx -> {
            logger.error("An error endpoint was accessed");
            throw new RuntimeException("This is an intentional error for logging demonstration.");
        });

        // Log the server start
        logger.info("Javalin application started on http://localhost:7070");
        debugLogger.debug("Debug log message from Main class during startup");

        // Exception handling example
        app.exception(Exception.class, (e, ctx) -> {
            logger.error("An exception occurred: {}", e.getMessage(), e);
            ctx.status(500).result("Internal Server Error");
        });

        app.error(HttpStatus.INTERNAL_SERVER_ERROR, ctx -> {
            logger.error("Bummer: {}", ctx.status());
            Map<String, String> msg = Map.of("error", "Internal Server Error, dude!", "status", String.valueOf(ctx.status()));
            throw new InternalServerErrorResponse("Off limits!", msg);
        });
    }
}
```

### Explanation of the Code

The provided code sets up a simple Javalin application with robust logging, exception, and error handling. Here's a detailed explanation of each section, with a focus on how logging, exceptions, and error handling are managed:

### Code Explanation

1. **Logger Initialization**:

   ```java
   private static final Logger logger = LoggerFactory.getLogger(Main.class);
   private static final Logger debugLogger = LoggerFactory.getLogger("app");
   ```

   - Two loggers are created:
     - `logger`: Logs messages specific to the `Main` class using its fully qualified name.
     - `debugLogger`: A separate logger named `"app"`, configured for more detailed debug-level logging if needed.

2. **Javalin Initialization**:

   ```java
   Javalin app = Javalin.create(config -> {
       config.showJavalinBanner = false; // Disable default Javalin banner
   }).start(7070);
   ```

   - A Javalin instance is created and configured to hide the default startup banner, making the console output cleaner. The server starts on port `7070`.

3. **Route Definitions**:
   - **Root Route (`/`)**:

     ```java
     app.get("/", ctx -> {
         logger.info("Handling request to /");
         ctx.result("Hello, Javalin with Logging!");
     });
     ```

     - Logs an informational message whenever a request is made to the root (`/`) endpoint.
     - Returns a simple response to the client.

   - **Error Route (`/error`)**:

     ```java
     app.get("/error", ctx -> {
         logger.error("An error endpoint was accessed");
         throw new RuntimeException("This is an intentional error for logging demonstration.");
     });
     ```

     - Logs an error message when the `/error` endpoint is accessed.
     - Intentionally throws a `RuntimeException` to demonstrate error handling and logging.

4. **Logging During Startup**:

   ```java
   logger.info("Javalin application started on http://localhost:7070");
   debugLogger.debug("Debug log message from Main class during startup");
   ```

   - Logs an informational message when the application starts.
   - Logs a debug message using `debugLogger`, demonstrating how to use a different logger for more detailed logs during startup.

5. **Exception Handling**:

   ```java
   app.exception(Exception.class, (e, ctx) -> {
       logger.error("An exception occurred: {}", e.getMessage(), e);
       ctx.status(500).result("Internal Server Error");
   });
   ```

   - Global exception handling is set up for all exceptions.
   - Logs the exception message and stack trace using the `logger`.
   - Responds with a 500 status code and a generic error message to the client.

6. **Custom Error Handling for 500 Internal Server Error**:

   ```java
   app.error(HttpStatus.INTERNAL_SERVER_ERROR, ctx -> {
       logger.error("Bummer: {}", ctx.status());
       Map<String, String> msg = Map.of("error", "Internal Server Error, dude!", "status", String.valueOf(ctx.status()));
       throw new InternalServerErrorResponse("Off limits!", msg);
   });
   ```

   - Handles specific HTTP 500 errors.
   - Logs the error status when such an error occurs.
   - Throws a custom `InternalServerErrorResponse` with a message and a map of error details, demonstrating more granular control over error responses.

### Highlighted Aspects of Logging, Exception, and Error Handling

- **Logging**:
  - The code uses SLF4J with Logback (assumed configuration) to log messages at various levels (`INFO`, `ERROR`, `DEBUG`).
  - Logging is strategically placed to capture key application events, such as startup, request handling, errors, and exceptions.

- **Exception Handling**:
  - The `app.exception()` method sets up a global exception handler, capturing all exceptions and logging them.
  - This prevents unhandled exceptions from crashing the application and provides a consistent error response.

- **Error Handling**:
  - The `app.error()` method targets specific HTTP error codes, in this case, `500 Internal Server Error`, allowing for custom error messages and responses.
  - Uses structured error responses to inform the client about what went wrong, aiding in debugging and enhancing the client experience.

### Summary

This approach ensures that the Javalin application remains robust, with detailed logs capturing the application’s behavior and errors. This setup is critical for monitoring the application's health, diagnosing issues in production, and understanding the root cause of failures. The use of global exception and error handlers ensures that errors are gracefully managed and logged.

### Running the Application

To run the application, execute the `main` method in `Main.java`. Access `http://localhost:7070` in your browser to see the logs in action. Try also the `/error` endpoint to see how exceptions are handled and logged.

This setup should provide you with a solid foundation for integrating logging into your Javalin application using SLF4J and Logback.
