## Day 2: Streams and Generics

## Streams
- Java streams provide several benefits that simplify and enhance the process of working with collections and processing data. Here are some key advantages of using java streams:
    - **readability and expressiveness:** streams enable you to express complex data transformations and processing in a more concise and readable manner. this leads to more maintainable and understandable code.
    - **declarative programming:** with streams, you focus on describing the operations you want to perform on the data, rather than how to perform them (**imperative programming**). this promotes a declarative programming style, making your code more intuitive. Explainer: (imperative code focuses on writing an explicit sequence of commands to describe how you want the computer to do things, and declarative code focuses on specifying the result of what you want)
    - **functional programming:** streams introduce functional programming concepts to java, such as immutability, first-class functions, and higher-order functions. this results in cleaner code that is easier to reason about and test.
    - **lazy evaluation:** streams use lazy evaluation, meaning that elements are processed only when needed. this can improve performance by avoiding unnecessary computations.
    - **parallelism:** streams can be easily parallelized, enabling concurrent processing of data on multi-core processors. this can lead to significant performance improvements for data-intensive tasks.
    - **method chaining:** streams support method chaining, allowing you to chain multiple operations together. this leads to more compact and fluent code.
    - **data aggregation:** streams provide various aggregation operations, such as sum, average, min, and max, which simplify common data summarization tasks.
    - **filtering and mapping:** streams offer operations like `filter` and `map` that make it easy to transform and filter data elements based on certain conditions.
    - **reduction:** streams support reduction operations, such as `reduce`, that allow you to combine elements of a collection into a single result.
    -  **no temporary collections:** many stream operations don't require intermediate collections. this can save memory and improve efficiency compared to traditional looping with collections.
    -  **focus on what, not how:** streams abstract away the looping and iteration details, allowing you to focus on the logic of what you want to achieve rather than the mechanics of how to achieve it.
    -  **easier debugging:** streams' fluent style of coding can make it easier to locate errors and debug issues, as each operation can be inspected individually.

In summary, java streams offer a more functional and declarative way to process data, leading to cleaner, more expressive, and potentially more performant code. they bring the benefits of functional programming to java collections, making it easier to write efficient, concise, and maintainable code for data manipulation and transformation.

### Creating streams: 
There are several ways to create streams in java. streams are created from various sources, such as collections, arrays, i/o channels, or even by generating elements using specific methods. here are the different ways to create streams:
1. **from a collection:**
   you can create a stream from a collection using the `stream()` method.

   ```java
   List<String> list = Arrays.asList("apple", "banana", "cherry");
   Stream<String> streamFromList = list.stream();
   ```
2. **from an array:**
   you can create a stream from an array using the `Arrays.stream()` method.

   ```java
   String[] array = {"one", "two", "three"};
   Stream<String> streamFromArray = Arrays.stream(array);
   ```
3. **from i/o channels:**
   you can create a stream from an i/o channel, like a file, using `Files.lines()`.

   ```java
   try (Stream<String> lines = Files.lines(Paths.get("file.txt"))) {
       // process each line
   } catch (IoException e) {
       e.printStacktrace();
   }
   ```
4. **using stream.of():**
   you can create a stream from individual elements using the `stream.of()` method.

   ```java
   Stream<String> streamOfElements = Stream.of("one", "two", "three");
   ```
5. **infinite streams:**
   you can create infinite streams using methods like `Stream.iterate()` and `Stream.generate()`.

   ```java
   Stream<Integer> infiniteStream = Stream.iterate(0, n -> n + 2); // generates even numbers
   ```
6. **using stream builder:**
   you can use the `Stream.builder()` to create a stream and add elements manually.

   ```java
   Stream.builder<String> streamBuilder = Stream.builder();
   streamBuilder.add("apple").add("banana").add("cherry");
   Stream<String> manualStream = streamBuilder.build();
   ```
7. **from intstream, longstream, and doublestream:**
   you can create specialized streams for primitive types.

   ```java
   IntStream intStream = IntStream.range(1, 6); // generates 1 to 5
   LongStream longStream = LongStream.rangeclosed(1, 5); // generates 1 to 5
   DoubleStream doubleStream = DoubleStream.of(1.0, 2.0, 3.0);
   ```

