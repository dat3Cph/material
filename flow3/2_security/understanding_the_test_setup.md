# Understanding the test setup

It is important to understand the fundamental difference between these three tests scenarios:

1. Unit test. A regular unitest in which we test a single method that doesn't involve a database and other external input.
2. An integration test, testing DAO methods that connects to a database.
3. Testing REST endpoints. These tests are also integrationtests, but more comprehensive since they usually also involve connecting
to a database - but also because we need to spin up a webserver to deploy and handle the endpoints. In this case Javalin on a given port number.

Test type 2 + 3 involves a database. To speed things up and simplify the testdesigns we use a Docker testcontainer with Postgres
for the test database. So when running these tests, the Hibernate configuration is modified to connect to a temporary database in a temporary Docker container.

![The test setup](./images/javalin_test_map.png)

### Dependencies
```xml
        <hamcrest.version>2.0.0.0</hamcrest.version>
        <restassured.version>5.3.0</restassured.version>
```

```xml
<!--        https://www.baeldung.com/hamcrest-core-matchers-->
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
```
