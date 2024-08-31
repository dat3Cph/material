---
title: Tester Exercise
description: tester exercise
layout: default
nav_order: 1
parent: Exercises
grand_parent: JPA Part 2
permalink: part2/exercises/tester/
---

# Tester Exercise (JPQL)

### 1. Create a new JPA project using Maven.

### 2. Create a new package called `model` and `dao`.

### 3. In the model package create a new entity class called `Employee` and add the following code to the class:

```java
    @Id
    @Column(name = "id", nullable = false, length = 6)
    private String id;

    @Column(name = "firstname", nullable = false)
    private String firstName;

    @Column(name = "lastname", nullable = false)
    private String lastName;

    @Column(name = "salary", nullable = false)
    private BigDecimal salary;

    public Employee(String id, String firstName, String lastName, BigDecimal salary) {
        this.id = id;
        this.firstName = firstName;
        this.lastName = lastName;
        this.salary = salary;
    }
```

**Remember to add the necessary annotations to the class.**

### 4. In the `dao` package add a new interface called `EmployeeDAO` and add the following code to the interface:

```java
public interface IEmployeeDAO {
    // fetch all employees with a salary > 100000 and return a list of their salaries
    List<BigDecimal> fetchAllEmployeesWithSalaryGreaterThan100000();

    // fetch the employee with the id "klo999" and return the employee's firstName
    String fetchEmployeeWithIdKlo999();

    // fetch the highest salary and return the value
    double fetchHighestSalary();

    // fetch the firstName of all Employees and return a List of all employees full names
    List<String> fetchFirstNameOfAllEmployees();

    // calculate the number of employees and return the number
    long calculateNumberOfEmployees();

    // fetch the Employee with the highest salary and return all his details
    Employee fetchEmployeeWithHighestSalary();
}
```

### 5. At the same location add a new class called `EmployeeDAOImpl` and implement the interface to the class with all the methods.

### 6. In the root of the project add a new class called `Populate` and add the following code to the class:

```java
public class Populate {

    private static final EntityManagerFactory emf = HibernateConfig.getEntityManagerFactoryConfig();

    public static void main(String[] args) {
        try(var em = emf.createEntityManager()) {
            em.getTransaction().begin();
            em.persist(new Employee("xa12tt", "Kurt", "Wonnegut", new BigDecimal(335567)));
            em.persist(new Employee("hyu654", "Hanne", "Olsen", new BigDecimal(435867)));
            em.persist(new Employee("uio876", "Jan", "Olsen", new BigDecimal(411567)));
            em.persist(new Employee("klo999", "Irene", "Petersen", new BigDecimal(33567)));
            em.persist(new Employee("jik666", "Tian", "Wonnegut", new BigDecimal(56567)));
            em.getTransaction().commit();
        }
    }

}
```

### 7. Run the `main` method in the Populate class to populate the database with the employees.

### 8. All the methods in the `EmployeeDAOImpl` class should now be implemented using JPQL.

### 9. Create a test class with a test method for each of the methods in the `EmployeeDAOImpl` class.

### 10. Implement and run the test class and verify that all tests pass.

**Good luck!**
