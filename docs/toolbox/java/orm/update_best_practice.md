---
title: JPA Updates Best Practices
description: How to perform partial updates in JPA
layout: default
nav_order: 11
parent: ORM
grand_parent: Toolbox
permalink: /toolbox/java/jpa/updates/
---


# Best Practices for Handling Partial Updates in JPA

Let’s walk through how you can handle partial updates in a **plain Java** application, using **JPA** and **Hibernate**.

Here's a step-by-step guide on how to handle a `PUT` or `PATCH` request where only some attributes are updated.

## General Approach

1. **Fetch the entity from the database**.
2. **Apply only the provided changes** to the entity.
3. **Persist the updated entity** using JPA, making sure to update only the fields that need changing and leaving the rest untouched.

This ensures that you're only updating the fields present in the request, avoiding overwriting unchanged attributes.

### Example Setup

#### 1. **DTO for Incoming Request**

Assume you have a DTO class to represent the incoming JSON request payload for a `Person` entity.

```java
public class PersonDTO {
    private String firstName;
    private String lastName;
    private Integer age;
    private String email;

    // Getters and Setters
}
```

#### 2. **Person Entity**

Your entity class, `Person`, represents the database table and will be managed by JPA.

```java
import javax.persistence.*;

@Entity
@Table(name = "persons")
public class Person {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String firstName;
    private String lastName;
    private Integer age;
    private String email;

    // Getters and Setters
}
```

### 3. **Service Layer for Updating an Entity**

This is the core part where you handle the update of the `Person` entity. We will manually handle the transactions and use `EntityManager` to manage the JPA lifecycle.

#### 3.1. **Update Method**

Here’s how you can implement a partial update using plain Java and Hibernate (JPA):

```java
import javax.persistence.EntityManager;
import javax.persistence.EntityManagerFactory;
import javax.persistence.EntityTransaction;
import javax.persistence.Persistence;

public class PersonService {

    private EntityManagerFactory emf;

    public PersonService(EntityManagerFactory emf) {
        // Initialize EntityManagerFactory (configure in persistence.xml)
        this.emf = emf;
    }

    public Person updatePerson(Long personId, PersonDTO updatedPersonDTO) {
        EntityManager em = emf.createEntityManager();
        EntityTransaction tx = em.getTransaction();

        try {
            // Start transaction
            tx.begin();

            // Fetch the existing person from the database
            Person existingPerson = em.find(Person.class, personId);
            if (existingPerson == null) {
                throw new RuntimeException("Person not found");
            }

            // Update only the fields that are not null in the DTO
            if (updatedPersonDTO.getFirstName() != null) {
                existingPerson.setFirstName(updatedPersonDTO.getFirstName());
            }

            if (updatedPersonDTO.getLastName() != null) {
                existingPerson.setLastName(updatedPersonDTO.getLastName());
            }

            if (updatedPersonDTO.getAge() != null) {
                existingPerson.setAge(updatedPersonDTO.getAge());
            }

            if (updatedPersonDTO.getEmail() != null) {
                existingPerson.setEmail(updatedPersonDTO.getEmail());
            }

            // Merge the updated entity to persist changes
            em.merge(existingPerson);

            // Commit the transaction
            tx.commit();

            return existingPerson;
        } catch (Exception e) {
            if (tx.isActive()) {
                tx.rollback();
            }
            throw e; // Propagate the exception or handle it appropriately
        } finally {
            em.close(); // Always close the EntityManager to avoid memory leaks
        }
    }

    // Other CRUD methods would go here...
}
```

### Explanation of the Code

1. **`EntityManagerFactory`**: We get an `EntityManagerFactory` to manage entity managers. This factory is typically set up in a `HibernateConfig` file, which defines how JPA will interact with the database.
  
2. **`EntityManager`**: For each operation, an `EntityManager` is created. This is the core JPA interface used to interact with entities and the database.

3. **Transaction Management**: We manually begin and commit (or rollback) transactions using `EntityTransaction`.
  
4. **Partial Updates**: Only the fields that are not `null` in the incoming `PersonDTO` are applied to the `Person` entity. If a field is missing in the `PersonDTO`, we leave the corresponding field in the `Person` entity unchanged.

5. **`merge()`**: The `merge()` method is used to update an existing entity in the database. It ensures the entity is synchronized with the database after modifications. Unlike `persist()`, which is used for new entities, `merge()` is used for updates.

6. **Transaction Handling**: If any exception occurs, we **rollback** the transaction to ensure consistency in the database. Afterward, the `EntityManager` is closed to free up resources.

### 4. **Null Handling and Validation**

In this approach, null checks are done manually:

- Before applying any update, we check if the field in the DTO is `null`. If it's `null`, we skip that update, ensuring that only fields explicitly provided in the request are updated.
- You can extend this with **validation** to check for valid data before applying updates.

### 5. **Handling PUT and PATCH Requests**

If you are using a simple Java HTTP server or Servlet to handle incoming HTTP requests:

- **PUT**: You can follow this approach to update the entire resource (the whole entity) when the client sends a `PUT` request.
- **PATCH**: The same logic can be applied for `PATCH` requests, which usually update only a subset of fields.

### Summary of Best Practices

- **Read-before-write**: Fetch the existing entity, modify the required fields, and merge the updated entity back to the database.
- **Selective Field Updates**: Only update the fields explicitly provided in the DTO (partial updates).
- **Manual Transaction Management**: Use `EntityTransaction` for managing transactions since Spring's `@Transactional` is not available.
- **Validation**: You can perform manual validation of fields in the DTO before applying updates.

This approach provides a clear and flexible way to handle updates in JPA without relying on Spring Boot, while still leveraging the full power of JPA and Hibernate for persistence.
