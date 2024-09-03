---
title: JPA Many-To-Many
description: Many to Many relationship in JPA
layout: default
nav_order: 7
parent: ORM
grand_parent: Toolbox
permalink: /toolbox/java/jpa/many-to-many/
---

# JPA - Many-To-Many associations explained

In JPA, a many-to-many association represents a relationship where multiple instances of one entity are associated with multiple instances of another entity. This is typically modeled using a join table that contains foreign keys referencing the primary keys of the two entities involved.

## Key Points to Understand

1. **Cardinality**:
   - In a many-to-many relationship, each instance of an entity can be related to multiple instances of another entity, and vice versa. For example, a `Student` entity can be associated with multiple `Course` entities, and each `Course` can have multiple `Student` entities.

2. **Join Table**:
   - A join table is used to establish the many-to-many relationship in the database. This table holds foreign keys to both entities.

3. **Owning Side**:
   - One of the entities is considered the owning side of the relationship. The entity on the owning side typically defines the `@JoinTable` annotation, which specifies the join table and the foreign key columns.

4. **Bidirectional and Unidirectional Relationships**:
   - **Unidirectional**: One entity knows about the relationship, while the other does not. Only one entity will have a reference to the other entity.
   - **Bidirectional**: Both entities know about the relationship. Each entity will have a reference to the other entity, and both will use the `@ManyToMany` annotation.

5. **Cascade Type and Fetch Type**:
   - Cascade operations can be applied to propagate operations from one entity to the related entities.
   - The default fetch type for `@ManyToMany` is `LAZY`, meaning related entities are loaded on demand.

## Example

Let's consider an example where we have two entities: `Student` and `Course`.

### Entity Classes

```java
@Entity
public class Student {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @ManyToMany
    @JoinTable(
        name = "student_course",
        joinColumns = @JoinColumn(name = "student_id"),
        inverseJoinColumns = @JoinColumn(name = "course_id")
    )
    private List<Course> courses = new ArrayList<>();

    // Getters and setters
}

@Entity
public class Course {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String title;

    @ManyToMany(mappedBy = "courses")
    private List<Student> students = new ArrayList<>();

    // Getters and setters
}
```

## Explanation

1. **Student Entity**:
   - The `Student` entity has a `List<Course>` field annotated with `@ManyToMany`, indicating that a student can be enrolled in multiple courses.
   - The `@JoinTable` annotation specifies the name of the join table (`student_course`) and the foreign key columns (`student_id` and `course_id`) that establish the many-to-many relationship.

2. **Course Entity**:

   - The `Course` entity has a `List<Student>` field annotated with `@ManyToMany(mappedBy = "courses")`, indicating that each course can have multiple students enrolled.

   - The `mappedBy` attribute points to the `courses` field in the `Student` entity, making `Student` the owning side of the relationship.

## Database Structure

### **Student Table**

| Column Name | Data Type    | Constraints                  |
|-------------|--------------|------------------------------|
| id          | BIGINT       | PRIMARY KEY, AUTO_INCREMENT  |
| name        | VARCHAR      | NOT NULL                     |

- **`id`**: The primary key for the `Student` table.

- **`name`**: A column to store the name of the student.

### **Course Table**

| Column Name | Data Type    | Constraints                  |
|-------------|--------------|------------------------------|
| id          | BIGINT       | PRIMARY KEY, AUTO_INCREMENT  |
| title       | VARCHAR      | NOT NULL                     |

- **`id`**: The primary key for the `Course` table.

- **`title`**: A column to store the title of the course.

### **Student_Course Table (Join Table)**

| Column Name | Data Type    | Constraints                          |
|-------------|--------------|--------------------------------------|
| student_id  | BIGINT       | FOREIGN KEY REFERENCES Student(id)   |
| course_id   | BIGINT       | FOREIGN KEY REFERENCES Course(id)    |

- **`student_id`**: A foreign key referencing the `id` column in the `Student` table.

- **`course_id`**: A foreign key referencing the `id` column in the `Course` table.

- The combination of `student_id` and `course_id` forms the composite primary key, ensuring that each pair is unique in the join table.

## Example of Table Content

Assume we have the following data in the `Student` and `Course` entities:

- **Students**:

  - { id: 1, name: "Alice" }
  - { id: 2, name: "Bob" }

- **Courses**:

  - { id: 101, title: "Mathematics" }
  - { id: 102, title: "Physics" }

### **Student Table**

| id | name  |
|----|-------|
|  1 | Alice |
|  2 | Bob   |

### **Course Table**

| id  | title       |
|-----|-------------|
| 101 | Mathematics |
| 102 | Physics     |

### **Student_Course Table (Join Table)**

| student_id | course_id |
|------------|-----------|
| 1          | 101       |
| 1          | 102       |
| 2          | 101       |

## How They Work Together

- The `Student_Course` table's `student_id` and `course_id` columns form a composite key that links students and courses together.
- This setup allows multiple students to be associated with multiple courses, enforcing the many-to-many relationship.

## Use Cases

- Many-to-many relationships are common in scenarios like students and courses, authors and books, or products and categories where each entity can relate to multiple instances of the other entity.

This relational structure efficiently manages the many-to-many association, ensuring that the relationship is accurately represented and enforced in the database.
