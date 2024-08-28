---
title: Point
description: point exercise
layout: default
nav_order: 1
parent: Exercises
grand_parent: JPA Part 1
permalink: /jpa-part-1/exercises/points/
---

# The Point exercise

## Introduction

Welcome to "The Point" exercise! This exercise will introduce you to the basics of JPA and Hibernate,
and you will learn how to create a simple application that stores and retrieves data from a database.
You will do that with help from the JPA and Hibernate frameworks, which will handle the database interactions for you.
Lombok will also be used to reduce boilerplate code. PostgresSQL and PgAdmin will be used as the database and database management tool, respectively.

**In the test class you would normally use a test database, but for this exercise you can use the same database as the application.**

## Exercise

1. Create a new JPA project. Use this [tutorial](../../toolbox/java/orm/JPASetup.md)
2. Create a new database called `points`
3. Update the Hibernate config file with the correct database name
4. Create a new entity called `Point` with the following fields:
    - `id` (int)
    - `x` (int)
    - `y` (int)
5. Add the correct annotations to the entity. (@Entity, @Id, @GeneratedValue)
    - Use the `identity` strategy for the `@GeneratedValue` annotation
6. Use Lombok to generate getters, toString  and a NoArgsConstructor
7. Create a constructor that takes `x` and `y` as parameters
8. Remember to add the entity to the Hibernate config file
9. Create a new class called Main and add a main method to it
10. Add the following code to the main method:

```java
    EntityManagerFactory emf = HibernateConfig.getEntityManagerFactoryConfig();
    EntityManager em = emf.createEntityManager();

        // Store 1000 Point objects in the database:
        em.getTransaction().begin();
        for (int i = 0; i < 1000; i++) {
            Point p = new Point(i, i);
            em.persist(p);
        }
        em.getTransaction().commit();

        // Find the number of Point objects in the database:
        Query q1 = em.createQuery("SELECT COUNT(p) FROM Point p");
        System.out.println("Total Points: " + q1.getSingleResult());

        // Find the average X value:
        Query q2 = em.createQuery("SELECT AVG(p.x) FROM Point p");
        System.out.println("Average X: " + q2.getSingleResult());

        // Retrieve all the Point objects from the database:
        TypedQuery<Point> query = em.createQuery("SELECT p FROM Point p", Point.class);
        List<Point> results = query.getResultList();
        for (Point p : results) {
            System.out.println(p);
        }

        // Close the database connection:
        em.close();
        emf.close();
    }
```

11. Run the code and verify that it works. Check either in PgAdmin or in IntelliJ's database tool that the data is actually stored in the database.
12. Create a DAO class and transfer all methods that interact with the database to this class.
13. Make each of the methods in the DAO class return a value instead of printing it to the console, or it's going to be difficult to test them. You do need to test the persistence of the data though.
    - The method that retrieves all Points for example should return a list of all the points from the database.
13. Add tests for each method in the DAO class. Use the `@BeforeAll` and `@AfterAll` annotations to set up and close the EntityManagerFactory and EntityManager objects.

## Conclusion

By completing this exercise, you've laid the foundation for building more complex applications that involve database interactions.
You've learned how to organize code by separating database operations into a DAO (Data Access Object) class, enhancing code modularity
and testability. Remember that this exercise only scratches the surface of what JPA and Hibernate can offer, and you can build upon this
knowledge to create sophisticated and efficient data-driven applications.
