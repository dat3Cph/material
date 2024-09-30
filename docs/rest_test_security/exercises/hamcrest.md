---
title: Hamcrest Mathcers
description: Learning how to use Hamcrest Matchers for assertions
layout: default
nav_order: 2
grand_parent: Rest API Test and Security
parent: Exercises
permalink: /rest-test-security/exercises/hamcrest/
---

# Hamcrest Matchers Exercises

This small exercise is meant to help students get familiar with Hamcrest matchers. The exercise will involve creating a simple class and writing unit tests with Hamcrest to check the properties of that class.

## Task: Student Class and Hamcrest Matchers

### Step 1: Create a `Student` class

Create a maven project from scratch and add a the dependencies at the [bottom of this page](#dependencies) to the pom.xml file.

The `Student` class will have the following properties:

- `String name`
- `int age`
- `double gpa` // Grade Point Average, a number between 0.0 and 4.0
- `List<Student> friends`

It should have:

- A constructor to initialize these fields.
- Getters for each field.
- A method `addFriend(Student friend)` to add a `Student` object to the `friends` list.

```java

import java.util.ArrayList;
import java.util.List;

public class Student {
    private String name;
    private int age;
    private double gpa;
    private List<Student> friends;

    public Student(String name, int age, double gpa) {
        this.name = name;
        this.age = age;
        this.gpa = gpa;
        this.friends = new ArrayList<>();
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public double getGpa() {
        return gpa;
    }

    public List<Student> getFriends() {
        return friends;
    }

    public void addFriend(Student friend) {
        this.friends.add(friend);
    }
}

```

### Step 2: Write Unit Tests with Hamcrest

Students should write tests using the following Hamcrest matchers:

- `is` // like "name is John", "age is 24"
- `equalTo`  // like age equalTo 24
- `greaterThan` // like gpa greaterThan 3.0
- `lessThanOrEqualTo`  // like age lessThanOrEqualTo 25
- `containsString`  // like name containsString 'John'
- `hasSize`  // like friends hasSize 3
- `hasItem`  // like friends hasItem 'Alice' as an object
- `not` // like name not 'John'
- `containsInAnyOrder` // like friends containsInAnyOrder 'Alice', 'Bob', 'Charlie'

## Read more

- [Toolbox overview](../../toolbox/test/hamcrest.md)
- [Hamcrest Matchers](https://www.baeldung.com/java-junit-hamcrest-guide)
- [Hamcrest Tutorial](https://www.vogella.com/tutorials/Hamcrest/article.html)

## Dependencies

To carry out the Hamcrest exercise with JUnit, you will need dependencies for both **JUnit** and **Hamcrest** in your `pom.xml` file if you are using Maven. Below are the necessary dependencies:

### 1. **JUnit** Dependency

Since you're using Java 17, it's best to use **JUnit 5** (Jupiter). JUnit 5 has its own set of dependencies for writing and running tests.

```xml
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-api</artifactId>
    <version>5.9.3</version> <!-- Use the latest version available -->
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-engine</artifactId>
    <version>5.9.3</version>
    <scope>test</scope>
</dependency>
```

### 2. **Hamcrest** Dependency

JUnit 5 doesn't bundle Hamcrest by default, so you need to include Hamcrest explicitly. Here's the Maven dependency for **Hamcrest**:

```xml
<dependency>
    <groupId>org.hamcrest</groupId>
    <artifactId>hamcrest</artifactId>
    <version>2.2</version> <!-- Use the latest version available -->
    <scope>test</scope>
</dependency>
```

### How to Run Tests

Make sure that your Maven `pom.xml` file has the `maven-surefire-plugin` configured to run JUnit 5 tests:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>3.0.0-M7</version> <!-- Make sure to use a version that supports JUnit 5 -->
        </plugin>
    </plugins>
</build>
```

### Summary

- **JUnit 5** for the testing framework.
- **Hamcrest** for matchers.
- **Maven Surefire Plugin** to ensure test cases are executed.
