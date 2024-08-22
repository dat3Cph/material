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

1. Addition
2. Subtraction
3. Multiplication
4. Division
5. Modulus
6. Power

Implement the following methods that take either 2 integers or integer arrays and an `ArithmeticOperation` and return the result of the operation:

- `int operate(int a, int b, ArithmeticOperation op)`
- `int[] operate(int[] a, int[] b, ArithmeticOperation op)`

Hint: Check these explanations and examples on [lambda expressions](../../toolbox/java/deepdive/lambdas.md).

## 2. Functional Programming

2.1 Create a functional interface `MyTransformingType` that has a method that can take an integer and return another integer (transforming the first one in some way)

2.2 Create another functional interface `MyValidatingType` that has a method, that can take an integer and return a boolean (based on some kind of validation of the boolean, e.g. is it divisible by 3 or whatever).

2.3 Implement the following methods using lambda expressions:

Create the following 2 methods that use the functional interfaces, to perform map and filter operations on an array of integers:

- `int[] map(int[] a, MyTransformingType op)`
- `int[] filter(int[] a, MyValidatingType op)`

When running the above map and filter methods, you should provide them with an integer array and a lambda expression that performs the map or filter operation. For example, to double all the values in an array, you would call the map method like this: `map(myArray, (x) -> x * 2);`

## 3. Functional Interfaces

Now we will apply the functional interfaces from the `java.util.function` package: `Predicate`, `Consumer`, `Supplier`, `Function`:

3.1 Explain to your nabour what the following functional interfaces do: `Predicate`, `Consumer`, `Supplier`, `Function`.

3.2 Use `Predicate` to filter a list of integers, so only those divisible by 7 remain.

3.3 Use `Supplier` to create a list of Employee objects based on a list of names like `Arrays.asList("John", "Jane", "Jack", "Joe", "Jill")`.
Hint: Check these explanations and examples on [Supplier](./day-2-hints.md#supplier).

3.4 Use `Consumer` to print the list of Employee objects.

3.5 Use `Function` to convert a list of Employee objects to a list of names.

3.6 Use `Predicate`to check if a given employee is older than 18.

Check these hints for [explanations of the built-in functional interfaces](./day-2-hints.md).

## 4. Generics

In this exercise, you will create a generic data storage system using interfaces and classes. Your goal is to design a flexible solution that can store and retrieve data of various types while maintaining type safety.

4.1 **Create a Generic Storage Interface:**
Create a generic interface called `DataStorage<T>` that defines methods for storing and retrieving data of type `T`.

```java
interface DataStorage<T> {
    String store(T data); // return a unique ID for the stored data or the filename
    T retrieve(String source); // retrieve data from the specified source (like a file or database table or ID)
}
```

4.2 **Implement Storage Classes:**
Implement three classes that implement the `DataStorage` interface:

- `MemoryStorage<T>`: Stores data in memory.
- `FileStorage<T>`: Stores data in a file.
- `DatabaseStorage<T>`: Stores data in a database. (Only do this if you have time)

Implement the classes using appropriate data structures (e.g., instance variable, files, or database connections).

In the first instance, you can just use a String to store the data and retrieve it. If you have time, then your implementation should ensure type safety by only allowing data of the specified type to be stored and retrieved. Hint: See [this file](./day-2-hints.md#how-to-serialize-objects-in-java-and-write-them-to-a-file) for help on how to read and write objects to a file.

4.3 **Main Application:**

In the main application, create instances of each storage class and demonstrate their usage by storing and retrieving data of different types.

```java
public class DataStorageApp {
    public static void main(String[] args) {
        DataStorage<String> memoryStorage = new MemoryStorage<>();
        memoryStorage.store("Hello, world!");
        String retrievedString = memoryStorage.retrieve(null);

        DataStorage<Employee> fileStorage = new FileStorage<>();
        String filename = fileStorage.store(new Employee("John", 30));
        Employee retrievedInt = fileStorage.retrieve(filename);

        // Create and demonstrate DatabaseStorage
    }
}
```

This exercise will challenge you to design a generic solution that allows for the storage and retrieval of various types of data while maintaining type safety. It will also give you hands-on experience in working with generics in both interface declarations and class implementations.

## 5. Method References

The methods defined in Step 2 "Functional Programming" can be implemented using method references. Implement them using method references. E.g. Create a named method that doubles a value and use this method as a method reference: `MyTransformingType doubleValue = (x) -> x * 2;` in your map function.

Check these hints for [method references](../../toolbox/java/deepdive/functional_programming.md#method-references).

## 10. Bonus exercise (optional)

This is the same exercise as we did on day-1, but now we can use lambda expressions and streams to solve it and also
use the functional interfaces we have learned about (Predicate, Consumer, Supplier, Function).

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
