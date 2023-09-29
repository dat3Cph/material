# Javalin Demonstration
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
[Example Code](https://github.com/HartmannDemoCode/javalindemo/blob/main/src/main/java/dk/cphbusiness/rest/SimpleDemo.java)
6. Run the `App.java` class.

## Javalin and Routes
[Example Code]()


