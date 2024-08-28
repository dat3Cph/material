---
title: JPQL Queries Exercise
description: jpql exercise
layout: default
nav_order: 1
parent: Exercises
grand_parent: JPA Part 1
permalink: /jpa-part-1/exercises/jpqlqueries/
---

# JPQL Queries

1. Create a new Java project using Maven.
2. Create `Employee` entity with the following attributes: `id`, `firstName`, `lastName`, `email`, `salary`
   and `department`.
3. Use JPA annotations to map the entity class to a database table named `employees`.
4. Add a constraint to the `email` attribute to ensure that the email address is unique.
5. Include appropriate annotations such as `@Entity`, `@Table`, `@Id`, `@GeneratedValue`, and `@Column` to define the
   primary key and attributes mapping.
6. Use the `Insert` SQL query below to add some data to the `employees` table.

```sql
INSERT INTO employee (id, firstName, lastName, department, salary, email)
VALUES (1, 'John', 'Doe', 'HR', 50000, 'john.doe@example.com'),
       (2, 'Jane', 'Smith', 'Finance', 60000, 'jane.smith@example.com'),
       (3, 'Michael', 'Johnson', 'IT', 70000, 'michael.johnson@example.com'),
       (4, 'Emily', 'Williams', 'Sales', 55000, 'emily.williams@example.com'),
       (5, 'Christopher', 'Brown', 'Marketing', 65000, 'christopher.brown@example.com'),
       (6, 'Amanda', 'Jones', 'HR', 48000, 'amanda.jones@example.com'),
       (7, 'David', 'Miller', 'IT', 72000, 'david.miller@example.com'),
       (8, 'Sarah', 'Wilson', 'Finance', 62000, 'sarah.wilson@example.com'),
       (9, 'Matthew', 'Taylor', 'Sales', 58000, 'matthew.taylor@example.com'),
       (10, 'Jennifer', 'Anderson', 'Marketing', 67000, 'jennifer.anderson@example.com');
```

Create a `Main.class` including a main method.
Create the following JPQL queries:

1. Write a JPQL query to select all employees.
2. Write a JPQL query to select employees with a salary greater than a certain value.
3. Write a JPQL query to select employees from a specific department.
4. Write a JPQL query to select employees whose first name starts with a certain letter.
5. Write a JPQL query to update the salary of an employee using a named parameter.
6. Write a JPQL query to update the department of an employee using positional parameters.
7. Write a JPQL query to calculate the average salary of all employees.
8. Write a JPQL query to calculate the total salary of all employees.
