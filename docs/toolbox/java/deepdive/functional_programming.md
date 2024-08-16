---
title: Functional Programming
description: Theory for functional programming in Java
layout: default
nav_order: 1
parent: Java
grand_parent: Toolbox
permalink: /toolbox/java/functional-programming/
---

# Java 8 Deep Dive II

## Day 1: Functional Programming

## Introduction to Java 8 Features

1. **Lambdas** enable concise and functional-style coding, making it easier to express operations on collections and functional interfaces.
2. **Streams** provide a declarative way to process data in parallel or sequentially, promoting cleaner and more readable code.
3. **Default Methods**: Interfaces can now have default method implementations, allowing for backward-compatible additions to interfaces without breaking existing implementations.
4. **Method References** : Method references simplify code by allowing methods to be referred to using concise syntax, enhancing code readability.
5. **Functional Interfaces** : Java 8 introduced functional interfaces, which are interfaces with a single abstract method, facilitating the use of lambda expressions.
6. **Type Inference**: The diamond operator and improved type inference allow for more concise code when dealing with generic types.
7. **Date and Time API**: The new Date and Time API (java.time) simplifies working with dates, times, and time zones, addressing many shortcomings of the old Date and Calendar classes.
8. **Functional Programming** Paradigm: Java 8 encourages a more functional programming style, promoting immutability, pure functions, and higher-order functions, resulting in more reliable and maintainable code.

## What is functional programming?

Functional programming is a programming paradigm that treats computation as the evaluation of mathematical functions and avoids changing-state and mutable data. While Java is primarily an object-oriented programming language, Java 8 introduced several features that enable functional programming concepts to be applied effectively. Here's how functional programming is characterized in Java:

1. **First-Class Functions:**
   In functional programming, functions are first-class citizens, meaning they can be treated like any other value. Java introduced lambda expressions (anonymous functions) in Java 8, allowing you to pass functions as arguments to other functions and return them as values from functions.

2. **Immutability:**
   Functional programming encourages the use of immutable data structures. While Java's core data structures are mutable, you can follow functional programming principles by creating immutable classes and using the `final` keyword to prevent modifications.

3. **Higher-Order Functions:**
   A higher-order function is a function that takes one or more functions as arguments or returns a function as its result. In Java, you can pass lambdas as arguments to methods, such as those provided by the Stream API or other functional interfaces.

4. **Pure Functions:**
   Pure functions are functions that have no side effects and always return the same output for the same input. While Java doesn't enforce pure functions, functional programming encourages writing code with minimal side effects and deterministic behavior.

5. **Functional Interfaces:**
   Java introduced functional interfaces in Java 8 to represent single-method interfaces. These interfaces are used to define the types of lambda expressions or method references. Java.util Examples include `Predicate`, `Consumer`, `Function`, and `Supplier`.

6. **Readability and Expressiveness:**
    Functional programming often results in more concise and readable code, thanks to lambda expressions and functional interfaces. It encourages a declarative style of programming, where you specify what you want to achieve rather than how to achieve it.

While Java is not a purely functional programming language like Haskell or Scala, it has incorporated many functional programming features that allow developers to write code using functional paradigms when appropriate. This can lead to more modular, maintainable, and efficient code in various scenarios.

## Lambda Expressions

What are Lambda expressions?

- Lambda expressions are a significant feature introduced in Java 8 that facilitates functional programming by allowing you to express instances of single-method interfaces (functional interfaces) using a concise syntax. Lambda expressions essentially enable you to treat functions as method arguments, creating a more readable and expressive code style.

- In simpler terms, a lambda expression is a way to represent an anonymous function (a function without a name, that you can pass around as if it was a variable). Lambda expressions are primarily used to define inline implementations of functional interfaces.

See example code here: <https://raw.githubusercontent.com/HartmannDemoCode/callbackInJava/master/src/callbackinjava/CallbackInJava.java>

- Syntax and structure of Lambda expressions.
Here's the basic syntax of a lambda expression:

```java
(parameter(s)) -> expression
```

Or for a block of code:

```java
(parameter(s)) -> {
    // code block
    // more statements
    return result;
}
```

Let's see an example of how lambda expressions work:

```java
// Functional interface with a single method
interface MyFunction {
    int doOperate(int a, int b);
}

public class Main {
    public static void main(String[] args) {
        // Using a lambda expression to define the implementation of the functional interface
        MyFunction addition = (a, b) -> a + b;
        
        System.out.println(addition.doOperate(3, 5));  // Output: 8
    }
}
```

In this example, the `MyFunction` interface is a functional interface with a single method named `doOperate`. The lambda expression `(a, b) -> a + b` defines the implementation of the `doOperate` method. It takes two integer parameters and returns their sum.

