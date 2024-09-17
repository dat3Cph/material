---
title: JPA Updates Best Practices
description: How to perform partial updates in JPA
layout: default
nav_order: 11
parent: ORM
grand_parent: Toolbox
permalink: /toolbox/java/jpa/updates/
---


# Update Best Practices in JPA (Java Persistence API)

Let’s walk through how you can handle partial updates in a **plain Java** application, using **JPA** and **Hibernate** (but not Spring Boot). The same principles apply, but we’ll use **standard JPA** features like `EntityManager`.

Here's a step-by-step guide on how to handle a `PUT` or `PATCH` request where only some attributes are updated, without using Spring Boot.

### Best Practices for Handling Partial Updates in JPA (without Spring)

#### General Approach

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

This is the core part where you handle the update of the `Person` entity without relying on Spring's utilities. We will manually handle the transactions and use `EntityManager` to manage the JPA lifecycle.

#### 3.1. **Update Method**

Here’s how you can implement a partial update using plain Java and Hibernate (JPA):

```java
import javax.persistence.EntityManager;
import javax.persistence.EntityManagerFactory;
import javax.persistence.EntityTransaction;
import javax.persistence.Persistence;

public class PersonService {

    private EntityManagerFactory emf;

    public PersonService() {
        // Initialize EntityManagerFactory (configure in persistence.xml)
        this.emf = Persistence.createEntityManagerFactory("my-persistence-unit");
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

1. **`EntityManagerFactory`**: We create an `EntityManagerFactory` to manage entity managers. This factory is typically set up in a `persistence.xml` file, which defines how JPA will interact with the database.
  
2. **`EntityManager`**: For each operation, an `EntityManager` is created. This is the core JPA interface used to interact with entities and the database.

3. **Transaction Management**: We manually begin and commit (or rollback) transactions using `EntityTransaction` since we’re not relying on Spring's `@Transactional` support.
  
4. **Partial Updates**: Only the fields that are not `null` in the incoming `PersonDTO` are applied to the `Person` entity. If a field is missing in the `PersonDTO`, we leave the corresponding field in the `Person` entity unchanged.

5. **`merge()`**: The `merge()` method is used to update an existing entity in the database. It ensures the entity is synchronized with the database after modifications. Unlike `persist()`, which is used for new entities, `merge()` is used for updates.

6. **Transaction Handling**: If any exception occurs, we **rollback** the transaction to ensure consistency in the database. Afterward, the `EntityManager` is closed to free up resources.

### 4. **Null Handling and Validation**

In this approach, null checks are done manually:

- Before applying any update, we check if the field in the DTO is `null`. If it's `null`, we skip that update, ensuring that only fields explicitly provided in the request are updated.
- You can extend this with **validation** to check for valid data before applying updates.

### Persistence Configuration Example

Here’s an example of what your `persistence.xml` might look like if you're using Hibernate as the JPA provider:

#### **persistence.xml**

```xml
<persistence xmlns="https://jakarta.ee/xml/ns/persistence" version="3.0">
    <persistence-unit name="my-persistence-unit">
        <provider>org.hibernate.jpa.HibernatePersistenceProvider</provider>
        <properties>
            <property name="javax.persistence.jdbc.driver" value="com.mysql.cj.jdbc.Driver" />
            <property name="javax.persistence.jdbc.url" value="jdbc:mysql://localhost:3306/mydatabase" />
            <property name="javax.persistence.jdbc.user" value="root" />
            <property name="javax.persistence.jdbc.password" value="password" />

            <property name="hibernate.dialect" value="org.hibernate.dialect.MySQL8Dialect" />
            <property name="hibernate.hbm2ddl.auto" value="update" />
            <property name="hibernate.show_sql" value="true" />
            <property name="hibernate.format_sql" value="true" />
        </properties>
    </persistence-unit>
</persistence>
```

### 5. **Handling PUT and PATCH Requests**

If you are using a simple Java HTTP server or Servlet to handle incoming HTTP requests:

- **PUT**: You can follow this approach to update the entire resource (the whole entity) when the client sends a `PUT` request.
- **PATCH**: The same logic can be applied for `PATCH` requests, which usually update only a subset of fields.

### 6. **Alternative Approach: Reflection-Based Partial Updates**

If your entity has many fields, manually updating each field can be cumbersome. Instead, you can use **reflection** to handle partial updates dynamically.

Here’s how you can do it:

```java
import java.beans.BeanInfo;
import java.beans.Introspector;
import java.beans.PropertyDescriptor;

public class PersonService {

    public Person updatePerson(Long personId, PersonDTO updatedPersonDTO) throws Exception {
        EntityManager em = emf.createEntityManager();
        EntityTransaction tx = em.getTransaction();

        try {
            tx.begin();

            Person existingPerson = em.find(Person.class, personId);
            if (existingPerson == null) {
                throw new RuntimeException("Person not found");
            }

            // Use reflection to update only non-null properties
            BeanInfo beanInfo = Introspector.getBeanInfo(PersonDTO.class);
            for (PropertyDescriptor pd : beanInfo.getPropertyDescriptors()) {
                Object newValue = pd.getReadMethod().invoke(updatedPersonDTO);
                if (newValue != null) {
                    PropertyDescriptor entityPd = new PropertyDescriptor(pd.getName(), Person.class);
                    entityPd.getWriteMethod().invoke(existingPerson, newValue);
                }
            }

            em.merge(existingPerson);
            tx.commit();

            return existingPerson;
        } catch (Exception e) {
            if (tx.isActive()) {
                tx.rollback();
            }
            throw e;
        } finally {
            em.close();
        }
    }
}
```

This uses Java Beans reflection (`Introspector` and `PropertyDescriptor`) to automatically update fields that are non-null in the DTO, simplifying the update logic when there are many fields.

### Summary of Best Practices

- **Read-before-write**: Fetch the existing entity, modify the required fields, and merge the updated entity back to the database.
- **Selective Field Updates**: Only update the fields explicitly provided in the DTO (partial updates).
- **Manual Transaction Management**: Use `EntityTransaction` for managing transactions since Spring's `@Transactional` is not available.
- **Validation**: You can perform manual validation of fields in the DTO before applying updates.
- **Reflection**: Optionally, you can use reflection to automate the partial update of fields for larger entities.

This approach provides a clear and flexible way to handle updates in JPA without relying on Spring Boot, while still leveraging the full power of JPA and Hibernate for persistence.
