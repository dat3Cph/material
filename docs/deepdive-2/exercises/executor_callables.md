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
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.*;

public class CallableFutureExample {
    public static void runTasks() {
        // Create a fixed thread pool with 3 threads
        ExecutorService executor = Executors.newFixedThreadPool(3);

        // Create a list to hold the Future objects
        List<Future<String>> futures = new ArrayList<>();

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
        Future<String> future = executor.submit(task1);
        futures.add(future);
        futures.add(executor.submit(task2));
        futures.add(executor.submit(task3));
        
        // Wait for all tasks to complete and retrieve their results
        for (Future<String> fut : futures) {
            try {
                // get() blocks until the result is available
                String result = fut.get();
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

### Explanation

1. **ExecutorService**: We use a fixed thread pool with 3 threads to execute the tasks concurrently.
2. **Callable**: Each task is represented by a `Callable<String>` which returns a `String`. The `Callable` simulates some work (sleeping for a number of seconds based on the task ID) and then returns a message indicating the task is complete.
3. **Future**: After submitting each task, we store the `Future<String>` object in a list. The `Future` allows us to retrieve the result of the task later, once it is done.
4. **Waiting for Completion**: We loop through the list of futures and call `future.get()`, which blocks until the task is complete. Once the task is complete, we print the result.
5. **Shutdown**: After all tasks are complete, we shut down the executor.

### Output (Example)

```plaintext
Task 1 completed
Task 2 completed
Task 3 completed
```

### Notes

- The `get()` method on a `Future` blocks until the task has completed, ensuring that we wait for each task to finish before printing its result.
- The tasks are executed concurrently, but because they sleep for `taskId` seconds, the tasks finish in increasing order (Task 1, Task 2, Task 3) based on their sleep durations.
