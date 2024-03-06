# Agenda
## Topics
- **Part 1: 60 min.**
- Catch up from last: 
  - `Arrays.asList` gets us a non-resizable list (wrap in `new ArrayList` to make it resizable)
  - Recap `Routes` and `Handlers` and `Controllers` and `DAOs` (See the PersonEntityController)
- CRUD (Focus on UPDATE and DELETE)
- Path parameters
- Query parameters
- Receive and set headers
- Exercise 20 min.
- **Break 15 min.**
- **Part 2: 60 min.**
  - Application Config setup with
    - Confic for
      - `config.staticFiles.add("/public");`  enables serving of static files from the public folder in the classpath. PROs: easy to use, CONs: you have to restart the server every time you change a file
            `config.http.defaultContentType = "application/json";` default content type for requests
            `config.routing.contextPath = "/";` base path for all routes
    - Singleton pattern
    - Dependency Injection for
      - routes
      - filters (before and after)
      - start/stop server
      - CORS (later)
      - Error handling (later today)
- Exercise 20 min.
- **Break 15 min**.
- **Part 3: 60 min.**
- Get and Set http headers
- Error handling
- Exercise 20 min.


### Class Exercise 1 headers:
- Create a new class called `ContextDemo.java` in the `src/main/java` folder.
- Create a new javalin application with the following routes:
  - GET /hello/{name} // Returns a greeting to the name provided in the path parameter
  - GET /headers // Returns a list of all headers in the request
  - GET /queryParam // Returns the value of the query parameter "name"
  - For the following 2 routes, check in browsers developer tools what the response header and status code is:
    - GET /responseHeaders // Returns a response with a custom header: X-My-Header with the value "Hello World"
    - GET /responseStatus // Returns a response with the status code 418

### Class Exercise 2 Application Config:
- In the Application Config create a new method that can add a filter (Use the .before method)
  - The filter should add a header to the response with the key "X-My-Header" and the value "Hello World"
  - It should also log the request method: path, request headers and time to the console

### Class Exercise 3 Error handling:
- Create a new class called `ErrorHandlingDemo.java` in the `src/main/java` folder.
- Add exception event handlers for 404 and 500 status codes on the Javalin app
  - Return a custom message for each status code
- Create a new javalin application with the following routes:
  - GET /error // Returns a response with the status code 500
    - Create a custom 
  - GET /notFound // Returns a response with the status code 404
- If you have time:
  - Create an EntityNotFoundException class that extends RuntimeException
     - Add a constructor that takes a message
     - Add a constructor that takes a message and a cause
  - Create a custom APIException class that extends RuntimeException
    - Add a constructor that takes a status code and a message
    - Add a constructor that takes a status code, a message and a cause

  