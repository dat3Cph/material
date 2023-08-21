### Exercise: Java JPA with Hibernate - Standard CRUD Operations on Unicorn Entity

#### Objective

Create a Java application that uses Java Persistence API (JPA) with Hibernate to perform standard CRUD (Create, Read, Update, Delete) operations on a `Unicorn` entity. Use standard JPA methods: `persist`, `merge`, `remove`, and `find`.

#### Prerequisites

1. JDK installed.
2. An IDE (IntelliJ IDEA)
3. A relational database (PostgreSQL).
4. Maven for dependency management.

![Alt text](../images/unicorn.png)

#### Steps

1. **Set Up a New Project**:
   - Create a new Maven project in your IDE using this [tutorial](https://github.com/dat3Cph/backend/blob/main/setup/JPASetup.md)

2. Create a new database in Postgres for the project.

3. **Create the Entity Class**:
   - Create a new Java class named `Unicorn`.
   - Add attributes: `id`, `name`, `age`, and `powerStrength`.
   - Annotate `id` with `@Id` and `@GeneratedValue`.
   - Annotate the class with `@Entity`.

5. **Create UnicornDAO Class**:
   - Create a new class named `UnicornDAO`.
   - Implement methods for CRUD operations using standard JPA methods:
      - `save(Unicorn unicorn)` using `EntityManager.persist()`
      - `update(Unicorn unicorn)` using `EntityManager.merge()`
      - `delete(int id)` using `EntityManager.remove()`
      - `findById(int id)` using `EntityManager.find()`
      - Peek at these [snippets](UnicornSnippets.md) for inspiration.

6. **Main Application**:
   - Create a `main` class.
   - Inside `main`, instantiate `UnicornDAO`.
   - Demonstrate CRUD operations:
      - Create a `Unicorn` and save it using `persist`.
      - Update the saved `Unicorn` using `merge`.
      - Fetch the updated `Unicorn` by ID using `find` and display its attributes.
      - Delete the `Unicorn` by ID using `remove`.

7. **Run and Test**:
   - Run your application.
   - Validate that each CRUD operation is functioning by examining the console output and checking the database.

#### Expected Outcome

After running the application, you should be able to see the `Unicorn` entity being created, updated, fetched, and deleted in both your database and console output, utilizing standard JPA methods.

#### Bonus Challenge

1. Implement a method `findAll()` in `UnicornDAO` that retrieves all `Unicorn` entities using the `EntityManager.createQuery()` method.
2. Add validation constraints to the `Unicorn` entity, such as `name` should not be null or empty and `powerStrength` should be between 1 and 100.

By completing this exercise, you will gain practical experience with standard JPA CRUD operations using Hibernate as the provider.