These are the primary ways to create streams in java. depending on your data sources and requirements, you can choose the appropriate method to create a stream and perform various operations on the data using the stream api.

### Common stream methods:
- **Intermediate and terminal operations** in streams.
    - common **intermediate operations**: `map`, `filter`, `flatmap`-(flattens nested stream into one single stream), `distinct`, `sorted`.
    - common **terminal operations**: `foreach`, `collect`, `reduce`, `count`, `anymatch`, `allmatch`, `nonematch`.
      - `min`, `max`, `findfirst`, `findany`, `anymatch`, `allmatch`, `nonematch`.
    - other operations on streams.
   - `peek`, `limit`, `skip`, `distinct`, `sorted`

## Collectors
- **Overview of collectors** and their role in stream operations.
  - `collectors` is a utility class in the java stream api that provides various predefined reduction operations (collectors) to accumulate elements from a stream into a collection, perform aggregations, and convert data into different formats. collectors are a powerful tool for efficiently collecting and processing data from streams.
  - built-in collectors: `toList`, `toSet`, `toMap`, `joining`, `groupingBy`, `partitioningBy`.
  code examples:

- **Collecting elements into a list:**
   ```java
   List<String> names = Stream.of("alice", "bob", "charlie")
       .collect(Collectors.tolist());
   ```

- **Collecting elements into a set:**
   ```java
   Set<Integer> numbers = Stream.of(1, 2, 3, 2, 4, 5)
       .collect(Collectors.toset());
   ```

- **Collecting elements into a map:**
   ```java
   Map<String, Integer> nameLengthMap = Stream.of("alice", "bob", "charlie")
       .collect(Collectors.toMap(name -> name, name -> name.length()));
   ```

- **Joining elements into a string:**
   ```java
   String joinedNames = Stream.of("alice", "bob", "charlie")
       .collect(Collectors.joining(", "));
   ```

- **Calculating sum, average, max, min, etc.:**
   ```java
   int sum = Stream.of(1, 2, 3, 4, 5)
       .collect(Collectors.summingInt(Integer::intvalue));
   
   double average = Stream.of(1, 2, 3, 4, 5)
       .collect(collectors.averagingint(Integer::intvalue));
   
   Optional<Integer> max = Stream.of(1, 2, 3, 4, 5)
       .collect(Collectors.maxby(Comparator.naturalorder()));
   ```

- **Grouping elements:**
   ```java
   Map<Character, List<String>> groupedNames = Stream.of("alice", "bob", "charlie")
       .collect(Collectors.groupingBy(name -> name.charAt(0)));
   ```

- **Partitioning elements:**
   ```java
   Map<Boolean, List<Integer>> evenOddPartition = Stream.of(1, 2, 3, 4, 5)
       .collect(Collectors.partitioningBy(num -> num % 2 == 0));
   ```

These are just a few examples of how you can use `collectors` to perform various operations on the elements of a stream and aggregate them into meaningful results. `collectors` greatly simplify the process of collecting data from streams and allow you to express complex transformations and aggregations in a concise and readable manner.

Creating custom collectors. you can create your own custom collectors by implementing the `collector` interface. custom collectors allow you to define specific accumulation logic tailored to your needs. here's an example of how you can create custom collectors:

Suppose you want to collect even and odd numbers separately into two different lists. here's how you could create a custom collector to achieve this:

