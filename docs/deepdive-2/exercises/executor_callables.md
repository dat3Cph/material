---
title: Executor and Callables
description: Java Deep Dive II Exercise on executors and callables
layout: default
nav_order: 7
has_children: false
grand_parent: Java Deep Dive II
parent: Exercises
permalink: /deepdive-2/exercises/executors-callables/
---
# Executor and Callables Exercise

This exercise is about using the `ExecutorService` and `Callable` classes. It's a little example to learn from. The problem we want to solve is to have more tasks running at the same time. We will use the `ExecutorService` to manage the tasks and the `Callable` interface to create the tasks. The `Callable` interface is similar to the `Runnable` interface, but it can return a result and throw a checked exception. That makes it suitable for returning a json result from an API etc.

## Code along - and make it your own

Here's an example in Java using **`Callable`**, **`Future`**, and **`ExecutorService`**. We'll create three tasks using `Callable` that return a `String`. We submit these tasks to an `ExecutorService`, gather the resulting `Future` objects into a list, and then wait until all tasks are done before looping over the `Future`s to print the results.

Create a simple Java program with the following code and run it in IntelliJ. Try to understand how it works and then modify it to fit your needs.

### Example Code

```java
import java.util.List;
import java.util.concurrent.*;

public class CallableFutureExample {
    public static void runTasks() {
        // Create a fixed thread pool with 3 threads
        ExecutorService executor = Executors.newFixedThreadPool(3);

        // Create 3 Callable tasks and submit them to the executor
        Callable<String> task1 = () -> {
            TimeUnit.SECONDS.sleep(1); // Sleep for taskId seconds
            return "Task " + 1 + " completed";
        };

        Callable<String> task2 = () -> {
            TimeUnit.SECONDS.sleep(2); // Sleep for taskId seconds
            return "Task " + 2 + " completed";
        };

        Callable<String> task3 = () -> {
            TimeUnit.SECONDS.sleep(3); // Sleep for taskId seconds
            return "Task " + 3 + " completed";
        };

        // Submit the task and add the Future to the list

        List<Future<String>> futures = null;
        try {
            futures = executor.invokeAll(List.of(task1, task2, task3));
        }
        catch (InterruptedException e) {
            throw new RuntimeException(e);
        }

        // Wait for all tasks to complete and retrieve their results
        for (Future<String> future : futures) {
            try {
                // get() blocks until the result is available
                String result = future.get();
                System.out.println(result);
            }
            catch (InterruptedException | ExecutionException e) {
                e.printStackTrace();
            }
        }

        // Shut down the executor service
        executor.shutdown();
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        // Record the start time
        long startTime = System.currentTimeMillis();

        CallableFutureExample.runTasks();

        long endTime = System.currentTimeMillis();
        long duration = endTime - startTime;
        System.out.println("Task runtime: " + duration + " milliseconds");
    }
}
```

### Explanation

This code demonstrates how to execute multiple **asynchronous tasks** using the **`Callable`** interface and **`Future`** objects in conjunction with an **`ExecutorService`**. Here's an explanation of each section of the code:

### 1. **Imports**

```java
import java.util.List;
import java.util.concurrent.*;
```

- **`java.util.List`**: This is for handling lists of `Future` objects, which represent the results of asynchronous tasks.
- **`java.util.concurrent.*`**: This imports classes from the `java.util.concurrent` package, including `Callable`, `ExecutorService`, `Executors`, `TimeUnit`, and `Future`.

### 2. **runTasks Method**

This method demonstrates how to create a fixed thread pool with `ExecutorService`, submit multiple `Callable` tasks, and retrieve their results using `Future`.

### 3. **Creating a Thread Pool**

```java
ExecutorService executor = Executors.newFixedThreadPool(3);
```

- The **`ExecutorService`** is created with a fixed thread pool of 3 threads using `Executors.newFixedThreadPool(3)`. This pool can run up to 3 tasks concurrently.

### 4. **Creating Callable Tasks**

```java
Callable<String> task1 = () -> {
    TimeUnit.SECONDS.sleep(1);
    return "Task " + 1 + " completed";
};

Callable<String> task2 = () -> {
    TimeUnit.SECONDS.sleep(2);
    return "Task " + 2 + " completed";
};

Callable<String> task3 = () -> {
    TimeUnit.SECONDS.sleep(3);
    return "Task " + 3 + " completed";
};
```

- Three **`Callable<String>`** tasks are defined using lambda expressions. Each task sleeps for a certain number of seconds (`1`, `2`, and `3` seconds) to simulate work, and then returns a completion message (e.g., `"Task 1 completed"`).
- **`Callable`** is similar to `Runnable`, but it can return a result (in this case, a `String`).

### 5. **Submitting Tasks with `invokeAll`**

```java
futures = executor.invokeAll(List.of(task1, task2, task3));
```

- **`invokeAll()`**: This method is used to submit a collection of `Callable` tasks (`task1`, `task2`, `task3`) to the executor service. It returns a `List<Future<String>>`, where each `Future` corresponds to a task and allows you to retrieve its result.
- **Blocking Behavior**: The `invokeAll` method **blocks** until all tasks are finished. This means the main thread will wait for all three tasks to complete.

### 6. **Retrieving Results from Futures**

```java
for (Future<String> future : futures) {
    try {
        String result = future.get();
        System.out.println(result);
    }
    catch (InterruptedException | ExecutionException e) {
        e.printStackTrace();
    }
}
```

- For each `Future<String>` in the `futures` list, the `get()` method is called to retrieve the result of the corresponding `Callable` task.
- **`get()`**: Blocks until the task is completed and the result is available.
- **Error Handling**: `get()` can throw `InterruptedException` (if the current thread is interrupted while waiting) or `ExecutionException` (if the task throws an exception during execution), so these exceptions are caught and handled.

### 7. **Shutting Down the Executor**

```java
executor.shutdown();
```

- **`shutdown()`**: Initiates an orderly shutdown of the executor service, meaning no new tasks will be accepted, but previously submitted tasks will continue to be executed.

### Full Execution Flow

1. Three tasks (`task1`, `task2`, `task3`) are created, each simulating work by sleeping for `1`, `2`, and `3` seconds, respectively.
2. The tasks are submitted to the `ExecutorService` using `invokeAll()`, which waits for all tasks to complete.
3. Once all tasks finish, their results are printed to the console using `Future.get()`.
4. The executor is gracefully shut down after all tasks are complete.

### Example Output

```
Task 1 completed
Task 2 completed
Task 3 completed
```

The tasks complete in the order of their sleep durations. The first task (1-second sleep) completes first, followed by the second (2-second sleep), and finally the third (3-second sleep).

### Benefits of this Approach

- **Efficient Task Management**: By using a fixed thread pool, the system can manage the number of concurrent threads efficiently.
- **Simplified Handling of Asynchronous Tasks**: With `Callable` and `Future`, you can manage asynchronous tasks that return values and easily retrieve their results once they finish.
- **Blocking Behavior Control**: `invokeAll()` ensures that the main thread waits for all tasks to complete before moving on, allowing for sequential result processing.
