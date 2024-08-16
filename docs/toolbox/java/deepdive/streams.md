---
title: Streams
description: Streams in Java
layout: default
nav_order: 12
parent: Java
grand_parent: Toolbox
permalink: /toolbox/java/streams/
---

## Java Streams

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
  - **no temporary collections:** many stream operations don't require intermediate collections. this can save memory and improve efficiency compared to traditional looping with collections.
  - **focus on what, not how:** streams abstract away the looping and iteration details, allowing you to focus on the logic of what you want to achieve rather than the mechanics of how to achieve it.
  - **easier debugging:** streams' fluent style of coding can make it easier to locate errors and debug issues, as each operation can be inspected individually.

In summary, java streams offer a more functional and declarative way to process data, leading to cleaner, more expressive, and potentially more performant code. they bring the benefits of functional programming to java collections, making it easier to write efficient, concise, and maintainable code for data manipulation and transformation.

### Creating streams

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

4. **using Stream.of():**
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
Stream.Builder<String> streamBuilder = Stream.builder();
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

### Common stream methods

- **Intermediate and terminal operations** in streams.
  - common **intermediate operations**: `map`, `filter`, `flatmap`-(flattens nested stream into one single stream), `distinct`, `sorted`.
  - common **terminal operations**: `foreach`, `collect`, `reduce`, `count`, `anymatch`, `allmatch`, `nonematch`.
    - `min`, `max`, `findfirst`, `findany`, `anymatch`, `allmatch`, `nonematch`.
  - other operations on streams.
  - `peek`, `limit`, `skip`, `distinct`, `sorted`

### Examples

```java
// Intermediate methods: filter, map, flatMap, distinct, sorted, peek, limit, skip
List<String> words = Arrays.asList("apple", "banana", "apple", "cherry", "apricot", "banana");
List<String> processedWords = words.stream()
        .filter(word -> !word.startsWith("a")) // Filter out words starting with "a"
        .map(String::toUpperCase) // Transform to uppercase
        .distinct() // Remove duplicates
        .sorted() // Sort alphabetically
        .collect(Collectors.toList()); // Collect to list
System.out.println(processedWords);

// Terminal methods: forEach, collect, reduce, min, max, count, anyMatch, allMatch, noneMatch, findFirst, findAny
words.stream().forEach(System.out::println); // Print each element
int totalLengthOfWords = words.stream().map((word) -> word.length()).reduce(0, (subTotal, element) -> subTotal + element); // Calculate total length
System.out.println("Total length of words: " + totalLengthOfWords);
int countOfWords = (int) words.stream().count(); // Count number of words
System.out.println("Number of words: " + countOfWords);
Optional<String> firstWord = words.stream().findFirst(); // Find first word
System.out.println("First word: " + firstWord.get());
Optional<String> anyWord = words.stream().findAny(); // Find any word
System.out.println("Any word: " + anyWord.get());
```

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
                .collect(Collectors.summingInt(Integer::intValue));

        double average = Stream.of(1, 2, 3, 4, 5)
                .collect(Collectors.averagingInt(Integer::intValue));

        Optional<Integer> max = Stream.of(1, 2, 3, 4, 5)
                .collect(Collectors.maxBy(Comparator.naturalOrder()));
   ```

- **Grouping elements:**

   ```java
   Map<Character, List<String>> groupedNames = Stream.of("Alice", "Bob", "Charlie","Allan")
       .collect(Collectors.groupingBy(name -> name.charAt(0)));
   ```

- **Partitioning elements:**

   ```java
   Map<Boolean, List<Integer>> evenOddPartition = Stream.of(1, 2, 3, 4, 5)
       .collect(Collectors.partitioningBy(num -> num % 2 == 0));
   ```

These are just a few examples of how you can use `collectors` to perform various operations on the elements of a stream and aggregate them into meaningful results. `collectors` greatly simplify the process of collecting data from streams and allow you to express complex transformations and aggregations in a concise and readable manner.

### Custom Collectors (Optional extra)

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
