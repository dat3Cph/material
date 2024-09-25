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

Here's a basic Javalin application that demonstrates how to use logging with SLF4J.

```java
package dat;

import io.javalin.Javalin;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

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
    }
}
```

### Explanation of the Code

1. **Logger Creation**: A logger instance is created using `LoggerFactory.getLogger(ClassName.class)`.
2. **Logging Levels**:
   - `logger.info(...)` logs informational messages.
   - `logger.error(...)` logs error messages.
   - You can use other levels like `debug`, `warn`, etc., depending on the context.
3. **Logback Configuration**: The `logback.xml` file defines how and where the logs will be output, such as the console with a custom format.
4. **Exception Handling**: The application logs exceptions using the `app.exception` method, demonstrating how to capture and log errors effectively.

### Running the Application

To run the application, execute the `main` method in `Main.java`. Access `http://localhost:7070` in your browser to see the logs in action. Try also the `/error` endpoint to see how exceptions are handled and logged.

This setup should provide you with a solid foundation for integrating logging into your Javalin application using SLF4J and Logback.
