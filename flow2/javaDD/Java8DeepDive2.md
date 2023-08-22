## day 2: streams and generics

## streams
- introduction to streams and their benefits.

- java streams provide several benefits that simplify and enhance the process of working with collections and processing data. here are some key advantages of using java streams:

  - **readability and expressiveness:** streams enable you to express complex data transformations and processing in a more concise and readable manner. this leads to more maintainable and understandable code.
  - **declarative programming:** with streams, you focus on describing the operations you want to perform on the data, rather than how to perform them. this promotes a declarative programming style, making your code more intuitive.
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

in summary, java streams offer a more functional and declarative way to process data, leading to cleaner, more expressive, and potentially more performant code. they bring the benefits of functional programming to java collections, making it easier to write efficient, concise, and maintainable code for data manipulation and transformation.

2. creating streams: there are several ways to create streams in java. streams are created from various sources, such as collections, arrays, i/o channels, or even by generating elements using specific methods. here are the different ways to create streams:

1. **from a collection:**
   you can create a stream from a collection using the `stream()` method.

   ```java
   list<string> list = arrays.aslist("apple", "banana", "cherry");
   stream<string> streamfromlist = list.stream();
   ```

2. **from an array:**
   you can create a stream from an array using the `arrays.stream()` method.

   ```java
   string[] array = {"one", "two", "three"};
   stream<string> streamfromarray = arrays.stream(array);
   ```

3. **from i/o channels:**
   you can create a stream from an i/o channel, like a file, using `files.lines()`.

   ```java
   try (stream<string> lines = files.lines(paths.get("file.txt"))) {
       // process each line
   } catch (ioexception e) {
       e.printstacktrace();
   }
   ```

4. **using stream.of():**
   you can create a stream from individual elements using the `stream.of()` method.

   ```java
   stream<string> streamofelements = stream.of("one", "two", "three");
   ```

5. **infinite streams:**
   you can create infinite streams using methods like `stream.iterate()` and `stream.generate()`.

   ```java
   stream<integer> infinitestream = stream.iterate(0, n -> n + 2); // generates even numbers
   ```

6. **using stream builder:**
   you can use the `stream.builder()` to create a stream and add elements manually.

   ```java
   stream.builder<string> streambuilder = stream.builder();
   streambuilder.add("apple").add("banana").add("cherry");
   stream<string> manualstream = streambuilder.build();
   ```

7. **from intstream, longstream, and doublestream:**
   you can create specialized streams for primitive types.

   ```java
   intstream intstream = intstream.range(1, 6); // generates 1 to 5
   longstream longstream = longstream.rangeclosed(1, 5); // generates 1 to 5
   doublestream doublestream = doublestream.of(1.0, 2.0, 3.0);
   ```

these are the primary ways to create streams in java. depending on your data sources and requirements, you can choose the appropriate method to create a stream and perform various operations on the data using the stream api.
3. common stream methods:
  - intermediate and terminal operations in streams.
      - common **intermediate operations**: `map`, `filter`, `flatmap`-(flattens nested stream into one single stream), `distinct`, `sorted`.
      - common **terminal operations**: `foreach`, `collect`, `reduce`, `count`, `anymatch`, `allmatch`, `nonematch`.
      - `min`, `max`, `findfirst`, `findany`, `anymatch`, `allmatch`, `nonematch`.
2. other operations on streams.
   - `peek`, `limit`, `skip`, `distinct`, `sorted`

## collectors
6. overview of collectors and their role in stream operations.
  - `collectors` is a utility class in the java stream api that provides various predefined reduction operations (collectors) to accumulate elements from a stream into a collection, perform aggregations, and convert data into different formats. collectors are a powerful tool for efficiently collecting and processing data from streams.
  - built-in collectors: `tolist`, `toset`, `tomap`, `joining`, `groupingby`, `partitioningby`.
  code examples:

1. **collecting elements into a list:**
   ```java
   list<string> names = stream.of("alice", "bob", "charlie")
       .collect(collectors.tolist());
   ```

