---
title: Learning Objectives Part 1
description: JPA Learning objectives
layout: default
nav_order: 1
has_children: true
parent: JPA Part 1
grand_parent: JPA
permalink: /jpa-part-1/learning-objectives-part-1/
---

# JPA Part 1

## Learning Objectives

1. Be able to create a simple Maven project with JUnit 5, Hibernate, PostgresSQL and JPA.
    - Create a PostgresSQL server and a database with help of Docker.
    - How to configure Hibernate to establish a database connection.
    - Run the project in a main and a test method and verify that the connection is working in pgAdmin
2. Hibernate and JPA
    - Be able to explain the difference between Hibernate and JPA.
    - Describe the key components of the JPA architecture and their relationships.
3. JPA entities and annotations
    - Be able to use and understand the basic annotations of JPA in classes, properties and methods.
    - Apply JPA annotations to map Java classes to database tables.
    - Be able to explain and demonstrate the use of the annotations @Entity, @Table, @Id, @GeneratedValue, @Column
4. EntityManager and EntityManagerFactory
    - Differentiate between the responsibilities of EntityManager and EntityManagerFactory in the context of JPA.
    - Be able to explain the lifecycle management of the EntityManager.
    - When is an entity in a transient, managed, detached or removed state?
    - Explain the difference between the methods persist and merge and when to use them.
5. Database transactions with help of JPA, Hibernate, JDBC, PostgresSQL.
    - Be able to explain and demonstrate how to use the EntityManager to perform CRUD operations like create, read, update and delete.
6. JPQL (Java Persistence Query Language) Part 1
    - Be able to explain the purpose of JPQL and how it differs from SQL.
    - Be able to write JPQL queries using the SELECT, FROM, WHERE and ORDER BY clauses.
    - Be able to write JPQL queries using aggregate functions COUNT, SUM and MIN.
7. JPQL (Java Persistence Query Language) Part 2
    - Be able to explain and demonstrate Named Queries.
    - Be able to explain the difference between TypedQuery vs Query in JPA.
    - Be able to write JPQL queries using aggregate functions MAX, AVG and DISTINCT.
8. JPA entities and annotations
    - Be able to explain and demonstrate JPA lifecycle annotations like @PrePersist, @PostPersist, @PreUpdate, @PostUpdate, @PreRemove, @PostRemove, @PostLoad.
9. Data Access Object (DAO) Architecture
    - Be able to explain and demonstrate the benefits of using a DAO architecture for separating database access logic from business logic.
10. Be able to explain and implement the Singleton design pattern.
11. Date and Time
    - Explain how Java Date and Time API integrates with JPA for managing date and time-related data.
    - Demonstrate the different types of date and time data using JPA annotations.
12. Lombok
    - Be able to explain the purpose of Lombok and how it reduces boilerplate code in Java entities.
    - Explain and demonstrate how to add a private constructor to a class with Lombok.
    - Explain and demonstrate Lombok @Data, @AllArgConstructor, @RequiredArgsConstructor and @Builder annotations.
