---
title: JS Arrow Functions
description: Exercises for Frontend Week I
layout: default
nav_order: 3
grand_parent: JS and React I
parent: Exercises
permalink: /frontend/javascript-react-intro/exercises/js-arrow-functions/
---

# Exercise 1: Getting comfortable arrow functions in JavaScript

**Make this exercise in Visual Studio Code and node.js.**

- [Documentation on MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

It's time to get familiar with arrow functions in JavaScript. Arrow functions are a concise way to write functions in JavaScript. They are especially useful when working with array methods like `map`, `filter`, and `reduce`. So it's similar to *lambda functions* in Java.

## 1.1 Basic Arrow Function Syntax

**Exercise:**  

Rewrite the following function as an arrow function:

```javascript
function greet() {
  return 'Hello, World!';
}
```

Store the result in a variable called `greet` and call the function to see the output.

**Expected Output:**

```plaintext
Hello, World!
```

## 1.2 Arrow Function with Parameters

**Exercise:**  

Convert this function into an arrow function:

```javascript
function add(a, b) {
  return a + b;
}
```

Store the arrow function in a variable called `add` and call it with `add(5, 3)`.

**Expected Output:**

```plaintext
8
```

## 1.3 Implicit Return in Arrow Functions

**Exercise:**  

Rewrite the following function using an arrow function with an implicit return:

```javascript
function multiply(a, b) {
  return a * b;
}
```

Test it by calling `multiply(4, 2)`.

**Expected Output:**

```plaintext
8
```

## 1.4 Arrow Function Without Parameters

**Exercise:**  

Write an arrow function called `getRandomNumber` that returns a random number between 0 and 1 (using `Math.random`). Test by calling `getRandomNumber()`.

**Expected Output:**

A random number between 0 and 1 (e.g., `0.456`).

## 1.5 Arrow Function with a Single Parameter

**Exercise:**  

Rewrite the following function as an arrow function with a single parameter and implicit return:

```javascript
function square(x) {
  return x * x;
}
```

Test by calling `square(5)`.

**Expected Output:**

```plaintext
25
```

## 1.6 Using Arrow Functions in Array Methods

**Exercise:**  

Use an arrow function to double each number in the array:

```javascript
const numbers = [1, 2, 3, 4];
const doubledNumbers = numbers.map(/* your arrow function here */);
console.log(doubledNumbers);
```

**Expected Output:**

```plaintext
[2, 4, 6, 8]
```

## 1.7 Filtering an Array with Arrow Functions

**Exercise:**  

Given an array of numbers:

```javascript
const numbers = [5, 12, 18, 7, 24];
```

Use an arrow function with the `filter` method to create a new array containing only the numbers greater than 10. Print the result.

**Expected Output:**

```plaintext
[12, 18, 24]
```

## 1.8 Arrow Function as a Callback

**Exercise:**  

Use an arrow function as a callback in the `setTimeout` function to print `"Hello after 1 second"` after a 1-second delay.

```javascript
setTimeout(/* your arrow function here */, 1000);
```

**Expected Output (after 1 second):**

```plaintext
Hello after 1 second
```

## 1.9 Arrow Function and `this` Context

**Exercise:**  
Write an object `person` with properties `name` and `sayHello`. The `sayHello` property should be an arrow function that logs `"Hello, my name is <name>"` where `<name>` is the value of the `name` property.

```javascript
const person = {
  name: 'Alice',
  sayHello: /* your arrow function here */
};
person.sayHello();
```

**Expected Output:**

```plaintext
Hello, my name is Alice
```

*(Note: This exercise demonstrates that arrow functions do not have their own `this` context.)*

## 1.10 Arrow Function with Default Parameters

**Exercise:**

Create an arrow function `greet` with two parameters: `name` and `greeting`, where `greeting` has a default value of `"Hello"`. The function should return a message like `"Hello, Alice!"` if no greeting is provided.

Test with:

```javascript
console.log(greet('Alice')); // Uses default greeting
console.log(greet('Bob', 'Hi')); // Uses custom greeting
```

**Expected Output:**

```plaintext
Hello, Alice!
Hi, Bob!
```
