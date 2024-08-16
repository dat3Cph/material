---
title: Generics
description: Generics in Java
layout: default
nav_order: 3
parent: Java
grand_parent: Toolbox
permalink: /toolbox/java/generics/
---

# Generics

Generics in java provide a way to create classes, interfaces, and methods that operate on types specified as parameters. they offer several benefits and are essential for writing more reusable, type-safe, and flexible code. here are some reasons why we need generics in java:

## Introduction to generics

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

### Generic classes and interfaces

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

### Type parameters and wildcards

#### Type parameters in generic methods

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

### Generics and method overloading

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