Lambda expressions are particularly useful in scenarios like using the Stream API for functional operations on collections, passing behavior to methods (e.g., sorting, filtering), and creating more concise and readable code. They provide a way to express functional behavior without the need to write full anonymous inner classes.

Lambda expressions are closely related to functional interfaces. A functional interface is an interface that contains **exactly one abstract method**, and it's the kind of interface that you'll often work with when using lambda expressions.

## Functional Interfaces

A functional interface is an interface that contains **exactly one abstract method**, and it's the kind of interface that you'll often work with when using lambda expressions.

Creating custom functional interfaces.
Example code here: <https://raw.githubusercontent.com/HartmannDemoCode/callbackInJava/master/src/callbackinjava/CallbackInJava.java>

## Some Functional interfaces in the `java.util.function` package

- Predicate: **One argument -> returns boolean**,
- Consumer: **One argument -> returns void**,
- Function<T,V>: **One argument (T) -> returns result (V)** (for more advanced use cases, you can use BiFunction<T,U,V> for two arguments)
- Supplier<T>: **Zero arguments -> returns (T)**.

### Predicate

A Predicate is a functional interface that **represents a boolean-valued function of a single argument**. It's often used for filtering elements in collections or making boolean decisions based on a condition.

```java
import java.util.function.Predicate;

public class PredicateExample {
    public static void main(String[] args) {
        // Predicate to check if a number is even
        Predicate<Integer> isEven = num -> num % 2 == 0;

        System.out.println(isEven.test(4));    // Output: true
        System.out.println(isEven.test(7));    // Output: false
    }
}
```

### Consumer

A Consumer is a functional interface that represents **an operation that takes a single input and has no result**. It's often used for side effects, like printing or modifying elements.

```java
import java.util.List;
import java.util.function.Consumer;

public class ConsumerExample {
    public static void main(String[] args) {
        // Consumer to print each element in a list
        Consumer<String> printElement = element -> System.out.println(element);

        List<String> names = List.of("Alice", "Bob", "Charlie");
        names.forEach(printElement);    // Output: Alice, Bob, Charlie
    }
}
```

### Function

A Function is a functional interface that represents a function that takes **one argument and produces a result**. It's often used for transforming input into output.

```java
import java.util.function.Function;

public class FunctionExample {
    public static void main(String[] args) {
        // Function to convert a string to its length
        Function<String, Integer> lengthFunction = str -> str.length();

        System.out.println(lengthFunction.apply("Java"));     // Output: 4
        System.out.println(lengthFunction.apply("Programming")); // Output: 11
    }
}
```

### Supplier

A Supplier is a functional interface that represents a supplier of **results, with no input arguments**. It's often used to generate or provide values.

```java
import java.util.Random;
import java.util.function.Supplier;

public class SupplierExample {
    public static void main(String[] args) {
        // Supplier to generate a random number
        Supplier<Integer> randomSupplier = () -> new Random().nextInt(100);

        System.out.println(randomSupplier.get());    // Output: Random number between 0 and 99
        System.out.println(randomSupplier.get());    // Another random number
    }
}
```

These functional interfaces, along with lambda expressions, provide a powerful way to work with functional programming concepts in Java.

## Functional Programming Concepts