```java
import java.util.Arraylist;
import java.util.Enumset;
import java.util.List;
import java.util.Set;
import java.util.stream.Collector;
import java.util.stream.Collectors;

public class CustomCollectorExample {
    public static void main(string[] args) {
        List<Integer> numbers = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        NumbersPartition partition = numbers.stream()
            .collect(new EvenOddPartitioningCollector());

        System.out.println("even numbers: " + partition.evennumbers);
        System.out.println("odd numbers: " + partition.oddnumbers);
    }
}

class NumbersPartition {
    List<Integer> evenNumbers = new ArrayList<>();
    List<Integer> oddNumbers = new ArrayList<>();
}

class EvenOddPartitioningCollector implements Collector<Integer, NumbersPartition, NumbersPartition> {
    @override
    public Supplier<Numberspartition> supplier() {
        return NumbersPartition::new;
    }

    @override
    public BiConsumer<NumbersPartition, Integer> accumulator() {
        return (partition, number) -> {
            if (number % 2 == 0) {
                Partition.evenNumbers.add(number);
            } else {
                Partition.oddNumbers.add(number);
            }
        };
    }

    @override
    public BinaryOperator<NumbersPartition> combiner() {
        return (left, right) -> {
            left.evenNumbers.addAll(right.evenNumbers);
            left.oddNumbers.addAll(right.oddNumbers);
            return left;
        };
    }

    @override
    public Function<NumbersPartition, NumbersPartition> finisher() {
        return partition -> partition;
    }

    @override
    public Set<Characteristics> characteristics() {
        return EnumSet.noneOf(Characteristics.class);
    }
}
```

In this example, the `evenoddpartitioningcollector` class implements the `collector` interface. it defines how elements are accumulated, combined, and transformed. the `numberspartition` class is used to hold the accumulated even and odd numbers. the collector can be used in the `collect()` operation to partition the numbers into even and odd lists.

This example demonstrates the process of creating a custom collector to handle a specific use case. custom collectors allow you to define complex accumulation strategies and are a powerful tool for customizing the behavior of your stream operations.

## New date and time api
- **Drawbacks of the old date and calendar apis.**
  - mutable state:
   both date and calendar were mutable classes, meaning that their internal state could be modified after creation. this made them prone to unexpected side effects and made it challenging to reason about the state of objects.
  - zero-based months:
   in the calendar api, months were represented using zero-based indexing. for example, january was represented as month 0, february as month 1, and so on. this was counterintuitive and led to confusion and mistakes in code.
  - lack of immutability:
   the date class was mutable, which made it challenging to ensure thread safety in multi-threaded environments.
- **java.time package:** 
  - LocalDate, 
  - LocalTime, 
  - LocalDateTime, 
  - Instant, 
  - Duration, 
  - Period.
- **Working with:**
  - **time zones** and 
  - **formatting dates**.


## Generics:
Generics in java provide a way to create classes, interfaces, and methods that operate on types specified as parameters. they offer several benefits and are essential for writing more reusable, type-safe, and flexible code. here are some reasons why we need generics in java:

### Introduction to generics:

**Type safety**: generics help catch type-related errors at compile-time rather than runtime. this ensures that you're using the correct types in a consistent manner, reducing the chances of bugs and runtime exceptions.
example (first without generics, then with generics):
```java
List myList = new ArrayList();
myList.add("hello");
Integer value = (Integer) myList.get(0); // runtime classcastexception
```
  - with generics:
```java
List<String> myList = new ArrayList<>();
myList.add("hello");
Integer value = myList.get(0); // compilation error
````

**Code reusability**: generics enable you to write classes, interfaces, and methods that can work with a variety of data types. this promotes code reuse, as a single implementation can cater to different types.

**Eliminate type casting**: generics eliminate the need for explicit type casting when retrieving elements from collections or working with other data structures. this leads to cleaner and more readable code.

**Stronger abstractions**: generics allow you to define abstractions that work with a range of types. this enables you to create more generic and flexible apis that can be used with different data types.

**Collections framework**: the java collections framework (e.g., list, set, map, etc.) heavily utilizes generics. it allows you to create collections that hold specific types of elements, improving type safety and eliminating casting.

### Generic classes and interfaces:
**defining and using generic classes in java**

Generic classes in java allow you to create classes that can work with different data types while maintaining type safety. they provide a powerful way to create reusable and flexible components that can operate seamlessly across various types. let´s explore how to define and use generic classes in java.

**Defining a generic class:**

to define a generic class, you use angle brackets (`<>`) to specify a type parameter. this type parameter acts as a placeholder for an actual data type that will be provided when an instance of the class is created. here's the basic syntax:

```java
public class MyGenericClass<T> {
    // class members and methods
}
```

In this example, `T` is the type parameter. it can be any valid java identifier, but by convention, single uppercase letters like `T` are often used. you can use this type parameter within the class just like any other type.

**Using a generic class:**

when you create an instance of a generic class, you provide the actual type argument that the type parameter will take. this binding of the type parameter to an actual type is called "parameterizing" the class. here's how you use a generic class:

```java
public class Main {
    public static void main(string[] args) {
        // parameterize mygenericclass with integer
        MyGenericClass<Integer> intObj = new MyGenericClass<>();
        
        // parameterize mygenericclass with string
        MyGenericClass<String> strObj = new MyGenericClass<>();
    }
}
```

**Example: generic box class**

here's a simple example of a generic class that represents a box that can hold any type of object:

```java
public class Box<T> {
    private T content;
    
