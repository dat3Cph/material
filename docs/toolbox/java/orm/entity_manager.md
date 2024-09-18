---
title: JPA Entity Manager(Factory)
description: entity manager in JPA
layout: default
nav_order: 3
parent: ORM
grand_parent: Toolbox
permalink: /toolbox/java/jpa/entity-manager/
---

# The role of the entity manager in JPA

**Prompt: What is the role of the entity manager in JPA?**

The Entity Manager in Java Persistence API (JPA) acts as a crucial interface between the Java application and the database. It is responsible for managing the lifecycle of entities and performs various operations like persisting, merging, finding, and removing entities. The Entity Manager is a part of the JPA persistence context, which is essentially a cache of managed entities that helps maintain object-relational mapping and manage transactions.

### Role of Entity Manager in JPA

1. **Managing Entity Lifecycle**: The Entity Manager controls the lifecycle of entities, transitioning them through states like New (Transient), Managed, Detached, and Removed.

    - **Transient**: Entities that are just created but have not yet been associated with an Entity Manager.
    - **Managed**: Entities that are associated with an Entity Manager's persistence context and represent data that is synchronized with the database.
    - **Detached**: Entities that were previously managed but are no longer associated with an Entity Manager.
    - **Removed**: Entities that are scheduled for deletion from the database.

2. **CRUD Operations**: Provides APIs for basic CRUD (Create, Read, Update, Delete) operations.
  
    - `persist()`: To insert a new entity into the database.
    - `find()`: To retrieve an entity from the database.
    - `merge()`: To update an existing entity.
    - `remove()`: To delete an entity from the database.

3. **Query Execution**: It executes JPQL (Java Persistence Query Language), Criteria API queries, and named queries to fetch data from the database.

4. **Transaction Management**: Manages transactions to ensure data consistency. This can include beginning, committing, and rolling back transactions.

5. **Cache Management**: Manages a first-level cache (persistence context) to store entities that have been read or written in the current transaction, reducing the need for frequent database hits.

6. **Relationship Management**: Manages relationships between entities such as one-to-one, one-to-many, many-to-one, and many-to-many.

7. **Cascade Operations**: Automatically propagates operations like `persist`, `merge`, and `remove` to related entities.

8. **Concurrency**: Handles optimistic and pessimistic locking to manage concurrent access to entities.

9. **Entity State Synchronization**: At the end of a transaction, changes made to managed entities are automatically synchronized with the database.

10. **Callbacks and Listeners**: Allows the definition of callback methods (`@PrePersist`, `@PostPersist`, `@PreRemove`, etc.) that get triggered on entity lifecycle events.

### Example of Using Entity Manager

```java
EntityManagerFactory emf = Persistence.createEntityManagerFactory("myJpaUnit");
EntityManager em = emf.createEntityManager();

// Begin Transaction
em.getTransaction().begin();

// Create and Persist an Entity
User newUser = new User("John", "john@email.com");
em.persist(newUser);

// Find an Entity
User foundUser = em.find(User.class, newUser.getId());

// Update an Entity
foundUser.setName("John Doe");
em.merge(foundUser);

// Remove an Entity
em.remove(foundUser);

// Commit Transaction
em.getTransaction().commit();

// Close resources
em.close();
emf.close();
```

In this example, an `EntityManager` instance is created from an `EntityManagerFactory`. We then start a transaction, perform some CRUD operations, and finally commit the transaction. After the operations are done, the resources are closed.