2. **collecting elements into a set:**
   ```java
   set<integer> numbers = stream.of(1, 2, 3, 2, 4, 5)
       .collect(collectors.toset());
   ```

3. **collecting elements into a map:**
   ```java
   map<string, integer> namelengthmap = stream.of("alice", "bob", "charlie")
       .collect(collectors.tomap(name -> name, name -> name.length()));
   ```

4. **joining elements into a string:**
   ```java
   string joinednames = stream.of("alice", "bob", "charlie")
       .collect(collectors.joining(", "));
   ```

5. **calculating sum, average, max, min, etc.:**
   ```java
   int sum = stream.of(1, 2, 3, 4, 5)
       .collect(collectors.summingint(integer::intvalue));
   
   double average = stream.of(1, 2, 3, 4, 5)
       .collect(collectors.averagingint(integer::intvalue));
   
   optional<integer> max = stream.of(1, 2, 3, 4, 5)
       .collect(collectors.maxby(comparator.naturalorder()));
   ```

6. **grouping elements:**
   ```java
   map<character, list<string>> groupednames = stream.of("alice", "bob", "charlie")
       .collect(collectors.groupingby(name -> name.charat(0)));
   ```

7. **partitioning elements:**
   ```java
   map<boolean, list<integer>> evenoddpartition = stream.of(1, 2, 3, 4, 5)
       .collect(collectors.partitioningby(num -> num % 2 == 0));
   ```

these are just a few examples of how you can use `collectors` to perform various operations on the elements of a stream and aggregate them into meaningful results. `collectors` greatly simplify the process of collecting data from streams and allow you to express complex transformations and aggregations in a concise and readable manner.

creating custom collectors. you can create your own custom collectors by implementing the `collector` interface. custom collectors allow you to define specific accumulation logic tailored to your needs. here's an example of how you can create custom collectors:

suppose you want to collect even and odd numbers separately into two different lists. here's how you could create a custom collector to achieve this:

```java
import java.util.arraylist;
import java.util.enumset;
import java.util.list;
import java.util.set;
import java.util.stream.collector;
import java.util.stream.collectors;

public class customcollectorexample {
    public static void main(string[] args) {
        list<integer> numbers = list.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        numberspartition partition = numbers.stream()
            .collect(new evenoddpartitioningcollector());

        system.out.println("even numbers: " + partition.evennumbers);
        system.out.println("odd numbers: " + partition.oddnumbers);
    }
}

class numberspartition {
    list<integer> evennumbers = new arraylist<>();
    list<integer> oddnumbers = new arraylist<>();
}

class evenoddpartitioningcollector implements collector<integer, numberspartition, numberspartition> {
    @override
    public supplier<numberspartition> supplier() {
        return numberspartition::new;
    }

    @override
    public biconsumer<numberspartition, integer> accumulator() {
        return (partition, number) -> {
            if (number % 2 == 0) {
                partition.evennumbers.add(number);
            } else {
                partition.oddnumbers.add(number);
            }
        };
    }

    @override
    public binaryoperator<numberspartition> combiner() {
        return (left, right) -> {
            left.evennumbers.addall(right.evennumbers);
            left.oddnumbers.addall(right.oddnumbers);
            return left;
        };
    }

    @override
    public function<numberspartition, numberspartition> finisher() {
        return partition -> partition;
    }

    @override
    public set<characteristics> characteristics() {
        return enumset.noneof(characteristics.class);
    }
}
```

in this example, the `evenoddpartitioningcollector` class implements the `collector` interface. it defines how elements are accumulated, combined, and transformed. the `numberspartition` class is used to hold the accumulated even and odd numbers. the collector can be used in the `collect()` operation to partition the numbers into even and odd lists.

this example demonstrates the process of creating a custom collector to handle a specific use case. custom collectors allow you to define complex accumulation strategies and are a powerful tool for customizing the behavior of your stream operations.