- **Immutability** and why it's important
- **Pure functions**, side effects, and referential transparency (it consistently produces the same output for the same input, and its evaluation doesn't have side effects that affect the rest of the program)
- **Equational Reasoning**: Referential transparency allows for equational reasoning, which means you can substitute function calls or expressions with their corresponding values and still reason about the correctness of your program.
- **Code Optimization**: Since referentially transparent expressions can be replaced with their values, compilers and runtime systems have more freedom to optimize the code without changing its behavior.
- **Parallelism and Concurrency**: In a referentially transparent program, you can safely parallelize or reorder function calls without introducing unexpected side effects.
- **Testing**: Referentially transparent functions are easier to test because you can predict their output based on their inputs, without worrying about hidden dependencies or changing states.
- **Code Reusability**: Referential transparency promotes modular and reusable code since functions with this property are isolated from the context in which they are used.
- In functional programming, designing functions and expressions to be referentially transparent is a key principle that encourages modularity, predictability, and robustness in software systems. It also aligns well with the goal of creating code that is easier to reason about and maintain.

## Java Time API

[Working with dates and times](JavaTimeAPI.md)

## Default and Static Methods in Interfaces

In Java 8, default methods were introduced in interfaces. A default method is a method that is defined in an interface with a default implementation. This means that if a class implements that interface but doesn't provide its own implementation for the default method, the default implementation from the interface will be used.

However, conflicts can arise when a class implements multiple interfaces that have default methods with the same signature. This situation leads to an ambiguity: which default method implementation should the class use?

Here's an example to illustrate the concept:

```java
interface InterfaceA {
    default void doSomething() {
        System.out.println("Default implementation in InterfaceA");
    }
}

interface InterfaceB {
    default void doSomething() {
        System.out.println("Default implementation in InterfaceB");
    }
}

class MyClass implements InterfaceA, InterfaceB {
    // This class inherits default methods from both InterfaceA and InterfaceB
    
    // Uncomment the following method to resolve the conflict
    /*
    @Override
    public void doSomething() {
        InterfaceA.super.doSomething(); // Calling specific default method
    }
    */
}

public class Main {
    public static void main(String[] args) {
        MyClass obj = new MyClass();
        obj.doSomething();
    }
}
```

- In this example, the `MyClass` class implements both `InterfaceA` and `InterfaceB`, both of which have a default method named `doSomething()`. This would lead to a compilation error due to a conflict.

- To resolve this conflict, you need to provide your own implementation of the conflicting method in the implementing class (`MyClass` in this case). You can call one of the default implementations explicitly using the `InterfaceName.super.methodName()` syntax, or you can provide a completely new implementation. In the example above, if you uncomment the overridden `doSomething()` method in `MyClass`, you can decide which default implementation to use by calling the specific default method using `InterfaceA.super.doSomething()`.

- Resolving conflicts with default methods ensures that the implementing class provides a clear and unambiguous choice of which default implementation to use when multiple interfaces have methods with the same signature.

## Method References

Simplifying Lambda expressions using method references.

- Types of method references: static, instance, and constructor references.

Method references in Java provide a concise way to refer to methods or constructors and use them as arguments for higher-order functions like those provided by the Stream API. Here are examples of static, instance, and constructor method references:

**1. Static Method Reference:**

```java
import java.util.Arrays;

public class StaticMethodReferenceExample {
    public static void main(String[] args) {
        String[] names = {"Alice", "Bob", "Charlie", "David"};

        // Using static method reference to sort the array
        Arrays.sort(names, StaticMethodReferenceExample::compareNames);

        // Printing the sorted array
        for (String name : names) {
            System.out.println(name);
        }
    }

    // Static method for comparing names
    public static int compareNames(String a, String b) {
        return a.compareTo(b);
    }
}
```

**2. Instance Method Reference:**

```java
import java.util.ArrayList;
import java.util.List;

public class InstanceMethodReferenceExample {
    public static void main(String[] args) {
        List<String> names = new ArrayList<>();
        names.add("Alice");
        names.add("Bob");
        names.add("Charlie");

        // Using instance method reference to print each element
        names.forEach(System.out::println);
    }
}
```

**3. Constructor Method Reference:**

```java
import java.util.function.Supplier;
import java.util.function.Function;
import java.util.function.BiFunction;

class Person {
    private String name;

    // 3 constructors:
    public Person() {
        this.name = "Unknown";
    }
    public Person(String name) {
        this.name = name;
    }
      public Person(String firstName, String lastName) {
         this.name = firstName + " " + lastName;
      }

    public String getName() {
        return name;
    }
}

public class ConstructorMethodReferenceExample {
    public static void main(String[] args) {
        // Using constructor method reference to create instances
        Supplier<Person> personSupplier = Person::new; // no-arg constructor
        Person person = personSupplier.get();
        person.getName();

        Function<String, Person> personCreatorOne = Person::new; // one-arg constructor
        Person person = personCreatorOne.apply("Alice"); 

        BiFunction<String, String, Person> personCreatorTwo = Person::new; // two-arg constructor
        Person person = personCreatorTwo.apply("Alice", "Johnson");

        // Using constructor method reference to create a Person object directly
        PersonCreator creator = Person::new;
        Person person = creator.createPerson("Alice");
        System.out.println("Person Name: " + person.getName());
    }

@FunctionalInterface
interface PersonCreator {
    Person createPerson(String name);
}
}
```

In these examples:

- **Static Method Reference:** We use a static method reference (`StaticMethodReferenceExample::compareNames`) to pass the comparison logic to the `Arrays.sort` method.

- **Instance Method Reference:** We use an instance method reference (`System.out::println`) to pass the `println` method of `System.out` as a consumer function to the `forEach` method of the `names` list.

- **Constructor Method Reference:** We use a constructor method reference (`Person::new`) to create instances of the `Person` class using the `Supplier` functional interface.

Method references provide a more compact and readable way to pass methods or constructors as arguments, especially when working with functional interfaces or stream operations.
