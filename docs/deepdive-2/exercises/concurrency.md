## 9. Concurrency

**Exercise: Concurrency with Java 8**

In this exercise, you'll work on a scenario involving multiple tasks running concurrently using the Java 8 Concurrency API. You'll use features like `CompletableFuture`, `ExecutorService`, and lambda expressions to manage parallel execution.

1. **Create a Task Class:**

   Create a simple `Task` class that simulates some computation. The class should have a `run()` method that performs the computation for a fixed time.

   ```java
   class Task {
       void run() {
           // Simulate some computation
           try {
               Thread.sleep(1000); // Simulate 1 second of work
           } catch (InterruptedException e) {
               e.printStackTrace();
           }
       }
   }
   ```

2. **Using CompletableFuture:**

   Use the `CompletableFuture` class to execute multiple tasks concurrently and wait for their completion.

   - Create several `CompletableFuture` instances, each running a `Task` asynchronously using the `runAsync()` method.
   - Use the `allOf()` method to wait for all `CompletableFuture` instances to complete.
   - Print a message indicating the completion of all tasks.

3. **Using ExecutorService:**

   Use the `ExecutorService` to manage a pool of threads and execute tasks concurrently.

   - Create an `ExecutorService` using `Executors.newFixedThreadPool()`.
   - Submit multiple `Task` instances to the executor using the `submit()` method.
   - Shutdown the executor using the `shutdown()` method after submitting tasks.
   - Print a message indicating the completion of all tasks.

4. **Exception Handling:**
Handle exceptions that might occur during task execution.

- Modify the `Task` class to throw an exception during computation.
- Handle the exceptions using `CompletableFuture.exceptionally()` and `ExecutorService.submit()`.

Here's a simplified example of what the code structure might look like:

```java
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

class Task {
    void run() {
        // Simulate some computation
        try {
            Thread.sleep(1000); // Simulate 1 second of work
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

public class ConcurrencyExercise {
    public static void main(String[] args) {
        // Using CompletableFuture
        CompletableFuture<Void> future1 = CompletableFuture.runAsync(() -> new Task().run());
        CompletableFuture<Void> future2 = CompletableFuture.runAsync(() -> new Task().run());

        CompletableFuture<Void> allFutures = CompletableFuture.allOf(future1, future2);
        allFutures.thenRun(() -> System.out.println("All CompletableFuture tasks completed."));

        // Using ExecutorService
        ExecutorService executorService = Executors.newFixedThreadPool(2);
        executorService.submit(() -> new Task().run());
        executorService.submit(() -> new Task().run());

        executorService.shutdown();
        System.out.println("All ExecutorService tasks submitted.");
    }
}
```

This exercise will give you hands-on experience with the Java 8 Concurrency API, helping you understand how to manage parallel execution of tasks and handle exceptions in a concurrent environment.
