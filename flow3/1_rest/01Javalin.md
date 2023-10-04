# Javalin Demonstration
**HUSK**: Køb DOMÆNE og set up til Digital Ocean.
- [Source](https://javalin.io/documentation)
- 

## Basic setup
1. In IntelliJ, create a new Maven project.
2. Select Java 17 and Maven.
3. Add Javalin dependency to pom.xml:
```XML
<dependency>
    <groupId>io.javalin</groupId>
    <artifactId>javalin</artifactId>
    <version>4.3.0</version>
</dependency>
```
4. Create a new Java class called `App.java` in the `src/main/java` folder.
5. Add the following code to the `App.java` class:

```Java
import io.javalin.Javalin;

public class App {
    public static void main(String[] args) {
        Javalin app = Javalin.create().start(7007);
        app.get("/", ctx -> ctx.result("Hello World"));
    }
}
```

[Example Code](https://github.com/HartmannDemoCode/javalindemo/blob/main/src/main/java/dk/cphbusiness/rest/P01SimpleDemo.java)

6. Run the `App.java` class.

### Class Exercise 1: Create a simple Javalin application with 2 endpoints:
- GET /todaysDate // Returns the current date
- GET /joke // Returns a random joke

## Javalin and Routes

- Handlers
  - Handlers are the functions that are executed when a request is made to a specific endpoint. 
- Controllers
  - Controllers are classes that can provide multiple handlers (usually based on a specific ressource).
- EndpointGroup
  - EndpointGroup is an interface that can be implemented to provide multiple routes
- app.routes
  - app.routes() is a method that can be used to group Endpoints together.
- app.path()
  - app.path() is a method that can be used to group routes together.
- ApplicationConfig
[Example Code](https://github.com/HartmannDemoCode/javalindemo/blob/main/src/main/java/dk/cphbusiness/rest/P02RoutesDemo.java)

### Class Exercise 2: 

- Create a new class called `RoutesDemo.java` in the `src/main/java` folder.
- Create a ProductDTO with the following fields:
  - id
  - name
  - price
  - category
- Create a new javalin application with the following routes:
  - GET /allProducts // Returns all products from an in-memory collection of products (You decide the data structure) 
  - GET /product/{id} // Returns a specific product based on the id
  - And one that gets all products from a specific category
- Setup the server so that all product endpoints are under the path `/api/products`

## Context object
- What is the context object?
- **Methods**
  - **Request methods:**
    - pathParam()
    - header()
    - queryParam()
    - req()
    - POST examples
        - bodyAsClass()
        - bodyValidator()
  - **Response methods:**
    - setContentType()
    - setHeader()
    - setStatus()
    - json()
    - html()
    - render()

### Class Exercise 3:
- Create a new class called `ContextDemo.java` in the `src/main/java` folder.
- Create a new javalin application with the following routes:
  - GET /hello/{name} // Returns a greeting to the name provided in the path parameter
  - GET /headers // Returns a list of all headers in the request
  - GET /queryParam // Returns the value of the query parameter "name"
  - For the following 2 routes, check in browsers developer tools what the response header and status code is:
    - GET /responseHeaders // Returns a response with a custom header: X-My-Header with the value "Hello World"
    - GET /responseStatus // Returns a response with the status code 418

## Errorhandling
In Javalin, `app.error()` and `app.exception()` are used to handle errors and exceptions that occur during the execution of your web application, but they are suited for different use cases:

1. **`app.error()`**:
   - Use Case: Handling Expected Errors
   - Description: The `app.error()` method is used to handle expected or known errors, such as client errors (e.g., 400 Bad Request, 404 Not Found) or application-specific errors.
   - You specify an HTTP status code and a handler function that will be invoked when an error with that status code occurs. This allows you to define custom error responses for specific HTTP error codes.
   - Example Use Cases: Customizing error messages for specific status codes, handling validation errors, or returning custom error pages.

   Example:
   ```java
   app.error(404, ctx -> {
       ctx.result("Page not found");
   });

   app.error(500, ctx -> {
       ctx.result("Internal Server Error");
   });
   ```

2. **`app.exception()`**:
   - Use Case: Handling Unexpected Exceptions
   - Description: The `app.exception()` method is used to handle unexpected exceptions that can occur during the execution of your application, such as unhandled runtime exceptions or errors in your code.
   - How It Works: You specify a Java exception class and a handler function that will be invoked when an instance of that exception is thrown. This allows you to gracefully handle exceptions and provide custom error responses.
   - Example Use Cases: Logging unhandled exceptions, returning user-friendly error messages for unexpected errors, or performing cleanup actions.

   Example:
   ```java
   app.exception(MyCustomException.class, (e, ctx) -> {
       ctx.status(500);
       ctx.result("An unexpected error occurred: " + e.getMessage());
   });

   app.exception(Exception.class, (e, ctx) -> {
       ctx.status(500);
       ctx.result("An internal server error occurred");
   });
   ```

In summary, `app.error()` is specifically for handling HTTP errors and allows you to customize responses for known error scenarios, while `app.exception()` is for handling unexpected exceptions that might occur anywhere in your application. You can use both of them together to provide comprehensive error handling for your Javalin application.

## Filters
- Filters are used to intercept requests and responses before and after they are handled by your application.
- Filters are executed in the order they are defined.

- app.before()
- Use cases:
    - **Authentication**
  ```java 
    app.before(ctx -> {
    // Check if the user is authenticated
        if (!isUserAuthenticated(ctx)) {
            ctx.status(401); // Unauthorized
            ctx.result("You must be logged in to access this resource.");
        }
    });
  ```
  - **Logging**
  - **Rate limiting**
  - **CORS**
  - **Set Response Headers**
- app.after()
  - **Logging response time, data etc.**
  - **Set Response Headers**
  ````java
  app.after(ctx -> {
          int responseStatus = ctx.status();
          String responseBody = ctx.resultString();
          
          System.out.println(String.format("Response Status: %d", responseStatus));
          System.out.println(String.format("Response Body: %s", responseBody));
  });```

### Class Exercise 4:
- Create a new class called `FiltersDemo.java` in the `src/main/java` folder.
- Create a new javalin application with a before filter, that can provide rate limiting for the following 3 routes:
  - GET /hello/{name} // Returns a greeting to the name provided in the path parameter
  - GET /headers // Returns a list of all headers in the request
  - GET /queryParam // Returns the value of the query parameter "name"  
- Create a new javalin application with an after filter, that can log both the request url and the response status and body for all routes.
  - Make sure to log everything as json to a file.
  - Include a timestamp in the log.