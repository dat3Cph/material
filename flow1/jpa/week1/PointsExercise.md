# The Point exercise

## Links

- [JPA Project Setup](https://github.com/dat3Cph/backend/blob/main/setup/JPASetup.md)

## Introduction

Welcome to "The Point" exercise! This exercise will introduce you to the basics of JPA and Hibernate,
and you will learn how to create a simple application that stores and retrieves data from a database.
You will do that with help from the JPA and Hibernate frameworks, which will handle the database interactions for you.
Lombok will also be used to reduce boilerplate code. PostgresSQL and PgAdmin will be used as the database and database management tool, respectively.

## Exercise

1. Create a new JPA project. (Link above)
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
8. Create a new class called Main and add a main method to it
9. Add the following code to the main method:
```jav
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

10. Run the code and verify that it works. Check either in PgAdmin or in IntelliJ's database tool that the data is actually stored in the database.
11. Create a DAO class and transfer all methods that interact with the database to this class.
12. Add tests for each method in the DAO class. Use the `@BeforeAll` and `@AfterAll` annotations to set up and tear down the database connection.

## Conclusion

By completing this exercise, you've laid the foundation for building more complex applications that involve database interactions. 
You've learned how to organize code by separating database operations into a DAO (Data Access Object) class, enhancing code modularity 
and testability. Remember that this exercise only scratches the surface of what JPA and Hibernate can offer, and you can build upon this 
knowledge to create sophisticated and efficient data-driven applications.

