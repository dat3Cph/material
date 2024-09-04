---
title: JPA One-To-One
description: crud examples 
layout: default
nav_order: 5
parent: ORM
grand_parent: Toolbox
permalink: /toolbox/java/jpa/one-to-one/
---

# JPA - One-To-One associations explained

In JPA (Java Persistence API), a one-to-one association is a type of relationship between two entities where each instance of one entity is associated with exactly one instance of another entity. This relationship is represented using the `@OneToOne` annotation.

## Key Points to Understand

1. **Cardinality**:
   - In a one-to-one relationship, each entity has a single corresponding entity. For example, if you have a `Person` entity and a `Passport` entity, each `Person` can have only one `Passport`, and each `Passport` can be assigned to only one `Person`.

2. **Owning vs. Non-Owning Side**:
   - **Owning Side**: The entity that contains the foreign key is considered the owning side of the relationship. This entity's table will have the column that refers to the primary key of the other entity.
   - **Non-Owning (Inverse) Side**: The other entity that does not contain the foreign key. This entity maps the relationship using the `mappedBy` attribute in the `@OneToOne` annotation.

3. **Bidirectional and Unidirectional Relationships**:
   - **Unidirectional**: Only one entity is aware of the relationship. This means only one entity has the `@OneToOne` annotation, and the other entity has no reference to the relationship.
   - **Bidirectional**: Both entities are aware of the relationship. Each entity will have a reference to the other entity, and both will use the `@OneToOne` annotation.

4. **Cascade Type**:
   - Cascade operations can be applied to propagate operations (like persist, remove) from one entity to another. This is often used in one-to-one relationships to manage both entities together.

5. **Fetch Type**:
   - By default, one-to-one relationships use `FetchType.EAGER`, meaning the related entity is fetched immediately along with the owner entity. However, you can change this to `FetchType.LAZY` if you want to load the related entity on demand.

## Example

Let's consider an example where we have two entities: `Person` and `Passport`.

### Entity Classes

```java
@Entity
public class Person {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @OneToOne(cascade = CascadeType.ALL)
    @JoinColumn(name = "passport_id", referencedColumnName = "id")
    private Passport passport;

    // Getters and setters
}

@Entity
public class Passport {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String passportNumber;

    @OneToOne(mappedBy = "passport")
    private Person person;

    // Getters and setters
}
```

## Explanation

1. **Person Entity**:
   - The `Person` entity has a `passport` field annotated with `@OneToOne`, indicating that each `Person` has one `Passport`.
   - The `@JoinColumn` specifies the foreign key column (`passport_id`) in the `Person` table that references the primary key of the `Passport` entity.

2. **Passport Entity**:
   - The `Passport` entity has a `person` field annotated with `@OneToOne(mappedBy = "passport")`. The `mappedBy` attribute specifies that the `Person` entity owns the relationship.

## Database Structure

- The `Person` table will have a column named `passport_id`, which stores the reference to the associated `Passport` entity.

## Use Cases

- One-to-one relationships are commonly used in scenarios where two entities are so closely related that they should be treated as a single entity from a data model perspective, but they still represent different concepts.

By understanding these concepts, you can effectively model and manage one-to-one relationships in JPA, ensuring that your data is accurately represented and managed within your application.

## The database schema

In the `Person` - `Passport` example with a one-to-one association in JPA, the database tables would typically look like the following:

### 1. **Person Table**

The `Person` table will contain all the fields related to the `Person` entity, including a foreign key that references the primary key of the `Passport` table.

#### **Table Structure: `Person`**

| Column Name   | Data Type    | Constraints                  |
|---------------|--------------|------------------------------|
| id            | BIGINT       | PRIMARY KEY, AUTO_INCREMENT  |
| name          | VARCHAR      | NOT NULL                     |
| passport_id   | BIGINT       | UNIQUE, FOREIGN KEY          |

- **`id`**: The primary key for the `Person` table.
- **`name`**: A column to store the name of the person.
- **`passport_id`**: A foreign key column that references the primary key (`id`) in the `Passport` table. This column is also unique because of the one-to-one relationship, ensuring that each `Person` is associated with only one `Passport`.

### 2. **Passport Table**

The `Passport` table will contain all the fields related to the `Passport` entity.

#### **Table Structure: `Passport`**

| Column Name       | Data Type    | Constraints                  |
|-------------------|--------------|------------------------------|
| id                | BIGINT       | PRIMARY KEY, AUTO_INCREMENT  |
| passport_number   | VARCHAR      | NOT NULL                     |

- **`id`**: The primary key for the `Passport` table.
- **`passport_number`**: A column to store the passport number.

### 3. **Relationship in the Tables**

- **Person Table**:
  - The `passport_id` column in the `Person` table acts as a foreign key, linking each `Person` to one `Passport`.
  - The `UNIQUE` constraint on the `passport_id` ensures that no two `Person` records can reference the same `Passport`.

- **Passport Table**:
  - There is no need for a foreign key in the `Passport` table because the `Person` table owns the relationship.

### Example of Table Content

Assume we have the following data in the `Person` and `Passport` entities:

- **Person**: { id: 1, name: "John Doe", passport_id: 101 }
- **Passport**: { id: 101, passport_number: "X12345678" }

#### **Person Table**

| id | name      | passport_id |
|----|-----------|-------------|
|  1 | John Doe  | 101         |

#### **Passport Table**

| id  | passport_number |
|-----|-----------------|
| 101 | X12345678       |

### How They Work Together

- The `Person` table's `passport_id` column references the `id` column in the `Passport` table.
- This setup allows for a strict one-to-one relationship, where each `Person` is associated with a unique `Passport`, and vice versa.

In this relational database design, the `Person` table holds the foreign key, which is typical when one side of the relationship is considered the owner (in this case, `Person`). This structure ensures the integrity and enforcement of the one-to-one relationship in the database.
