# Tuesday Exercise

**Exercise 1: Mapping Entities and Annotations**
Objective: Apply JPA annotations to map Java classes to database tables and understand entity lifecycle.

1. Create a new Java project using Maven.
2. Define a simple entity class called "Student" with attributes like `id`, `firstName`, `lastName`, and `age`.
3. Use JPA annotations to map the entity class to a database table named "students".
4. Include appropriate annotations such as `@Entity`, `@Table`, `@Id`, `@GeneratedValue`, and `@Column` to define the primary key and attributes mapping.
5. Implement lifecycle methods using `@PrePersist` and `@PreUpdate` annotations to automatically update timestamp fields for created and updated dates.
6. Write a Java program that uses the EntityManager to create and persist instances of the "Student" entity to the database.
7. Retrieve and display the list of all students using a JPQL query.
8. Update the information of a student and demonstrate how the lifecycle methods trigger.

**Exercise 2: EntityManager and Transaction Management**
Objective: Understand EntityManager's role, entity states, and transaction management.

1. Create an entity class "Product" with attributes like `id`, `name`, `price`, and `stockQuantity`.
2. Implement methods to simulate CRUD operations for the "Product" entity using EntityManager.
3. Develop a program that demonstrates the transition of entity states (transient, managed, detached, and removed) during the execution of CRUD operations.
4. Explicitly manage transactions using `EntityTransaction`. Begin transactions, perform CRUD operations within the transaction, and commit the transaction.
5. Implement a scenario where a transaction fails (e.g., due to a validation check) and ensure that the data remains consistent by rolling back the transaction.

**Exercise 3: Data Access Object (DAO) Implementation**
Objective: Implement DAO pattern for separating database access logic from business logic.

1. Design a DAO interface for the "Student" entity with methods like `create`, `read`, `update`, and `delete`.
2. Create a JPA-based implementation of the DAO interface, utilizing EntityManager for database operations.
3. Implement a class that demonstrates the use of the DAO to interact with the database, perform CRUD operations, and retrieve data.
4. Develop a program that showcases the benefits of the DAO pattern in isolating database-related code from business logic.
5. Compare the code maintainability and separation of concerns between a scenario where DAO pattern is used and where it is not.

