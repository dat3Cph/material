# Tuesday Exercise

**Exercise 1: Hibernate and JPA Basics**

- Question: Describe the key components of the JPA architecture and how they relate to each other. (Entity Classes, EntityManager, EntityManagerFactory, Entity Mapping Annotations, Persistence Provider (Hibernate), Query Language(JPQL))
- Question: Explain the difference between Hibernate and JPA.

**Exercise 2: JPQL**
Objective: Understand the purpose of JPQL and how it differs from SQL.

- Question: Explain the purpose of JPQL and how it differs from SQL.

**Exercise 3: Mapping Entities and Annotations**
Objective: Apply JPA annotations to map Java classes to database tables and understand entity lifecycle.

1. Create a new Java project using Maven.
2. Define a simple entity class called "Student" with attributes like `id`, `firstName`, `lastName`, and `age`.
3. Use JPA annotations to map the entity class to a database table named "students".
4. Include appropriate annotations such as `@Entity`, `@Table`, `@Id`, `@GeneratedValue`, and `@Column` to define the primary key and attributes mapping. 
5. Write a Java program that uses the EntityManager to create and persist instances of the "Student" entity to the database. 
6. Retrieve and display the list of all students using a JPQL query. 
7. Update the information of a student and demonstrate how the lifecycle methods trigger.

- Question: Explain the purpose of the `@GeneratedValue` annotation and how it can be used to generate primary key values for entities. 
- Question: Explain the difference between the `AUTO`, `IDENTITY`, and `SEQUENCE` strategies  in conjunction with the `@GeneratedValue` annotation.

**Exercise 4: EntityManager and Transaction Management**
Objective: Understand EntityManager's role, entity states, and transaction management.

- Question: Explain the roles and responsibilities of EntityManager and EntityManagerFactory in JPA.
- Question: Describe the lifecycle states of JPA entities (transient, managed, detached, removed). Provide an example scenario for each state.



