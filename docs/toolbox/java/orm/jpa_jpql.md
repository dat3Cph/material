---
title: JPA JPQL
description: Many to Many relationship in JPA with extra attributes
layout: default
nav_order: 9
parent: ORM
grand_parent: Toolbox
permalink: /toolbox/java/jpa/jpql/
---

# JPA - JPQL examples

JPQL (Java Persistence Query Language) is a powerful query language in JPA that allows you to write queries using the entity model rather than the database tables. Below are examples of both typed and untyped JPQL queries.

### 1. **Basic JPQL Query (Untyped)**

**Example 1: Fetch all employees**

```java
String jpql = "SELECT e FROM Employee e";
Query query = entityManager.createQuery(jpql);
List employees = query.getResultList();
```

- **Explanation**:
  - This query selects all `Employee` entities from the database.
  - The result is returned as a raw `List` because the query is untyped.

### 2. **Basic JPQL Query (Typed)**

**Example 2: Fetch all employees (Typed)**

```java
String jpql = "SELECT e FROM Employee e";
TypedQuery<Employee> query = entityManager.createQuery(jpql, Employee.class);
List<Employee> employees = query.getResultList();
```

- **Explanation**:
  - Similar to the untyped query, but the `TypedQuery` interface is used to specify the type of the result (`Employee`).
  - This provides type safety, ensuring that the result list contains only `Employee` objects.

### 3. **JPQL Query with Parameters (Untyped)**

**Example 3: Fetch employees by department (Untyped)**

```java
String jpql = "SELECT e FROM Employee e WHERE e.department.name = :deptName";
Query query = entityManager.createQuery(jpql);
query.setParameter("deptName", "Sales");
List employees = query.getResultList();
```

- **Explanation**:
  - This query selects all `Employee` entities that belong to a department with the name "Sales".
  - The parameter `:deptName` is set using `setParameter`.

### 4. **JPQL Query with Parameters (Typed)**

**Example 4: Fetch employees by department (Typed)**

```java
String jpql = "SELECT e FROM Employee e WHERE e.department.name = :deptName";
TypedQuery<Employee> query = entityManager.createQuery(jpql, Employee.class);
query.setParameter("deptName", "Sales");
List<Employee> employees = query.getResultList();
```

- **Explanation**:
  - The same query as above but using a `TypedQuery` for type safety.
  - The result is a list of `Employee` objects.

### 5. **JPQL Query with Aggregate Functions (Untyped)**

**Example 5: Count the number of employees**

```java
String jpql = "SELECT COUNT(e) FROM Employee e";
Query query = entityManager.createQuery(jpql);
Long count = (Long) query.getSingleResult();
```

- **Explanation**:
  - This query counts the number of `Employee` entities in the database.
  - The result is cast to `Long` because the query returns a single result.

### 6. **JPQL Query with Aggregate Functions (Typed)**

**Example 6: Calculate average salary (Typed)**

```java
String jpql = "SELECT AVG(e.salary) FROM Employee e";
TypedQuery<Double> query = entityManager.createQuery(jpql, Double.class);
Double averageSalary = query.getSingleResult();
```

- **Explanation**:
  - This query calculates the average salary of all `Employee` entities.
  - The result is a single `Double` value.

### 7. **JPQL Query with Joins (Untyped)**

**Example 7: Fetch employees and their departments (Untyped)**

```java
String jpql = "SELECT e.name, d.name FROM Employee e JOIN e.department d";
Query query = entityManager.createQuery(jpql);
List<Object[]> results = query.getResultList();
for (Object[] result : results) {
    String employeeName = (String) result[0];
    String departmentName = (String) result[1];
    // Process results
}
```

- **Explanation**:
  - This query joins `Employee` entities with their corresponding `Department` entities and selects the names of both.
  - The result is a list of `Object[]`, where each element in the array corresponds to the selected fields.

### 8. **JPQL Query with Joins (Typed)**

**Example 8: Fetch employees and their departments (Typed)**

```java
String jpql = "SELECT new com.example.EmployeeDepartmentDTO(e.name, d.name) FROM Employee e JOIN e.department d";
TypedQuery<EmployeeDepartmentDTO> query = entityManager.createQuery(jpql, EmployeeDepartmentDTO.class);
List<EmployeeDepartmentDTO> results = query.getResultList();
```

- **Explanation**:
  - This query also joins `Employee` entities with their `Department` entities but uses a constructor expression to map the result to a `EmployeeDepartmentDTO` class.
  - The result is a list of `EmployeeDepartmentDTO` objects, providing a more structured and typed result.

### 9. **JPQL Query with Named Query (Untyped)**

**Example 9: Fetch employees by named query (Untyped)**