    public void setContent(T content) {
        this.content = content;
    }
    
    public T getContent() {
        return content;
    }
    
    public static void main(String[] args) {
        Box<Integer> intBox = new Box<>();
        intBox.setContent(42);
        
        Box<String> strBox = new Box<>();
        strBox.setContent("hello, world!");
        
        System.out.println(intBox.getContent()); // output: 42
        System.out.println(strBox.getContent()); // output: hello, world!
    }
}
```

In this example, the `Box` class is defined with a type parameter `T`. instances of `Box` are created by specifying the actual type (e.g., `Integer`, `String`) when declaring the variable.

**Implementing generic interfaces in java**

generic interfaces allow you to create flexible and reusable contracts that can be implemented by various classes, accommodating different types while maintaining type safety. just like generic classes, generic interfaces enable you to design components that work with a wide range of data types. let's explore how to implement generic interfaces in java.

**Defining a generic interface:**

A generic interface is defined similarly to a regular interface, with the addition of type parameters enclosed in angle brackets (`<>`). these type parameters represent placeholders for actual types that will be provided when implementing the interface. here's the basic syntax:

```java
public interface MyGenericInterface<T> {
    // method signatures
}
```

In this example, `T` is the type parameter of the generic interface.

**Implementing a generic interface:**

When you implement a generic interface, you need to provide the actual type argument that matches the type parameter of the interface. this allows you to customize the interface methods to work with specific data types. here's how you implement a generic interface:

```java
public class MyImplementation<T> implements MyGenericInterface<T> {
    // implement interface methods
}
```

**Example: stack interface**

here's a practical example of a generic interface called `stack`, which represents a stack data structure. the interface defines methods to push, pop, and peek at elements in the stack:

```java
public interface Stack<T> {
    void push(T element);
    T pop();
    T peek();
}
```

Now, let's implement the `stack` interface with a class that uses a list to maintain the stack:

```java
import java.util.ArrayList;
import java.util.List;

public class ListStack<T> implements Stack<T> {
    private List<T> stackList = new ArrayList<>();

    @override
    public void push(T element) {
        stackList.add(element);
    }

    @override
    public T pop() {
        if (isEmpty()) {
            throw new IllegalStateException("stack is empty");
        }
        return stackList.remove(stackList.size() - 1);
    }

    @override
    public T peek() {
        if (isEmpty()) {
            throw new IllegalStateException("stack is empty");
        }
        return stackList.get(stackList.size() - 1);
    }

    public boolean isEmpty() {
        return stackList.isEmpty();
    }

    public static void main(string[] args) {
        stack<Integer> intStack = new ListStack<>();
        intStack.push(10);
        intStack.push(20);
        intStack.push(30);
        
        System.out.println(intStack.pop()); // output: 30
        System.out.println(intStack.peek()); // output: 20
    }
}
```

In this example, the `ListStack` class implements the `Stack` interface with a generic type parameter `T`. the class uses an `ArrayList` to manage the Stack. by implementing the `Stack` interface, the class ensures that it adheres to the stack contract for any type `T`.

### Type parameters and wildcards:
#### Type parameters in generic methods:
You can use type parameters in generic methods to create methods that work with multiple types. The type parameter is declared before the return type of the method. Here's an example:
```java
public class MyGenericMethods {
    public <T> void printArray(T[] array) {
        for (T element : array) {
            System.out.println(element);
        }
    }