## new date and time api
12. drawbacks of the old date and calendar apis.
  - mutable state:
   both date and calendar were mutable classes, meaning that their internal state could be modified after creation. this made them prone to unexpected side effects and made it challenging to reason about the state of objects.
  - zero-based months:
   in the calendar api, months were represented using zero-based indexing. for example, january was represented as month 0, february as month 1, and so on. this was counterintuitive and led to confusion and mistakes in code.
  - lack of immutability:
   the date class was mutable, which made it challenging to ensure thread safety in multi-threaded environments.
13. java.time package: 
  - localdate, 
  - localtime, 
  - localdatetime, 
  - instant, 
  - duration, 
  - period.
14. working with:
  - **time zones** and 
  - **formatting dates**.

**advanced: concurrency enhancements**

15. introduction to completablefuture for asynchronous programming.
16. creating and chaining completablefutures.
17. handling exceptions and composing asynchronous tasks.

## generics:
generics in java provide a way to create classes, interfaces, and methods that operate on types specified as parameters. they offer several benefits and are essential for writing more reusable, type-safe, and flexible code. here are some reasons why we need generics in java:

### introduction to generics:

**type safety**: generics help catch type-related errors at compile-time rather than runtime. this ensures that you're using the correct types in a consistent manner, reducing the chances of bugs and runtime exceptions.
example (first without generics, then with generics):
```java
list mylist = new arraylist();
mylist.add("hello");
integer value = (integer) mylist.get(0); // runtime classcastexception
```
  - with generics:
```java
list<string> mylist = new arraylist<>();
mylist.add("hello");
integer value = mylist.get(0); // compilation error
````

**code reusability**: generics enable you to write classes, interfaces, and methods that can work with a variety of data types. this promotes code reuse, as a single implementation can cater to different types.

**eliminate type casting**: generics eliminate the need for explicit type casting when retrieving elements from collections or working with other data structures. this leads to cleaner and more readable code.

**stronger abstractions**: generics allow you to define abstractions that work with a range of types. this enables you to create more generic and flexible apis that can be used with different data types.

**collections framework**: the java collections framework (e.g., list, set, map, etc.) heavily utilizes generics. it allows you to create collections that hold specific types of elements, improving type safety and eliminating casting.

### generic classes and interfaces:
**defining and using generic classes in java**

generic classes in java allow you to create classes that can work with different data types while maintaining type safety. they provide a powerful way to create reusable and flexible components that can operate seamlessly across various types. let´s explore how to define and use generic classes in java.

**defining a generic class:**

to define a generic class, you use angle brackets (`<>`) to specify a type parameter. this type parameter acts as a placeholder for an actual data type that will be provided when an instance of the class is created. here's the basic syntax:

```java
public class mygenericclass<t> {
    // class members and methods
}
```

in this example, `t` is the type parameter. it can be any valid java identifier, but by convention, single uppercase letters like `t` are often used. you can use this type parameter within the class just like any other type.

**using a generic class:**

when you create an instance of a generic class, you provide the actual type argument that the type parameter will take. this binding of the type parameter to an actual type is called "parameterizing" the class. here's how you use a generic class:

```java
public class main {
    public static void main(string[] args) {
        // parameterize mygenericclass with integer
        mygenericclass<integer> intobj = new mygenericclass<>();
        
        // parameterize mygenericclass with string
        mygenericclass<string> strobj = new mygenericclass<>();
    }
}
```

**example: generic box class**

here's a simple example of a generic class that represents a box that can hold any type of object:

```java
public class box<t> {
    private t content;
    
    public void setcontent(t content) {
        this.content = content;
    }
    
    public t getcontent() {
        return content;
    }
    
