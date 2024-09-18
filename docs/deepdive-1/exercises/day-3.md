---
title: Day 3
description: Exercise for day 3
layout: default
nav_order: 4
parent: Exercises
grand_parent: Java Deep Dive I
permalink: /deepdive-1/exercises/day-3
---


# Day 3: Java Deep Dive Exercise

This exercise combines the concepts of generics, lambda expressions, streams, and dates. The exercise involves creating a simple task list application using Java. You'll need to implement classes to manage tasks, create a task list, and perform operations like filtering, sorting, and date-based calculations.

**Exercise: Task List Application**

Create a Java program that simulates a task list application. Follow these steps:

1. **Create the Task Class:**

   Create a `Task` class with the following attributes:
   - `title` (String): The title of the task.
   - `description` (String): The description of the task.
   - `dueDate` (LocalDate): The due date of the task.

2. **Create a GardenTask Class:**

   Create a `GardenTask` class that extends the `Task` class. The `GardenTask` class must have an additional attribute called `gardenLocation` (String) that stores the location of the garden where the task needs to be performed.

3. **Create the TaskList Class:**

   Create a `TaskList` class that manages a collection of Tasks (and GardenTasks). Include methods to:
   - Add tasks to the list.
   - Filter tasks based on a keyword in the title or description.
   - Sort tasks by due date.
   - Get tasks that are due today.
   - Get tasks that are overdue.
   - Print the list of tasks.

   The class must be generic and accept any Task or subtype of Task. The class must also implement the `Iterable` interface to allow iterating over the tasks.

4. **Main Application:**

   In the main application:
   - Create instances of `Task` and `GardenTask` and add them to a `TaskList`.
   - Demonstrate the usage of lambda expressions and streams for filtering and sorting tasks.
   - Use the Java Time API to set due dates and perform date-based calculations.
   - Print the resulting task lists after each operation.

This exercise will help you practice the following skills:

- Defining and using classes with generics (`Task`, `GardenTask` and `TaskList`).
- Using lambda expressions for filtering and sorting (`TaskList` methods).
- Utilizing streams to process collections (`TaskList` methods).
- Working with the Java Time API for handling dates (`Task` dueDate).
- Implementing various methods to perform operations on collections (`TaskList` methods).

4. **Background**

Using generics for your `Task` and `TaskList` classes can offer several benefits in terms of type safety, reusability, and flexibility. Let's explore the advantages of using generics in each of these classes:

**1. Type Safety:**

Using generics ensures that you can define the specific type of data each class will work with. This helps catch type-related errors at compile time rather than runtime, improving the overall reliability of your code. For example, by using generics, you can ensure that only `Task` objects are added to the `TaskList`, and any attempt to add other types of objects will result in a compile-time error.

**2. Reusability:**

Generics allow you to create more versatile and reusable classes. By parameterizing the classes with a type, you enable them to work with different data types while maintaining the same structure and behavior. This can make your code more adaptable to changes and easier to extend in the future.

**3. Flexibility:**

Using generics enables you to create classes that can work with different types without the need for duplicating code. For instance, you might want to create different `TaskList` instances that store tasks of different types, such as personal tasks and work-related tasks. With generics, you can achieve this flexibility without having to create separate classes for each type of task list.

**4. Avoiding Type Casting:**

Generics help eliminate the need for explicit type casting when retrieving objects from collections. In your `TaskList` class, when you use a generic type parameter for the task list, you won't need to cast elements to the appropriate type when retrieving them from the list.

Here's an example of how you might use generics in your `Task` and `TaskList` classes:

```java
import java.time.LocalDate;

class Task {
    private String title;
    private String description;
    private LocalDate dueDate;

    public Task(String title, String description, LocalDate dueDate) {
        this.title = title;
        this.description = description;
        this.dueDate = dueDate;
    }

    // ... getters and setters
}

class TaskList<T extends Task> {
    private List<T> tasks;

    public TaskList() {
        tasks = new ArrayList<>();
    }

    public void addTask(T task) {
        tasks.add(task);
    }

    public List<T> getTasks() {
        return tasks;
    }

    // ... other methods
}
```

In this example, the `TaskList` class is parameterized with a type `T` that extends the `Task` class. This ensures that the `TaskList` can only work with subclasses of `Task`, providing type safety and better organization of your code.

By using generics in your `Task` and `TaskList` classes, you can create more robust and flexible code that adheres to Java's type system and promotes cleaner, safer, and more reusable code.
