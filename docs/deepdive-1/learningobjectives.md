---
title: Learning Objectives
description: Java Deep Dive I Learning objectives
layout: default
nav_order: 1
has_children: false
parent: Java Deep Dive I
permalink: /deepdive-1/learning-objectives/
---

# Learning Objectives for Java 8 Deep Dive week

## Day 1

### 1. Understand and use Java 8 streams

1. **Understand the Concept and Purpose of Streams**: Learners should be able to explain what Java Streams are, the difference between streams and collections, and how streams support functional programming paradigms in Java for processing data more efficiently.

2. **Learn to Create and Use Streams**: Learners should be able to create streams from various data sources (e.g., collections, arrays, files) and understand the difference between intermediate operations (like `filter`, `map`) and terminal operations (like `collect`, `forEach`).

3. **Master Stream Operations for Data Manipulation**: Learners should be able to use stream operations such as `filter`, `map`, `reduce`, `flatMap`, `sorted`, and `distinct` to transform and manipulate data, understanding how each operation works and how to combine them effectively.

4. **Apply Streams in Real-World Scenarios**: Learners should be able to apply streams in practical coding scenarios, such as processing large datasets, performing complex data transformations, and refactoring traditional iterative code to use streams for improved readability and maintainability.

### 2. Understand and use Java Generics

1. **Understand the Purpose of Generics**: Learners should be able to explain why generics are used in Java, particularly how they help in writing type-safe code and reduce runtime errors by catching type mismatches at compile-time.

2. **Learn to Define and Use Generic Classes and Methods**: Learners should be able to define their own generic classes and methods, understanding how to create and utilize type parameters in these constructs.

3. **Master Bounded Type Parameters**: Learners should be able to use bounded type parameters (e.g., `<T extends Number>`) to restrict the types that can be passed to a generic class or method, and understand how to use wildcards (`? extends T`, `? super T`) to increase the flexibility of generics.

4. **Apply Generics in Common Data Structures**: Learners should be able to apply generics to commonly used Java data structures like `List`, `Set`, `Map`, etc., and understand the benefits and limitations of using generics with these collections.

### 3. Understand and use the Java 8 Date and Time API

1. **Understand the Need for the New Date and Time API**: Learners should be able to explain the limitations of the pre-Java 8 date and time handling (e.g., `java.util.Date` and `java.util.Calendar`) and how the new API, introduced in `java.time` package, addresses these issues with a more consistent and user-friendly approach.

2. **Learn to Work with LocalDate, LocalTime, and LocalDateTime**: Learners should be proficient in using the core classes `LocalDate`, `LocalTime`, and `LocalDateTime` for representing dates, times, and date-time combinations, respectively, and understand how to perform common operations like parsing, formatting, and manipulating these objects.

3. **Master the Use of ZonedDateTime and Time Zones**: Learners should be able to work with `ZonedDateTime` and related classes to handle date and time in different time zones, understanding how to convert between time zones and the significance of `ZoneId` and `ZoneOffset`.

4. **Understand Duration and Period for Time-based Calculations**: Learners should be familiar with the `Duration` and `Period` classes for representing and performing calculations involving spans of time, such as calculating the difference between two dates or times and adding or subtracting durations from date-time objects.

5. **Apply the DateTimeFormatter for Parsing and Formatting Dates and Times**: Learners should be able to use the `DateTimeFormatter` class to parse strings into date/time objects and format date/time objects into strings, understanding the various predefined formatters and how to create custom formatting patterns.

## Day 2

### 4. Understand and use functional Programming in Java

 1. **Understand the Fundamentals of Functional Programming**: Learners should grasp the core principles of functional programming, such as immutability, pure functions, higher-order functions, and how these principles contrast with imperative programming. They should understand why and when to use functional programming techniques in Java.

 2. **Master Lambda Expressions**: Learners should be proficient in writing and using lambda expressions to create concise, anonymous functions in Java. They should understand how lambdas can replace anonymous inner classes and how they contribute to more readable and maintainable code.

 3. **Explore Method References and Functional Interfaces**: Learners should be able to use method references to refer to methods in a more compact form and understand the concept of functional interfaces (e.g., `Predicate`, `Function`, `Supplier`, `Consumer`) that form the backbone of functional programming in Java.

 4. **Apply Stream API for Functional Data Processing**: Learners should be able to leverage the Stream API to process collections of data using functional programming techniques, such as filtering, mapping, and reducing data in a declarative manner.

 5. **Understand and Implement Functional Composition**: Learners should understand how to compose functions (combining multiple functions to form more complex operations), which is fundamental to writing clean and effective functional code.