    public static void main(string[] args) {
        box<integer> intbox = new box<>();
        intbox.setcontent(42);
        
        box<string> strbox = new box<>();
        strbox.setcontent("hello, world!");
        
        system.out.println(intbox.getcontent()); // output: 42
        system.out.println(strbox.getcontent()); // output: hello, world!
    }
}
```

in this example, the `box` class is defined with a type parameter `t`. instances of `box` are created by specifying the actual type (e.g., `integer`, `string`) when declaring the variable.

**implementing generic interfaces in java**

generic interfaces allow you to create flexible and reusable contracts that can be implemented by various classes, accommodating different types while maintaining type safety. just like generic classes, generic interfaces enable you to design components that work with a wide range of data types. let's explore how to implement generic interfaces in java.

**defining a generic interface:**

a generic interface is defined similarly to a regular interface, with the addition of type parameters enclosed in angle brackets (`<>`). these type parameters represent placeholders for actual types that will be provided when implementing the interface. here's the basic syntax:

```java
public interface mygenericinterface<t> {
    // method signatures
}
```

in this example, `t` is the type parameter of the generic interface.

**implementing a generic interface:**

when you implement a generic interface, you need to provide the actual type argument that matches the type parameter of the interface. this allows you to customize the interface methods to work with specific data types. here's how you implement a generic interface:

```java
public class myimplementation<t> implements mygenericinterface<t> {
    // implement interface methods
}
```

**example: stack interface**

here's a practical example of a generic interface called `stack`, which represents a stack data structure. the interface defines methods to push, pop, and peek at elements in the stack:

```java
public interface stack<t> {
    void push(t element);
    t pop();
    t peek();
}
```

now, let's implement the `stack` interface with a class that uses a list to maintain the stack:

```java
import java.util.arraylist;
import java.util.list;

public class liststack<t> implements stack<t> {
    private list<t> stacklist = new arraylist<>();

    @override
    public void push(t element) {
        stacklist.add(element);
    }

    @override
    public t pop() {
        if (isempty()) {
            throw new illegalstateexception("stack is empty");
        }
        return stacklist.remove(stacklist.size() - 1);
    }

    @override
    public t peek() {
        if (isempty()) {
            throw new illegalstateexception("stack is empty");
        }
        return stacklist.get(stacklist.size() - 1);
    }

    public boolean isempty() {
        return stacklist.isempty();
    }

    public static void main(string[] args) {
        stack<integer> intstack = new liststack<>();
        intstack.push(10);
        intstack.push(20);
        intstack.push(30);
        
        system.out.println(intstack.pop()); // output: 30
        system.out.println(intstack.peek()); // output: 20
    }
}
```

in this example, the `liststack` class implements the `stack` interface with a generic type parameter `t`. the class uses an `arraylist` to manage the stack. by implementing the `stack` interface, the class ensures that it adheres to the stack contract for any type `t`.

### type parameters and wildcards:
#### type parameters in generic methods:
you can use type parameters in generic methods to create methods that work with multiple types. The type parameter is declared before the return type of the method. Here's an example:
```java
public class mygenericmethods {
    public <T> void printarray(T[] array) {
        for (T element : array) {
            system.out.println(element);
        }
    }

    public static void main(string[] args) {
        integer[] intarray = { 1, 2, 3 };
        string[] strarray = { "a", "b", "c" };

        mygenericmethods genericmethods = new mygenericmethods();
        genericmethods.printarray(intarray); // prints 1 2 3
        genericmethods.printarray(strarray); // prints a b c
    }
}
```

in this example, the printarray method is a generic method that can work with arrays of any type. the type parameter T is used to represent the element type of the array.

#### unbounded wildcards, upper-bounded wildcards, lower-bounded wildcards
**Unbounded Wildcards, Upper-Bounded Wildcards, and Lower-Bounded Wildcards in Java Generics**

Wildcards in Java generics provide a way to write more flexible and versatile code when working with generic types. There are three types of wildcards: unbounded wildcards, upper-bounded wildcards, and lower-bounded wildcards. These wildcards allow you to work with generic types in a broader context while maintaining type safety. Let's explore each type:

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


### generics and method overloading:
- handling method overloading with generic methods
- resolving ambiguity in overloaded methods with type inference
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