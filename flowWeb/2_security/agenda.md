# Agenda Monday Rest assured
1. SOLID: Open/Closed Principle - ApplicationConfig from last week
2. Rest Assured
  - Setup POM dependencies: 
```xml
<dependency>
            <groupId>org.hamcrest</groupId>
            <artifactId>java-hamcrest</artifactId>
            <version>${hamcrest.version}</version>
            <scope>test</scope>
        </dependency>
        <!--        https://www.baeldung.com/rest-assured-tutorial-->
        <dependency>
            <groupId>io.rest-assured</groupId>
            <artifactId>rest-assured</artifactId>
            <version>${restassured.version}</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>io.rest-assured</groupId>
            <artifactId>json-schema-validator</artifactId>
            <version>${restassured.version}</version>
            <scope>test</scope>
        </dependency>
                <!-- Test dependencies -->
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>5.7.0</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-params</artifactId>
            <version>5.7.0</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-engine</artifactId>
            <version>5.7.0</version>
            <scope>test</scope>
        </dependency>

```
  - Write basic API tests to verify endpoints' CRUD functionality and response status codes.
  - Demonstrate how to use a variety of Hamcrest matchers to write expressive
  assertions in Rest Assured tests.
  - Given, When, Then - BDD (Behavior Driven Development) style of writing tests (Gherkin language)


# Agenda Wednesday JWT
1. Explain the concept of JWT (JSON Web Tokens) and its role in securing RESTful web services.
2. Show the JavalinDemo Security server in action
  - Register a user
  - Login a user and get a token
  - Access a protected endpoint with the token
3. Show how the users password is hashed and salted in db.
4. Show how to implement JWT-based authentication and authorization in a Javalin application.
5. Demonstrate how to secure REST endpoints using JWTs to control access to resources.
7. Show how to salt and hash passwords with bcrypt.
