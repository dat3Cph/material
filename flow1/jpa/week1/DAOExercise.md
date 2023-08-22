# DAO Exercise

**Exercise 1: Data Access Object (DAO) Implementation**
Objective: Implement DAO pattern for separating database access logic from business logic.

1. Design a DAO interface for the "Student" entity with methods like `create`, `read`, `update`, and `delete`.
2. Create a JPA-based implementation of the DAO interface, utilizing EntityManager for database operations.
3. Implement a class that demonstrates the use of the DAO to interact with the database, perform CRUD operations, and retrieve data.

- Question: Explain the benefits of using a DAO architecture for separating database access logic from business logic.

Implement lifecycle methods using `@PrePersist` and `@PreUpdate` annotations to automatically update timestamp fields for created and updated dates.