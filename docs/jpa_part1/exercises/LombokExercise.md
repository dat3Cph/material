---
title: Lombok Exercise
description: lombok exercise
layout: default
nav_order: 1
parent: Exercises
grand_parent: JPA Part 1
permalink: /jpa-part-1/exercises/lombok/
---

# Coding Exercise: Demonstrate Lombok in Java

Lombok is a popular library in Java that helps reduce boilerplate code. One of its most used features is
to generate getter, setter, constructor, and `toString()` methods without having to manually write them.
Let's use that as a basis for our exercise.

## Requirements

1. Setup a new Java project with Maven.
2. Add Lombok as a dependency.
3. Create a simple `Person` class with a few fields.
4. Use Lombok annotations to auto-generate the required methods.

#### Steps

1. **Setup Lombok Dependency**

For Maven, add the following to your `pom.xml`:

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.20</version> <!-- You can check for the latest version on Maven Central -->
    <scope>provided</scope>
</dependency>
```

2. **Create the Person class**

```java
import lombok.Getter;
import lombok.Setter;
import lombok.NoArgsConstructor;
import lombok.ToString;
import lombok.AllArgsConstructor;

@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
@ToString
public class Person {
    private String firstName;
    private String lastName;
    private int age;
}
```

3. **Test the Person class**

Now create a `Main` class to test out the `Person` class:

```java
public class Main {
    public static void main(String[] args) {
        Person person = new Person("John", "Doe", 25);
        System.out.println(person); // This should print something like "Person(firstName=John, lastName=Doe, age=25)"

        person.setAge(26);
        System.out.println(person.getAge()); // This should print "26"
    }
}
```

## Expected Output

```
Person(firstName=John, lastName=Doe, age=25)
26
```

## Reading

Go to the Lombok homepage and read the documentation. <https://projectlombok.org/> or to
our [Toolbox](../../toolbox/java/deepdive/lombok.md) for more information.

## Challenge

For those who want to explore further, try adding more Lombok annotations to the `Person` class like `@EqualsAndHashCode`, and `@Builder` and observe the functionalities they bring.
