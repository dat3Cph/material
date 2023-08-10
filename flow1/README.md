# Flow 1 Learning Objectives and Technologies

## Technologies used in flow 1:

- Maven
- JUnit 5
- JPQL
- JDBC
- JPA
- Hibernate
- IntelliJ
- Java 17
- PostgresQl
- pgAdmin
- Docker

## Learning Objectives:

### Week 1:

**Monday:** 

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
  - Be able to explain and demonstrate JPA lifecycle annotations like @PrePersist, @PostPersist, @PreUpdate, @PostUpdate, @PreRemove, @PostRemove, @PostLoad
  - Understand the purpose of Lombok and how it reduces boilerplate code in Java entities.
- EntityManager and EntityManagerFactory
  - Differentiate between the responsibilities of EntityManager and EntityManagerFactory in the context of JPA.
  - Be able to explain the lifecycle management of the EntityManager.
  - When is an entity in a transient, managed, detached or removed state?
  - Explain the difference between the methods persist and merge and when to use them.
- Database transactions with help of JPA, Hibernate, JDBC, PostgresSQL and DAO.
  - Be able to explain and demonstrate how to use the EntityManager to perform CRUD operations like create, read, update and delete.
  - Explain the Data Access Object (DAO) architecture and its benefits in separating database access logic from business logic.

**Wednesday:**

- JPQL
  - Be able to explain the purpose of JPQL and how it differs from SQL.
  - What is the difference between TypedQuery and Query and when to use them.
  - Be able to demonstrate and explain how to use NamedQueries.
  - Be able to demonstrate code with complex JPQL queries using joins, aggregate functions, group by, order by, having, subqueries and native queries.
  - Be able to explain the difference between the methods `createQuery` and `createNamedQuery`.
  - Be able to explain the difference between the methods `getResultList` and `getSingleResult`.
  - Be able to explain the difference between the methods `setParameter` and `setParameters`.
  - Be able to explain the difference between the methods `executeUpdate` and `executeQuery`.
  - Be able to explain the difference between the methods `getFirstResult` and `setMaxResults`.
  - Be able to explain the difference between the methods `getSingleResult` and `getResultList`.
- JPA relations between entities
  - Be able to explain and demonstrate the use of the annotations @OneToMany, @ManyToOne, @OneToOne, @ManyToMany and @JoinColumn.
  - Be able to explain the difference between unidirectional and bidirectional relationships.
  - Be able to explain the difference between eager and lazy loading.
  - Be able to explain and demonstrate cascading and orphan removal.
- Date and Time
  - Explore how Java Date and Time API integrates with JPA for managing date and time-related data.
  - Handle different types of date and time data using JPA annotations.



