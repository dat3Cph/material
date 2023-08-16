# JPA Week 1

## Learning Objectives

### Monday

- Be able to create a simple Maven project with JUnit 5, Hibernate, PostgresSQL and JPQL.
    - Create a PostgresSQL server and a database with help of Docker.
    - How to configure Hibernate to establish a database connections.
    - Run the project in a main and a test method and verify that the connection is working in pgAdmin
- Hibernate and JPA
    - Be able to explain the difference between Hibernate and JPA.
    - Describe the key components of the JPA architecture and their relationships.
- JPA entities and annotations
    - Be able to use and understand the basic annotations of JPA in classes, properties and methods.
    - Apply JPA annotations to map Java classes to database tables and define relationships.
    - Be able to explain and demonstrate the use of the annotations @Entity, @Table, @Id, @GeneratedValue, @Column
- EntityManager and EntityManagerFactory
    - Differentiate between the responsibilities of EntityManager and EntityManagerFactory in the context of JPA.
    - Be able to explain the lifecycle management of the EntityManager.
    - When is an entity in a transient, managed, detached or removed state?
    - Explain the difference between the methods persist and merge and when to use them.
- Database transactions with help of JPA, Hibernate, JDBC, PostgresSQL.
    - Be able to explain and demonstrate how to use the EntityManager to perform CRUD operations like create, read, update and delete.


### Wednesday

- JPQL
    - Be able to explain the purpose of JPQL and how it differs from SQL.
    - Be able to write JPQL queries using the SELECT, FROM, WHERE, GROUP BY, HAVING, and ORDER BY clauses.
    - Be able to write JPQL queries using aggregate functions like COUNT, SUM, MIN, MAX, and AVG.
    - Be able to explain and demonstrate Named Queries.
    - Be able to explain the difference between TypedQuery vs Query in JPA.
- JPA entities and annotations
    - Be able to explain and demonstrate JPA lifecycle annotations like @PrePersist, @PostPersist, @PreUpdate, @PostUpdate, @PreRemove, @PostRemove, @PostLoad
    - Understand the purpose of Lombok and how it reduces boilerplate code in Java entities.
- Data Access Object (DAO) Architecture
    - Be able to explain the benefits of using a DAO architecture for separating database access logic from business logic.
- Date and Time
    - Explore how Java Date and Time API integrates with JPA for managing date and time-related data.
    - Handle different types of date and time data using JPA annotations.