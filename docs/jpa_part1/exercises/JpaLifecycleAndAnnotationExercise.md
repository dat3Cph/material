---
title: JPA Lifecycle Annotations Exercise
description: jpa lifecycle and annotations exercise
layout: default
nav_order: 1
parent: Exercises
grand_parent: JPA Part 1
permalink: /jpa-part-1/exercises/jpalifecycleannotations/
---

# JPA Lifecycle and Annotations

### Objective

**Apply JPA annotations to map Java classes to database tables and understand the entity lifecycle.**

***

![JPA Entity Flow](../../images/jpaentityflow.png)

***

### Instructions

1. [ ] Create a new Java project using Maven.
2. [ ] Define a simple entity class called "Student" with attributes like `id`, `firstName`, `lastName`, `email` and `age`. Remember to include a no-arg constructor.
3. [ ] Use JPA annotations to map the entity class to a database table named `students`.
4. [ ] Add a constraint to the `email` attribute to ensure that the email address is unique.
5. [ ] Include appropriate annotations such as `@Entity`, `@Table`, `@Id`, `@GeneratedValue`, and `@Column` to define the primary key and attributes mapping.
6. [ ] Add a `Main.class` including a main method
7. [ ] Create the following methods in the Main class:
   - `public static void createStudent(Student student)` - This method should create a new student and persist it to the database.
   - `public static Student readStudent(int id)` - This method should read a student from the database using the student's id.
   - `public static Student updateStudent(Student updStd)` - This method should update an existing student in the database.
   - `public static void deleteStudent(int id)` - This method should delete a student from the database using the student's id.
   - `public static List<Student> readAllStudents()` - This method should retrieve all students from the database and return them as a list. Use a `TypedQuery` to retrieve all students.

_In all the methods above, remember to open and close the `EntityManager` and `EntityManagerFactory` objects._
_You can use either the `try-with-resources` or the `finally` block to close the objects._

***

1. [ ] In all the methods above, write small comments that explains when an object is transient, detached, removed or managed. (See example below)

```JAVA
    public static void main(String[] args) {
    // entity is in transient state
    Student student = new Student("Michelle", "Schmidt", "schmidt@mail.com", 30);

    }
    
    public static void createStudent(Student student) {
        try(EntityManager em = emf.createEntityManager()) {
            em.getTransaction().begin();
            // entity is in managed state (after persist)
            em.persist(student);
            // entity is in detached state after the transaction is committed
            em.getTransaction().commit();
        }
    }
```

1. [ ] Add a `@PrePersist` method to the Student class that verifies that the email address is valid. If the email address is not valid, throw an exception.
2. [ ] Use the same logic as above but this time in the `@PreUpdate` method.
