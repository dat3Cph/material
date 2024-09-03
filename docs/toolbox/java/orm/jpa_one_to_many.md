---
title: JPA One-To-Many
description: One to Many relationship in JPA
layout: default
nav_order: 6
parent: ORM
grand_parent: Toolbox
permalink: /toolbox/java/jpa/one-to-many/
---

# JPA - One-To-Many associations explained

In JPA, a one-to-many association is a relationship where one entity is associated with multiple instances of another entity. This is typically represented using the `@OneToMany` annotation on the owning side of the relationship and the `@ManyToOne` annotation on the other side.

## Key Points to Understand

1. **Cardinality**:
   - In a one-to-many relationship, one entity (the parent) is associated with multiple instances of another entity (the child). For example, a `Department` entity might have many `Employee` entities.

2. **Owning Side**:
   - The many side (the child entity) is usually the owning side of the relationship because it contains the foreign key that references the primary key of the one side (the parent entity).

3. **Bidirectional and Unidirectional Relationships**:
   - **Unidirectional**: The parent entity knows about the child entities, but the child entities do not have a reference back to the parent. Only the `@OneToMany` annotation is used.
   - **Bidirectional**: Both entities are aware of the relationship. The parent entity has a `@OneToMany` annotation, and the child entity has a `@ManyToOne` annotation.

4. **Cascade Type and Fetch Type**:
   - Cascade operations can propagate changes from the parent to the children.
   - Fetch type for a `@OneToMany` relationship is `LAZY` by default, meaning the child entities are loaded on demand.

## Example

Let's consider an example where we have two entities: `Department` and `Employee`.

### Entity Classes

```java
@Entity
public class Department {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @OneToMany(mappedBy = "department", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<Employee> employees = new ArrayList<>();

    // Getters and setters
}

@Entity
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @ManyToOne
    @JoinColumn(name = "department_id")
    private Department department;

    // Getters and setters
}
```

## Explanation

1. **Department Entity**:

   - The `Department` entity has a `List<Employee>` field annotated with `@OneToMany`, indicating that a department can have multiple employees.
   - The `mappedBy` attribute specifies that the `department` field in the `Employee` entity owns the relationship.
   - `cascade = CascadeType.ALL` ensures that operations on the `Department` entity cascade to the `Employee` entities.
   - `orphanRemoval = true` ensures that if an `Employee` is removed from the `List<Employee>`, it will also be removed from the database.

2. **Employee Entity**:

   - The `Employee` entity has a `department` field annotated with `@ManyToOne`, indicating that each employee belongs to one department.
   - The `@JoinColumn` annotation specifies the foreign key column (`department_id`) in the `Employee` table that references the primary key of the `Department` entity.

## Database Structure

### **Department Table**

| Column Name | Data Type    | Constraints                  |
|-------------|--------------|------------------------------|
| id          | BIGINT       | PRIMARY KEY, AUTO_INCREMENT  |
| name        | VARCHAR      | NOT NULL                     |

- **`id`**: The primary key for the `Department` table.
- **`name`**: A column to store the name of the department.

### **Employee Table**

| Column Name     | Data Type    | Constraints                  |
|-----------------|--------------|------------------------------|
| id              | BIGINT       | PRIMARY KEY, AUTO_INCREMENT  |
| name            | VARCHAR      | NOT NULL                     |
| department_id   | BIGINT       | FOREIGN KEY                  |

- **`id`**: The primary key for the `Employee` table.

- **`name`**: A column to store the name of the employee.

- **`department_id`**: A foreign key column that references the `id` column in the `Department` table. This establishes the many-to-one relationship between `Employee` and `Department`.

## Example of Table Content

Assume we have the following data in the `Department` and `Employee` entities:

- **Department**: { id: 1, name: "IT" }

- **Employees**:

  - { id: 101, name: "Alice", department_id: 1 }
  - { id: 102, name: "Bob", department_id: 1 }

### **Department Table**

| id | name   |
|----|--------|
|  1 | IT     |

### **Employee Table**

| id  | name  | department_id |
|-----|-------|---------------|
| 101 | Alice | 1             |
| 102 | Bob   | 1             |

## How They Work Together

- The `Employee` table’s `department_id` column references the `id` column in the `Department` table, establishing a foreign key relationship.
- This setup allows multiple `Employee` records to be associated with a single `Department`, enforcing the one-to-many relationship.

## Use Cases

- One-to-many relationships are commonly used in scenarios like departments and employees, orders and order items, or any parent-child relationship where one parent entity manages multiple child entities.

This relational structure helps in organizing the data in a way that reflects the real-world relationships between entities, ensuring integrity and consistency in the database.
