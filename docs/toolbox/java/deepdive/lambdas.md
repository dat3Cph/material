---
title: Lambdas
description: Lambdas in Java
layout: default
nav_order: 11
parent: Java
grand_parent: Toolbox
permalink: /toolbox/java/lambdas/
---

# Lambdas

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
