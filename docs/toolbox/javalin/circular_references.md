---
title: Circular References in JPA
description: How to avoid circular references in JPA Many-to-Many relationships and JSON serialization
layout: default
nav_order: 2
grand_parent: Toolbox
parent: Javalin
has_children: false
permalink: /toolbox/javalin/circular-refs/
---

# How to avoid circular references in JPA Many-to-Many relationships and JSON serialization

When working with JPA entities that have `@ManyToMany` relationships, you may encounter issues with circular references during serialization. This can lead to infinite loops and stack overflow errors when serializing entities to JSON.

In JPA, when using Lombok in your entities and DTOs, managing `@ManyToMany` relationships can lead to infinite loops if one side tries to serialize the other side repeatedly during JSON conversion (e.g., with frameworks like Jackson).

To solve this, there are several approaches you can use to avoid infinite loops, including the following:

### 1. Use `@JsonManagedReference` and `@JsonBackReference` (Jackson)

To handle serialization and prevent the infinite recursion, you can use `@JsonManagedReference` and `@JsonBackReference` annotations from the `com.fasterxml.jackson.annotation` package.

Here's how you can apply them:

```java
@Entity
public class Course {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToMany(mappedBy = "courses")
    @JsonBackReference // Prevent infinite recursion during serialization
    private Set<Student> students = new HashSet<>();

    // Getters and setters
}

@Entity
public class Student {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToMany
    @JoinTable(
        name = "student_courses",
        joinColumns = @JoinColumn(name = "student_id"),
        inverseJoinColumns = @JoinColumn(name = "course_id")
    )
    @JsonManagedReference
    private Set<Course> courses = new HashSet<>();

    // Getters and setters
}
```

- `@JsonManagedReference` is used on the "owner" side of the relationship.
- `@JsonBackReference` is used on the "inverse" side.
- This annotation pair will instruct Jackson to serialize the `@JsonManagedReference` but ignore the `@JsonBackReference`, thus preventing an infinite loop.

### 2. Use `@JsonIgnore` (Simple but Limited)

Another simple approach is to use the `@JsonIgnore` annotation on one side of the relationship. This means that one side of the relationship will not be serialized at all:

```java
@Entity
public class Course {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToMany(mappedBy = "courses")
    @JsonIgnore // Prevents infinite loop
    private Set<Student> students = new HashSet<>();

    // Getters and setters
}

@Entity
public class Student {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToMany
    @JoinTable(
        name = "student_courses",
        joinColumns = @JoinColumn(name = "student_id"),
        inverseJoinColumns = @JoinColumn(name = "course_id")
    )
    private Set<Course> courses = new HashSet<>();

    // Getters and setters
}
```

- This prevents infinite recursion but means that any JSON serialization of `Course` will not include the related `students`.

### 3. Use `@JsonIdentityInfo` (Avoid Cyclic Dependency by Object IDs)

Using `@JsonIdentityInfo` annotation can also solve the problem by using an identity-based approach for serialization, so the same instance is not serialized multiple times.

```java
import com.fasterxml.jackson.annotation.JsonIdentityInfo;
import com.fasterxml.jackson.annotation.ObjectIdGenerators;

@Entity
@JsonIdentityInfo(generator = ObjectIdGenerators.PropertyGenerator.class, property = "id")
public class Course {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToMany(mappedBy = "courses")
    private Set<Student> students = new HashSet<>();

    // Getters and setters
}

@Entity
@JsonIdentityInfo(generator = ObjectIdGenerators.PropertyGenerator.class, property = "id")
public class Student {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToMany
    @JoinTable(
        name = "student_courses",
        joinColumns = @JoinColumn(name = "student_id"),
        inverseJoinColumns = @JoinColumn(name = "course_id")
    )
    private Set<Course> courses = new HashSet<>();

    // Getters and setters
}
```

- `@JsonIdentityInfo` instructs Jackson to use object identifiers instead of directly serializing nested objects. This can prevent recursion issues when dealing with bi-directional relationships.

### 4. Use DTOs for Serialization

Another effective way to avoid serialization issues is to use Data Transfer Objects (DTOs) rather than serializing the entity classes directly.

- You can create DTOs that represent only the necessary information, thus avoiding the `@ManyToMany` relationship altogether.
- Convert entities to DTOs using utility classes like `ModelMapper`, or manually in your service layer.

### Choosing Between the Options

- **`@JsonManagedReference` / `@JsonBackReference`**: Use when you have a clear owner/inverse relationship, and you want to serialize data from the owner side.
- **`@JsonIgnore`**: Simple and lightweight but may hide too much information.
- **`@JsonIdentityInfo`**: Good if you want to serialize both sides of the relationship and avoid cycles with identifiers.
- **DTOs**: A clean and flexible approach that decouples your database entities from serialization concerns.

A typical recommendation for REST APIs is to use DTOs. This allows you to control what data is exposed and helps avoid complex issues related to lazy-loading and bidirectional relationships.
