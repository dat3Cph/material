---
title: JS Destructuring
description: Exercises for Frontend Week I
layout: default
nav_order: 4
grand_parent: JS and React I
parent: Exercises
permalink: /frontend/javascript-react-intro/exercises/js-destructuring/
---

# Exercise 2: Destructuring in JavaScript

**Make this exercise in Visual Studio Code and node.js.**

These exercises practice the destructuring in JavaScript, which will be valuable when you start learning React.

- [Documentation on MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

## 2.1 Basic Array Destructuring

**Exercise:**

Given the array:

```javascript
const fruits = ['apple', 'banana', 'cherry'];
```

Use array destructuring to assign the values to variables `firstFruit`, `secondFruit`, and `thirdFruit`. Print each variable to check the result.

**Expected Output:**

```plaintext
apple
banana
cherry
```

## 2.2 Skipping Elements in Arrays

**Exercise:**

Given the array:

```javascript
const colors = ['red', 'green', 'blue', 'yellow'];
```

Use destructuring to assign the first and third colors to `firstColor` and `thirdColor`, skipping the second color.

**Expected Output:**

```plaintext
red
blue
```

## 2.3 Default Values with Array Destructuring

**Exercise:**  

Given an array that might be missing values:

```javascript
const numbers = [10, 20];
```

Use destructuring to assign `num1`, `num2`, and `num3`, where `num3` should default to 30 if it’s not in the array. Print each variable to check the result.

**Expected Output:**

```plaintext
num1: 10
num2: 20
num3: 30
```

## 2.4 Object Destructuring Basics

**Exercise:**  

Given the object:

```javascript
const person = { name: 'Alice', age: 25, city: 'Wonderland' };
```

Use object destructuring to assign the `name`, `age`, and `city` properties to separate variables. Print each variable to check the result.

**Expected Output:**

```plaintext
Alice
25
Wonderland
```

## 2.5 Renaming Variables in Object Destructuring

**Exercise:**  
Given the object:

```javascript
const book = { title: '1984', author: 'George Orwell', year: 1949 };
```

Use destructuring to assign `title` to `bookTitle`, `author` to `bookAuthor`, and `year` to `publicationYear`. Print each variable.

**Expected Output:**

```plaintext
bookTitle: 1984
bookAuthor: George Orwell
publicationYear: 1949
```

## 2.6 Nested Object Destructuring

**Exercise:**  
Given the object:

```javascript
const student = {
  name: 'Bob',
  grade: 10,
  subjects: {
    math: 'A',
    science: 'B'
  }
};
```

Use nested destructuring to get `name`, `grade`, and the `math` grade. Print each variable.

**Expected Output:**

```plaintext
Bob
10
A
```

## 2.7. Function Parameter Destructuring

**Exercise:**  

Define a function `displayPerson` that takes an object as a parameter with properties `name`, `age`, and `city`. Use destructuring in the function’s parameter to access these properties directly. Call the function with:

```javascript
displayPerson({ name: 'Charlie', age: 30, city: 'Paris' });
```

**Expected Output:**

```plaintext
Name: Charlie, Age: 30, City: Paris
```

## 2.8 Swapping Variables Using Array Destructuring

**Exercise:**  

Given two variables:

```javascript
let a = 5;
let b = 10;
```

Use array destructuring to swap the values of `a` and `b`. Print the variables to check the result.

**Expected Output:**

```plaintext
a: 10
b: 5
```
