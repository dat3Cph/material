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

- [Toolbox](../../toolbox/test/hamcrest.md)
- [Hamcrest Matchers](https://www.baeldung.com/hamcrest)
- [Hamcrest Tutorial](https://www.vogella.com/tutorials/Hamcrest/article.html)
- [Hamcrest Matchers Cheat Sheet](https://dzone.com/articles/hamcrest-matchers-cheat-sheet)
