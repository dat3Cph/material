---
title: Day 1
description: Exercise for day 1
layout: default
nav_order: 1
parent: Exercises
grand_parent: Java Deep Dive I
permalink: /deepdive-1/exercises/day-1
---

# Day 1: Exercises

## 1. Streams API Basics

In this exercise, you will work with a list of books and use the Stream API to perform various operations on the data.

1.1 **Create the Book Class:**

Create a `Book` class with attributes like title, author, publication year, pages and rating.

1.2 **Data Collection:**

Create a collection of `Book` objects to work with. You can either create a sample dataset or read data from a file or database.

1.3 **Stream Processing:**

- Use the Stream API to perform the following operations on the collection of books:
  - Find the average rating of all books.
  - Filter and display books published after a specific year.
  - Sort books by rating in descending order.
  - Find and display the title of the book with the highest rating.
  - Group books by author and calculate the average rating for each author's books.
  - Calculate the total number of pages for all books (assuming each book has a fixed number of pages).

1.4 **Chaining and Composition:**

Chain multiple Stream operations together to perform complex tasks, such as filtering and sorting.

1.5 **Collecting Results:**

Use terminal operations like `collect`, `forEach`, or `reduce` to collect and display the results of your Stream operations.

Here's a simplified example of what the code structure might look like:

```java
import java.util.List;

class Book {
    private String title;
    private String author;
    private int publicationYear;
    private double rating;
    private int pages;

    // Constructor, getters, and setters
}

public class StreamProcessing {
    public static void main(String[] args) {
        // Create a list of books
        
        // Calculate the average rating of all books
        
        // Filter and display books published after a specific year
        
        // Sort books by rating in descending order
        
        // Find and display the title of the highest-rated book
        
        // Group books by author and calculate average rating for each author
        
        // Calculate the total number of pages for all books
    }
}
```

## 2. Collectors

In Java, Collectors is a utility class provided by the java.util.stream package that offers various methods to perform reduction and aggregation operations on streams of data. Collectors are used in conjunction with the Stream API to collect elements from a stream into various data structures or perform aggregation operations like summing, grouping, counting, and more.

Collectors provide a convenient way to gather the results of stream operations and convert them into different formats, such as lists, sets, maps, or even custom data structures. They encapsulate the logic required for accumulating, transforming, and processing elements in a streamlined and efficient manner.

Here are some common tasks that can be achieved using collectors:

### Collecting Elements into a Collection

- Collectors.toList(): Collects elements into a List.
- Collectors.toSet(): Collects elements into a Set.
- Collectors.toCollection(): Collects elements into a specified collection type.

### Aggregations and Reductions

- `Collectors.summingInt()`,  `summingLong()`,  `summingDouble()`: Calculates the sum of elements.
- `Collectors.averagingInt()`, `averagingLong()`, `averagingDouble()`: Calculates the average of elements.
- `Collectors.counting()`: Counts the number of elements.
- `Collectors.maxBy()`, `minBy()`: Finds the maximum or minimum element based on a specified comparator.

### Grouping Elements

Collectors.groupingBy(): Groups elements by a specified classifier and returns a map.

2.1 **Create the Transaction Class:**

Create a `Transaction` class with attributes like id, amount, and currency.

2.2 **Data Collection:**

Create a collection of `Transaction` objects to work with. You can either create a sample dataset or read data from a file or database.

2.3 **Aggregation with Collectors:**

Use the `Collectors` class to perform the following operations on the list of transactions:

- Calculate the total sum of all transaction amounts.
- Group transactions by currency and calculate the sum of amounts for each currency.
- Find the highest transaction amount.
- Find the average transaction amount.

2.4 **Collecting Results:**

Use the `collect` method with different `Collectors` to aggregate and collect the results of your operations.

Here's a simplified example of what the code structure might look like:

```java
import java.util.List;

class Transaction {
    private int id;
    private double amount;
    private String currency;

    public Transaction(int id, double amount, String currency) {
        this.id = id;
        this.amount = amount;
        this.currency = currency;
    }

    public double getAmount() {
        return amount;
    }

    public String getCurrency() {
        return currency;
    }
}

public class CollectorsExercise {
    public static void main(String[] args) {
        List<Transaction> transactions = List.of(
            new Transaction(1, 100.0, "USD"),
            new Transaction(2, 150.0, "EUR"),
            new Transaction(3, 200.0, "USD"),
            new Transaction(4, 75.0, "GBP"),
            new Transaction(5, 120.0, "EUR"),
            new Transaction(6, 300.0, "GBP")
        );
        
        // Calculate the total sum of all transaction amounts
        double totalSum = transactions.stream()
                .mapToDouble(Transaction::getAmount)
                .sum();
        System.out.println("Total sum of all transactions: " + totalSum);
        
        // Group transactions by currency and calculate sum for each currency
        
        // Find the highest transaction amount
        
        // Find the average transaction amount
    }
}
```

## 3. Generics

In this exercise, you will create a generic data storage system using interfaces and classes. Your goal is to design a flexible solution that can store and retrieve data of various types while maintaining type safety.

3.1 **Create a Generic Storage Interface:**
Create a generic interface called `DataStorage<T>` that defines methods for storing and retrieving data of type `T`.

```java
interface DataStorage<T> {
    String store(T data); // return a unique ID for the stored data or the filename
    T retrieve(String source); // retrieve data from the specified source (like a file or database table or ID)
}
```

3.2 **Implement Storage Classes:**
Implement three classes that implement the `DataStorage` interface:

- `MemoryStorage<T>`: Stores data in memory.
- `FileStorage<T>`: Stores data in a file.
- `DatabaseStorage<T>`: Stores data in a database. (Only do this if you have time)

Implement the classes using appropriate data structures (e.g., instance variable, files, or database connections).

In the first instance, you can just use a String to store the data and retrieve it. If you have time, then your implementation should ensure type safety by only allowing data of the specified type to be stored and retrieved. Hint: See [this file](SerializeObjects.md) for help on how to read and write objects to a file.

3.3 **Main Application:**

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

## 4. Bonus exercise

Imagine you have a collection of **employees**, each with attributes like `name`, `age`, `department`, and `salary`. Your task is to perform various data analysis tasks using lambda expressions and streams.

4.1 Create the Employee Class:
4.2 Create an Employee class with attributes like name, age, department, and salary.
4.3 Data Collection:

- Create a collection of Employee objects to work with. You can either create a sample dataset or read data from a file or database.

4.4 Data Analysis:

- Implement the following tasks using lambda expressions and streams:
- Calculate the average age of all employees.
- Find the employee with the highest salary.
- Group employees by department and calculate the average salary for each department.
- Count the number of employees in each department.
- Find the three oldest employees.
- Filter and display employees whose salary is above a certain threshold.

4.5 Sorting:

- Use the `sorted` method to sort employees based on different criteria, such as `age`, `salary`, or `name`.

4.6 Custom Functional Interfaces:

- Define custom functional interfaces to represent various operations. For example, you could define an interface for filtering employees based on a certain condition.

4.7 Advanced Operations:

Implement more complex operations, such as:

- Combine multiple streams or operations.
- Transform data, such as calculating bonuses based on employee performance.
- Handle cases where some attributes might be missing (use `Optional` to handle null values).

This exercise will challenge your ability to work with lambda expressions, functional interfaces, and the Stream API in more complex scenarios. It also provides an opportunity to practice real-world data analysis tasks that often involve processing and transforming collections of data.