    public static void main(String[] args) {
        Integer[] intArray = { 1, 2, 3 };
        String[] strArray = { "a", "b", "c" };

        MyGenericMethods genericMethods = new MyGenericMethods();
        genericMethods.printArray(intarray); // prints 1 2 3
        genericMethods.printarray(strarray); // prints a b c
    }
}
```

In this example, the printarray method is a generic method that can work with arrays of any type. the type parameter T is used to represent the element type of the array.

#### Unbounded wildcards, upper-bounded wildcards, lower-bounded wildcards
**Unbounded Wildcards, Upper-Bounded Wildcards, and Lower-Bounded Wildcards in Java Generics**

Wildcards in Java generics provide a way to write more flexible and versatile code when working with generic types. There are **three types** of wildcards: **unbounded wildcards**, **upper-bounded wildcards**, and **lower-bounded wildcards**. These wildcards allow you to work with generic types in a broader context while maintaining type safety. Let's explore each type:

**1. Unbounded Wildcards (`?`):**

Unbounded wildcards are represented by a question mark (`?`). They are used when you want to work with an unknown type and you're not concerned about the specific type. Unbounded wildcards are useful when you need to perform operations that don't depend on the actual type of the generic parameter.

```java
public void processList(List<?> list) {
    // Process the list without knowing its element type
}
```

**2. Upper-Bounded Wildcards (`? extends Type`):**

Upper-bounded wildcards are used when you want to work with a collection of objects that are of a specific type or a subtype of that type. They are represented using the `? extends Type` syntax.

```java
// Type or a subtype of Type
public double calculateTotal(List<? extends Number> numbers) {
    double total = 0;
    for (Number num : numbers) {
        total += num.doubleValue();
    }
    return total;
}
```

**3. Lower-Bounded Wildcards (`? super Type`):**

Lower-bounded wildcards are used when you want to work with a collection of objects that are of a specific type or a supertype of that type. They are represented using the `? super Type` syntax.

```java
// Type or a supertype of Type
public void addNumbers(List<? super Integer> numbers) {
    numbers.add(42);
}
```

**Advantages of Wildcards:**

1. **Flexibility:** Wildcards allow you to write methods and code that can work with a wide range of types, providing more flexibility and reusability.

2. **Avoid Type Casts:** Wildcards help you avoid type casting when working with collections of unknown types.

3. **Interoperability:** Wildcards enable better interoperability between different types that share a common hierarchy.

**Limitations:**

1. **Read-Only Access:** Unbounded and upper-bounded wildcards provide read-only access to the elements in the collection. You can't add elements to a collection with these wildcards.

2. **Write-Only Access:** Lower-bounded wildcards provide write-only access to the elements in the collection. You can't retrieve elements from a collection with this wildcard.

**Examples:**

Here are examples that demonstrate the use of each type of wildcard:

```java
public class WildcardExamples {
    public static void processList(List<?> list) {
        // Process the list without knowing its element type
    }
    
    public static double calculateTotal(List<? extends Number> numbers) {
        double total = 0;
        for (Number num : numbers) {
            total += num.doubleValue();
        }
        return total;
    }
    
    public static void addNumbers(List<? super Integer> numbers) {
        numbers.add(42);
    }
}
```
The limitations placed on wildcard types in Java generics are designed to prevent scenarios where type safety could be compromised. By enforcing read-only access or write-only access based on the type hierarchy, these limitations help maintain consistency and prevent runtime errors that could occur if incompatible elements were added or retrieved from collections


### Generics and method overloading:
- Handling method overloading with generic methods
- Resolving ambiguity in overloaded methods with type inference
```java
public class AmbiguityExample {

    // Overloaded method with non-generic parameter
    public void printValue(int value) {
        System.out.println("Non-generic method: " + value);
    }

    // Overloaded method with generic parameter
    public <T> void printValue(T value) {
        System.out.println("Generic method: " + value);
    }

    public static void main(String[] args) {
        AmbiguityExample example = new AmbiguityExample();
        example.printValue(42); // Ambiguity between the two methods
        example.printValue((int) 42); // Calls the non-generic method
        example.printValue("Hello"); // Calls the generic method (no problem)
    }
}
```
