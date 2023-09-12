# Day 1
## 1. Lambda
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

Hint: Check these explanations and examples on [lambda expressions](./Java8DeepDive.md#lambda-expressions).

## 2. Functional Programming

Implement the following methods using lambda expressions (First create the appropriate functional interfaces: `MyTransformingType` and `MyValidatingType`). You should provide each inteface with a single method that is appropriate for the task.

Create the following 2 methods that use the functional interfaces, to perform map and filter operations on an array of integers:

- `int[] map(int[] a, MyTransformingType op)`
- `int[] filter(int[] a, MyValidatingType op)`

When running the above map and filter methods, you should provide them with an integer array and a lambda expression that performs the map or filter operation. For example, to double all the values in an array, you would call the map method like this:

Check hints for how the [map](./ExerciseHints.md#the-map-function) and [filter](./ExerciseHints.md#the-filter-function) methods work.

## 3. Functional Interfaces

Apply the functional interfaces from the `java.util.function` package: `Predicate`, `Consumer`, `Supplier`, `Function`:

1. Use `Predicate` to filter a list of integers, so only those divisible by 3 remain.
2. Use `Supplier` to create a list of Employee objects based on a list of names like `Arrays.asList("John", "Jane", "Jack", "Joe", "Jill")`.
Hint: Check these explanations and examples on [Supplier](./ExerciseHints.md#supplier).
3. Use `Consumer` to print the list of Employee objects.
4. Use `Function` to convert a list of Employee objects to a list of names.
5. Use `Predicate`to check if a given employee is older than 18.

Check these hints for [explanations of the built-in functional interfaces](./Java8DeepDive.md#functional-interfaces).

## 4. Time API

Add a birth date to the Employee class and implement the following tasks using the Java Time API:

1. Calculate the age of each employee based on their birthdate
2. Calculate the average age of all employees
3. Filter and display employees who have birthdays in a specific month.
4. Group employees by birth month and display the count of employees in each group.
5. List all employees who has a birthday in the current month.

Check these hints for [explanations of the date and time API in Java 8](./JavaTimeAPI.md).

## 5. Method References

The methods defined in Step 2 "Functional Programming" can be implemented using method references. Implement them using method references.

Check these hints for [method references](./Java8DeepDive.md#method-references).

# Day 2

## 6. Streams API

In this exercise, you will work with a list of books and use the Stream API to perform various operations on the data.

1. **Create the Book Class:**
  - Create a `Book` class with attributes like title, author, publication year, and rating.
2. **Data Collection:**
  - Create a collection of `Book` objects to work with. You can either create a sample dataset or read data from a file or database.
3. **Stream Processing:**
  - Use the Stream API to perform the following operations on the list of books:
    - Find the average rating of all books.
    - Filter and display books published after a specific year.
    - Sort books by rating in descending order.
    - Find and display the title of the book with the highest rating.
    - Group books by author and calculate the average rating for each author's books.
    - Calculate the total number of pages for all books (assuming each book has a fixed number of pages).
4. **Chaining and Composition:**
  - Chain multiple Stream operations together to perform complex tasks, such as filtering and sorting.
5. **Collecting Results:**
- Use terminal operations like `collect`, `forEach`, or `reduce` to collect and display the results of your Stream operations.

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

## 7. Collectors
In Java, Collectors is a utility class provided by the java.util.stream package that offers various methods to perform reduction and aggregation operations on streams of data. Collectors are used in conjunction with the Stream API to collect elements from a stream into various data structures or perform aggregation operations like summing, grouping, counting, and more.

Collectors provide a convenient way to gather the results of stream operations and convert them into different formats, such as lists, sets, maps, or even custom data structures. They encapsulate the logic required for accumulating, transforming, and processing elements in a streamlined and efficient manner.

Here are some common tasks that can be achieved using collectors:

- Collecting Elements into a Collection:
  - Collectors.toList(): Collects elements into a List.
  - Collectors.toSet(): Collects elements into a Set.
  - Collectors.toCollection(): Collects elements into a specified collection type.

- Aggregations and Reductions:
  - Collectors.summingInt()/summingLong()/summingDouble(): Calculates the sum of elements.
  - Collectors.averagingInt()/averagingLong()/averagingDouble(): Calculates the average of elements.
  - Collectors.counting(): Counts the number of elements.
  - Collectors.maxBy()/minBy(): Finds the maximum or minimum element based on a specified comparator.

- Grouping Elements:
  - Collectors.groupingBy(): Groups elements by a specified classifier and returns a map.

1. **Create the Transaction Class:**
- Create a `Transaction` class with attributes like id, amount, and currency.
2. **Data Collection:**
- Create a collection of `Transaction` objects to work with. You can either create a sample dataset or read data from a file or database.
3. **Aggregation with Collectors:**
- Use the `Collectors` class to perform the following operations on the list of transactions:
   - Calculate the total sum of all transaction amounts.
   - Group transactions by currency and calculate the sum of amounts for each currency.
   - Find the highest transaction amount.
   - Find the average transaction amount.
4. **Collecting Results:**
- Use the `collect` method with different `Collectors` to aggregate and collect the results of your operations.

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
## 8. Generics
In this exercise, you will create a generic data storage system using interfaces and classes. Your goal is to design a flexible solution that can store and retrieve data of various types while maintaining type safety.

1. **Create a Generic Storage Interface:**
Create a generic interface called `DataStorage<T>` that defines methods for storing and retrieving data of type `T`.

```java
interface DataStorage<T> {
    void store(T data);
    T retrieve();
}
```

2. **Implement Storage Classes:**
Implement three classes that implement the `DataStorage` interface:

- `MemoryStorage<T>`: Stores data in memory.
- `FileStorage<T>`: Stores data in a file.
- `DatabaseStorage<T>`: Stores data in a database.

Implement these classes using appropriate data structures (e.g., lists, files, or database connections). Your implementation should ensure type safety by only allowing data of the specified type to be stored and retrieved.

3. **Main Application:**

In the main application, create instances of each storage class and demonstrate their usage by storing and retrieving data of different types.

```java
public class DataStorageApp {
    public static void main(String[] args) {
        DataStorage<String> memoryStorage = new MemoryStorage<>();
        memoryStorage.store("Hello, world!");
        String retrievedString = memoryStorage.retrieve();

        DataStorage<Employee> fileStorage = new FileStorage<>("data.txt");
        fileStorage.store(new Employee("John", 30));
        Employee retrievedInt = fileStorage.retrieve();

        // Create and demonstrate DatabaseStorage
    }
}
```

This exercise will challenge you to design a generic solution that allows for the storage and retrieval of various types of data while maintaining type safety. It will also give you hands-on experience in working with generics in both interface declarations and class implementations.

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

# Summary
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
- Use the sorted method to sort employees based on different criteria, such as age, salary, or name.
6. Custom Functional Interfaces:
- Define custom functional interfaces to represent various operations. For example, you could define an interface for filtering employees based on a certain condition.
7. Advanced Operations:
- Implement more complex operations, such as:
  - Combine multiple streams or operations.
  - Transform data, such as calculating bonuses based on employee performance.
  - Handle cases where some attributes might be missing (use Optional to handle null values).

This exercise will challenge your ability to work with lambda expressions, functional interfaces, and the Stream API in more complex scenarios. It also provides an opportunity to practice real-world data analysis tasks that often involve processing and transforming collections of data.
