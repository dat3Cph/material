---
title: Student
description: student exercise
layout: default
nav_order: 1
parent: Exercises
grand_parent: JPA Part 1
permalink: /jpa-part-1/exercises/student/
---

# Student Exercise

**Exercise 1: Mapping Entities and Annotations**
Objective: Apply JPA annotations to map Java classes to database tables and understand entity lifecycle.

1. Create a new Java project using Maven.
2. Define a simple entity class called "Student" with attributes like `id`, `firstName`, `lastName`, `email` and `age`. Remember to include a no-arg constructor.
3. Use JPA annotations to map the entity class to a database table named `students`. The `email` property should be unique.
4. Include appropriate annotations such as `@Entity`, `@Table`, `@Id`, `@GeneratedValue`, and `@Column` to define the primary key and attributes mapping.
5. Add a Main class with a main method and one static property: `EntityManagerFactory`.
6. Create the following methods and add it to the Main class:
    - `public static void createStudent(Student student)` - This method should create a new student and persist it to the database.
    - `public static Student readStudent(int id)` - This method should read a student from the database using the student's id.
    - `public static Student updateStudent(Student updStd)` - This method should update an existing student in the database.
    - `public static void deleteStudent(int id)` - This method should delete a student from the database using the student's id.
    - `public static List<Student> readAllStudents()` - This method should retrieve all students from the database and return them as a list. Use a `TypedQuery` to retrieve all students.
    - In all the methods above, remember to open and close the `EntityManager` and `EntityManagerFactory` objects.
    - You can use either the `try-with-resources` or the `finally` block to close the objects.
7. In all the methods above, write small comments that explains when an object is transient, detached, removed or managed. (See example below)

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

8. Create a method in the Student class that verifies that the email address is valid. The method should return a boolean value.
9. Add a `@PrePersist` method to the Student class that verifies that the email address is valid. If the email address is not valid, throw an exception.
10. Do the same as in step 9, but this time use a `@PreUpdate` method.
11. Create a test class with a test method for each of the methods in the Main class.
12. Run the test class and verify that all tests pass.
13. Create 10 students and persist them to the database.
    - 3 of the students should have the last name "Hansen" and 4 should have the last name "Jensen".
    - 1 of the students should be the oldest with an age of 90.
    - 1 of the students should be the youngest with an age of 10.
14. Get the `average` age of all students in the database.
15. Get the `average` age of all students in the database whose last name is "Hansen".
16. `count` the number of students in the database whose last name is "Jensen".
17. Get the first name of the oldest student in the database.
18. Get the youngest student in the database.
19. Get the `sum` of all ages of all students in the database.

**Exercise 2: Q & A**

1. Why do we need a no-arg constructor in an entity class?
2. Investigate where we in our code can change the following:
    - specify the database dialect?
    - specify the JDBC connection properties?
    - add annotated classes?
3. What is the purpose of the `@GeneratedValue` annotation and what are the different strategies that can be used to generate primary key values for entities?
4. In Java, we have something called `try with resources`. What does it do and how can we use it in our code?
5. What is the difference between `persist()` and `merge()` methods in JPA?
6. What is the difference between the `TypedQuery` and `Query` interfaces in JPA?
7. What is the difference between the `getSingleResult()` and `getResultList()` methods in JPA?
8. What are the different states of an entity in JPA?
