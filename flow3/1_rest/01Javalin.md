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

## Javalin and Routes
- Handlers
- Controllers
- EndpointGroup
- app.routes
- app.path()
- ApplicationConfig
[Example Code](https://github.com/HartmannDemoCode/javalindemo/blob/main/src/main/java/dk/cphbusiness/rest/P02RoutesDemo.java)

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

## Filters
- **Filters**
  - app.exception()
  ````Java
  app.exception(Exception.class, (e, ctx) -> {
    ctx.status(500);
    ctx.result("Something went wrong");
  });
  ````
  - app.error()
  ````java 
  app.error(404, ctx -> {
    ctx.result("Custom 404 page");
  });
  ````
  - app.before()
  ````java 
    app.before(ctx -> {
        //what to do
        
    });
    ````
  `
  - app.after()
  - app.routes()
  - app.start()
  - app.stop()
  - app.events()
  - app.attribute()