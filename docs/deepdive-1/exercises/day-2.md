---
title: Day 2
description: Exercise for day 2
layout: default
nav_order: 3
parent: Exercises
grand_parent: Java Deep Dive I
permalink: /deepdive-1/exercises/day-2
---

# Day 2: Functional Programming and Lambda Expressions

## 1. Lambda Expressions

Based on the following functional interface:

```java
interface ArithmeticOperation {
    int perform(int a, int b);
}
```

Implement the following arithmetic operations using lambda expressions:

- Addition
- Subtraction
- Multiplication
- Division
- Modulus
- Power

Implement the following methods that take either 2 integers or integer arrays and an `ArithmeticOperation` and return the result of the operation:

- `int operate(int a, int b, ArithmeticOperation op)`
- `int[] operate(int[] a, int[] b, ArithmeticOperation op)`

Hint: Check these explanations and examples on [lambda expressions](../../toolbox/java/deepdive/lambdas).

## 2. Functional Programming

2.1 Create a functional interface `MyTransformingType` that has a method that can take an integer and return another integer (transforming the first one in some way)

2.2 Create another functional interface `MyValidatingType` that has a method, that can take an integer and return a boolean (based on some kind of validation of the boolean, e.g. is it divisible by 3 or whatever).

2.3 Implement the following methods using lambda expressions:

Create the following 2 methods that use the functional interfaces, to perform map and filter operations on an array of integers:

- `int[] map(int[] a, MyTransformingType op)`
- `int[] filter(int[] a, MyValidatingType op)`

When running the above map and filter methods, you should provide them with an integer array and a lambda expression that performs the map or filter operation. For example, to double all the values in an array, you would call the map method like this: `map(myArray, (x) -> x * 2);`

## 3. Functional Interfaces

Apply the functional interfaces from the `java.util.function` package: `Predicate`, `Consumer`, `Supplier`, `Function`:

3.1 Use `Predicate` to filter a list of integers, so only those divisible by 7 remain.

3.2 Use `Supplier` to create a list of Employee objects based on a list of names like `Arrays.asList("John", "Jane", "Jack", "Joe", "Jill")`.
Hint: Check these explanations and examples on [Supplier](.//day-2-hints.md#supplier).

3.3 Use `Consumer` to print the list of Employee objects.

3.4 Use `Function` to convert a list of Employee objects to a list of names.

3.5 Use `Predicate`to check if a given employee is older than 18.

Check these hints for [explanations of the built-in functional interfaces](./day-2-hints.md).

## 4. Time API

Add a birth date to the Employee class and implement the following tasks using the Java Time API:

4.1 Calculate the age of each employee based on their birthdate

4.2 Calculate the average age of all employees

4.3 Filter and display employees who have birthdays in a specific month.

4.4 Group employees by birth month and display the count of employees in each group.

4.5 List all employees who has a birthday in the current month.

Check these hints for [explanations of the date and time API in Java 8](../../toolbox/java/deepdive/datetime.md).

## 5. Method References

The methods defined in Step 2 "Functional Programming" can be implemented using method references. Implement them using method references. E.g. Create a named method that doubles a value and use this method as a method reference: `MyTransformingType doubleValue = (x) -> x * 2;` in your map function.

Check these hints for [method references](../../toolbox/java/deepdive/functional_programming.md#method-references).

## 10. Bonus exercise

Imagine you have a collection of **employees**, each with attributes like `name`, `age`, `department`, and `salary`. Your task is to perform various data analysis tasks using lambda expressions and streams.

1. Create the Employee Class:
2. Create an Employee class with attributes like name, age, department, and salary.
3. Data Collection:

- Create a collection of Employee objects to work with. You can either create a sample dataset or read data from a file or database.

4. Data Analysis:

- Implement the following tasks using lambda expressions and streams:
- Calculate the average age of all employees.
- Find the employee with the highest salary.
- Group employees by department and calculate the average salary for each department.
- Count the number of employees in each department.
- Find the three oldest employees.
- Filter and display employees whose salary is above a certain threshold.

5. Sorting:

- Use the `sorted` method to sort employees based on different criteria, such as `age`, `salary`, or `name`.

6. Custom Functional Interfaces:

- Define custom functional interfaces to represent various operations. For example, you could define an interface for filtering employees based on a certain condition.

7. Advanced Operations:

Implement more complex operations, such as:

- Combine multiple streams or operations.
- Transform data, such as calculating bonuses based on employee performance.
- Handle cases where some attributes might be missing (use `Optional` to handle null values).

This exercise will challenge your ability to work with lambda expressions, functional interfaces, and the Stream API in more complex scenarios. It also provides an opportunity to practice real-world data analysis tasks that often involve processing and transforming collections of data.