```java
@NamedQuery(name = "Employee.findByName", query = "SELECT e FROM Employee e WHERE e.name = :name")

// Later in code
Query query = entityManager.createNamedQuery("Employee.findByName");
query.setParameter("name", "Alice");
List employees = query.getResultList();
```

- **Explanation**:
  - The `@NamedQuery` annotation defines a named query at the entity level.
  - The query is executed using `createNamedQuery`.

### 10. **JPQL Query with Named Query (Typed)**

**Example 10: Fetch employees by named query (Typed)**

```java
@NamedQuery(name = "Employee.findByName", query = "SELECT e FROM Employee e WHERE e.name = :name")

// Later in code
TypedQuery<Employee> query = entityManager.createNamedQuery("Employee.findByName", Employee.class);
query.setParameter("name", "Alice");
List<Employee> employees = query.getResultList();
```

- **Explanation**:
  - Similar to the untyped named query, but using a `TypedQuery` to ensure the result is a list of `Employee` objects.

### Summary

- **Typed Queries** provide type safety and help avoid casting errors. They are generally preferred when you know the type of the results.
- **Untyped Queries** are more flexible but require casting the results to the appropriate type, which can lead to runtime errors if not handled carefully.

JPQL is a powerful way to interact with the database using a more object-oriented approach, and these examples cover some common use cases you might encounter.

For more advanced JPQL features and query patterns, refer to the [JPQL documentation](https://jakarta.ee/specifications/persistence/3.0/jakarta-persistence-spec-3.0.html#query-language).

## Constructor Expressions in JPQL

In JPQL, a constructor expression using the `new` keyword allows you to create and return objects of a specific class directly from the query results. This is particularly useful when you want to retrieve a subset of data from an entity and encapsulate it in a Data Transfer Object (DTO) or a custom class.

### Example Scenario

Let's say we have an `Employee` entity, and we want to retrieve a list of employees' names and their departments' names. Instead of returning the entire `Employee` and `Department` objects, we can use a constructor expression to return a list of `EmployeeDepartmentDTO` objects.

### Step-by-Step Example

#### 1. **Define the DTO Class**

First, create a DTO class that matches the fields you want to return from the query.

```java
public class EmployeeDepartmentDTO {

    private String employeeName;
    private String departmentName;

    // Constructor
    public EmployeeDepartmentDTO(String employeeName, String departmentName) {
        this.employeeName = employeeName;
        this.departmentName = departmentName;
    }

    // Getters and setters (optional)
    public String getEmployeeName() {
        return employeeName;
    }

    public String getDepartmentName() {
        return departmentName;
    }

    // toString method for easy display
    @Override
    public String toString() {
        return "EmployeeDepartmentDTO{" +
               "employeeName='" + employeeName + '\'' +
               ", departmentName='" + departmentName + '\'' +
               '}';
    }
}
```

#### 2. **Create the JPQL Query with Constructor Expression**

Now, write a JPQL query using the `new` keyword to create instances of `EmployeeDepartmentDTO` from the query results.

```java
String jpql = "SELECT new com.example.EmployeeDepartmentDTO(e.name, d.name) " +
              "FROM Employee e " +
              "JOIN e.department d";

TypedQuery<EmployeeDepartmentDTO> query = entityManager.createQuery(jpql, EmployeeDepartmentDTO.class);
List<EmployeeDepartmentDTO> results = query.getResultList();
```

#### 3. **Processing the Results**

Finally, process or display the results.

```java
for (EmployeeDepartmentDTO dto : results) {
    System.out.println(dto);
}
```

### Explanation

- **JPQL Query**:
  - The `new` keyword is used in the JPQL query to indicate that a new object of the specified class (`EmployeeDepartmentDTO`) should be created for each row returned by the query.
  - The query selects the employee's name (`e.name`) and the department's name (`d.name`) and passes them as arguments to the `EmployeeDepartmentDTO` constructor.

- **Typed Query**:
  - We use `TypedQuery<EmployeeDepartmentDTO>` to ensure that the query returns a list of `EmployeeDepartmentDTO` objects.
  
- **Result Processing**:
  - The result is a list of `EmployeeDepartmentDTO` objects, which can be iterated over and processed as needed.

### Example Output

If there are employees in the database with their respective departments, the output might look like this:

```
EmployeeDepartmentDTO{employeeName='Alice', departmentName='IT'}
EmployeeDepartmentDTO{employeeName='Bob', departmentName='HR'}
EmployeeDepartmentDTO{employeeName='Charlie', departmentName='Finance'}
```

### Summary

- **Constructor expressions** using `new` in JPQL are useful for returning non-entity objects like DTOs directly from queries.
- This approach reduces the amount of data retrieved from the database to only what is needed and allows for better encapsulation and separation of concerns in your application code.
