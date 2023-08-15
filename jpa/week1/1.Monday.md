# Day 1 - JPA Introduction

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
- Date and Time
    - Explore how Java Date and Time API integrates with JPA for managing date and time-related data.
    - Handle different types of date and time data using JPA annotations.

***

## Videos internal resources

- [JPA Introduction](#)
- [JPA Entities](#)

## Videos external resources
- [Entity Lifecycle Model](https://www.youtube.com/watch?v=tciSOIQngig)
- [Best practice advices jpa relation mapping](https://www.youtube.com/watch?v=tciSOIQngig)
- [Pagination in JPQL](https://www.youtube.com/watch?v=Xny3OJquWuo)

## Links external resources

- [JAVA Persistence](https://en.wikibooks.org/wiki/Java_Persistence)
- [JPA Manual](https://www.objectdb.com/java/jpa/tool)
- [Thorben Hansen](https://thorben-janssen.com/)
- [JPA Tutorial](https://www.javacodegeeks.com/jpa-tutorial)
- [Interface EntityManager](https://docs.oracle.com/javaee/5/api/javax/persistence/EntityManager.html)


## 1. How to create a simple Maven project with JUnit 5, Hibernate, PostgresSQL and Lombok.

    - Open IntelliJ and create a new project.
    - Select Maven and Java 17.
    - In advanced settings, add groupId and artifactId(is mostly the project name).
    - Click finish.
    - Open the pom.xml file and add the following dependencies: https://gist.github.com/tysker/33f364970e366ba1d2daf96d034abea6
        - JUnit 5
        - Hibernate
        - PostgresSQL
        - Lombok

   - Add the following properties to the pom.xml file:
    ```xml
        <properties>
            <hibernate-version>6.2.4.Final</hibernate-version>
            <junit.version>5.9.1</junit.version>
        </properties>
    ```
   - Create a new java class file called HibernateConfig.
   - copy and paste the following gist into the file: https://gist.github.com/tysker/cdf831680b964aa8dedd5545079e43b2

*** 

## 2. Hibernate and JPA

**What are the similarities and differences between JPA and hibernate?**


Java Persistence API (JPA) and Hibernate are closely related concepts, but they have distinct roles and relationships. Let's examine the similarities and differences between them:

**Similarities:**

1. **ORM Framework:** Both JPA and Hibernate are related to Object-Relational Mapping (ORM), which is the practice of mapping object-oriented concepts to relational database structures.

2. **Entity Mapping:** Both JPA and Hibernate provide mechanisms to map Java objects (entities) to database tables and vice versa. This includes defining relationships, specifying attributes, and managing persistence.

3. **Persistence Context:** Both JPA and Hibernate manage a persistence context, which is an in-memory cache of managed entities. This context tracks changes to entities and facilitates their synchronization with the database.

4. **Querying:** Both JPA and Hibernate offer query languages for retrieving data from the database. JPA uses JPQL (Java Persistence Query Language), while Hibernate provides its own query language called HQL (Hibernate Query Language), which is similar to JPQL.

5. **Transaction Management:** Both JPA and Hibernate support transaction management, allowing you to define and manage transactions around database operations.

**Differences:**

1. **Standard vs. Implementation:** JPA is a specification developed as a part of the Java EE (now Jakarta EE) platform. It defines a standard API for working with ORM in Java applications. Hibernate, on the other hand, is a specific implementation of the JPA specification. Other implementations of JPA also exist, such as EclipseLink and Apache OpenJPA.

2. **Portability:** JPA aims to provide portability by offering a standardized API. Applications written using JPA can be more easily switched between different JPA providers, although some variations might exist due to provider-specific features.

3. **API Complexity:** JPA focuses on providing a simplified API for ORM operations, adhering to a common set of features across different providers. Hibernate, being a more feature-rich implementation, provides additional features and capabilities beyond what is mandated by the JPA specification.

4. **Configuration:** JPA provides a standardized way of configuring persistence units in `persistence.xml`. Hibernate offers more extensive configuration options, including its own configuration file (`hibernate.cfg.xml`), annotations, and programmatic configuration.

5. **Extensibility and Advanced Features:** Hibernate offers many advanced features that go beyond the JPA specification, such as caching strategies, custom data types, and event listeners. These features are Hibernate-specific and may not be available in other JPA implementations.

6. **Community and Ecosystem:** Hibernate has its own active and well-established community, with a wealth of resources and documentation available. JPA implementations other than Hibernate might have smaller communities and fewer resources.

In summary, JPA provides a standardized API for ORM in Java applications, while Hibernate is a specific implementation of this API with additional features and capabilities. Developers can choose between using the standardized JPA API for portability or leveraging Hibernate's rich set of features for more complex use cases.

*** 

**Key components of the JPA architecture and their relationships.**

The Java Persistence API (JPA) architecture consists of several key components that work together to provide a standardized way to map Java objects to relational database structures and manage their persistence. Here are the key components of the JPA architecture and their relationships:

1. **Entity:**
    - An entity is a Java class that is mapped to a database table. It represents a persistent object that can be stored, retrieved, and manipulated in the database.
    - Entities are defined using plain Java classes and annotated with JPA annotations to specify their mappings and relationships.

2. **EntityManager:**
    - The EntityManager is a core component of JPA responsible for managing the lifecycle and persistence of entities.
    - It acts as a bridge between Java objects and the database, allowing you to perform CRUD (Create, Read, Update, Delete) operations on entities.
    - EntityManager provides methods for persisting, querying, updating, and removing entities, as well as managing transactions.

3. **Persistence Unit:**
    - A persistence unit is a logical grouping of entities and configuration information.
    - It is defined in the `persistence.xml` configuration file and contains settings such as database connection details, entity mapping information, and other JPA-related configurations.

4. **Entity Manager Factory:**
    - The EntityManagerFactory is a factory class responsible for creating and managing EntityManager instances.
    - It is typically created once per application and is used to create multiple EntityManager instances throughout the application's lifecycle.

5. **Entity Transaction:**
    - The EntityTransaction interface provides methods for managing transactions in JPA.
    - It allows you to start, commit, and rollback transactions involving one or more EntityManager instances.

6. **JPQL (Java Persistence Query Language):**
    - JPQL is a query language similar to SQL but used specifically to query JPA-managed entities.
    - JPQL queries operate on entity objects and abstract away the underlying database structure, allowing for database-agnostic querying.

7. **Persistence Context:**
    - The persistence context is a cache-like area within the EntityManager that holds managed entity instances.
    - It tracks changes made to entities, ensures their synchronization with the database, and manages relationships and associations.

8. **Mapping Annotations:**
    - JPA provides a set of annotations that allow you to specify how entities are mapped to database tables, columns, and relationships.
    - Annotations like `@Entity`, `@Table`, `@Column`, `@OneToMany`, `@ManyToOne`, etc., are used to define mappings and relationships.

9. **Lifecycle Callbacks:**
    - JPA allows you to define lifecycle callback methods in entities to execute custom logic at specific points in an entity's lifecycle, such as `@PrePersist`, `@PostLoad`, etc.

10. **ORM Provider (JPA Implementation):**
    - The ORM provider is responsible for implementing the JPA specification and providing the underlying functionality.
    - Hibernate, EclipseLink, and others are popular JPA providers that implement the JPA specification and offer additional features beyond the standard.

In the JPA architecture, entities, the EntityManager, and the EntityManagerFactory are central components that work together to manage the persistence of Java objects in a relational database. The mapping annotations define how Java classes correspond to database tables and columns, while JPQL provides a way to query and manipulate these entities using a Java-centric query language.


## 3. JPA entities and annotations

**JPA lifecycle**

1. **New (Transient) State:**
- An entity is in the "new" or "transient" state when it has been instantiated but is not yet associated with a persistence context.
- In this state, the entity is not being managed by JPA, and changes made to it are not automatically synchronized with the database.

2. **Managed State:**
- An entity transitions to the "managed" state when it is associated with a persistence context. This occurs when you call `EntityManager.persist()` on a new entity.
- In the managed state, changes to the entity's properties are tracked, and they will be automatically synchronized with the database upon the next flush or transaction commit.

3. **Detached State:**
- An entity enters the "detached" state when it was once managed by a persistence context but has since been detached from that context. This can occur when an EntityManager is closed or when an explicit detachment is performed.
- In the detached state, changes to the entity are no longer tracked by JPA. You need to re-attach the entity to a new persistence context to persist any further changes.

4. **Removed State:**
- An entity enters the "removed" state when you call `EntityManager.remove()` on a managed entity. This marks the entity for deletion during the next flush or commit.
- The entity remains in this state until the next flush or commit operation, when it will be deleted from the database.

***

**JPA lifecycle annotations**

1. Pre-Persist (@PrePersist):
   This event is triggered just before an entity is persisted to the database.
   It's commonly used for tasks like setting default values, generating timestamps, or performing validation before insertion.

2. Pre-Update (@PreUpdate):
   This event occurs before an entity is updated in the database.
   It's often used for updating timestamps, tracking changes, or performing validation before updates.

3. Pre-Remove (@PreRemove):
   This event is triggered just before an entity is removed from the database.
   It can be used for actions like cleaning up associated data or performing validation before deletion.

4. Post-Persist (@PostPersist):
   This event occurs after an entity has been persisted to the database.
   It can be useful for tasks that need to be performed after a successful insertion, such as sending notifications or updating related entities.

5. Post-Update (@PostUpdate):
   This event is triggered after an entity has been updated in the database.
   It's often used for auditing, logging changes, or triggering additional actions based on updates.

6. Post-Remove (@PostRemove):
   This event occurs after an entity has been removed from the database.
   It can be used for tasks like updating related entities, generating historical records, or logging deletion events.

7. Post-Load (@PostLoad):
   This event is triggered when an entity is retrieved from the database.
   It's commonly used to initialize transient fields, calculate derived values, or perform additional loading-related operations.

*** 

## 4. Data Access Object (DAO) architecture

The Data Access Object (DAO) architecture is a design pattern that separates the data access logic from the rest of an application's business logic. It provides an abstraction layer between the application's domain/business logic and the underlying data storage mechanism (usually a relational database). The DAO pattern aims to improve modularity, maintainability, and code reusability by encapsulating data-related operations in dedicated classes.

Here's how the DAO architecture works:

1. **Data Access Objects (DAOs):**
    - DAOs are classes that encapsulate the logic for accessing and manipulating data in a specific data source (e.g., a database table).
    - Each DAO is responsible for a specific entity or data structure and provides methods for common operations like CRUD (Create, Read, Update, Delete).

2. **Domain/Business Logic:**
    - The core business logic of an application resides in the higher layers, separate from the DAOs.
    - The business logic uses DAO methods to interact with the data source without needing to know the specific details of data access.

3. **Abstraction:**
    - The DAO pattern provides an abstraction layer that hides the complexities of data access and database interactions.
    - This abstraction allows changes to the data source (such as switching databases) without affecting the application's business logic.

4. **Isolation:**
    - By isolating data access code in DAOs, changes to the database schema, queries, or data access logic can be localized to the DAO classes.
    - This isolation minimizes the impact of changes on the rest of the application.

5. **Code Reusability:**
    - DAOs promote code reusability by centralizing data access logic. Other parts of the application can reuse the same DAO methods across different components.

6. **Testing:**
    - DAOs can be individually tested in isolation using mock data sources or in-memory databases, making testing of data access logic more focused and controllable.

7. **Transaction Management:**
    - DAOs can encapsulate transaction management logic, ensuring that data operations within a single transaction are consistent and adhere to the ACID properties.

8. **Decoupling:**
    - The DAO pattern reduces coupling between data access and application logic. This separation makes the codebase more modular and easier to maintain.

A simplified example of a DAO might involve a `UserDAO` class that provides methods for CRUD operations on a `User` entity. The business logic in the application can then use these methods to interact with user data without needing to know the specific details of the database interactions.

The DAO pattern is commonly used in combination with other design patterns and frameworks, such as Object-Relational Mapping (ORM) tools like Hibernate or JPA, to further simplify and streamline the data access process.