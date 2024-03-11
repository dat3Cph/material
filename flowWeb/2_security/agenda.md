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
  - 
3. 