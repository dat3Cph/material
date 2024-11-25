---
title: JS Spread Operator
description: Exercises for Frontend Week I
layout: default
nav_order: 4
grand_parent: JS and React I
parent: Exercises
permalink: /frontend/javascript-react-intro/exercises/js-spread-operator/
---

# Exercise 3: The Spread Operator in JavaScript

**Make this exercise in Visual Studio Code and node.js.**

These exercises practice the spread operator, which will be valuable when you start learning React.

[Documentation on MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

### 3.1 Merging Arrays

**Exercise:**  

Given two arrays:

```javascript
const array1 = [1, 2, 3];
const array2 = [4, 5, 6];
```

Use the spread operator to merge `array1` and `array2` into a new array called `mergedArray`. Print `mergedArray`.

**Expected Output:**

```plaintext
[1, 2, 3, 4, 5, 6]
```

### 3.2 Copying Array

**Exercise:**

Given the array:

```javascript
const originalArray = ['apple', 'banana', 'cherry'];
```

Use the spread operator to create a copy of `originalArray` called `copiedArray`. Then, add `'date'` to `copiedArray` without changing `originalArray`. Print both arrays to verify.

**Expected Output:**

```plaintext
originalArray: ['apple', 'banana', 'cherry']
copiedArray: ['apple', 'banana', 'cherry', 'date']
```

### 3.3 Adding Elements to the Beginning of an Array

**Exercise:**  

Given the array:

```javascript
const numbers = [20, 30, 40];
```

Use the spread operator to add `10` at the beginning of `numbers`, creating a new array called `newNumbers`. Print `newNumbers`.

**Expected Output:**

```plaintext
[10, 20, 30, 40]
```

### 4. Merging Objects

**Exercise:**  

Given two objects:

```javascript
const userDetails = { name: 'Alice', age: 25 };
const contactInfo = { email: 'alice@example.com', phone: '123-456-7890' };
```

Use the spread operator to merge `userDetails` and `contactInfo` into a new object called `userProfile`. Print `userProfile`.

**Expected Output:**

```plaintext
{ name: 'Alice', age: 25, email: 'alice@example.com', phone: '123-456-7890' }
```

### 3.5 Copying and Modifying an Object

**Exercise:**  

Given the object:

```javascript
const book = { title: '1984', author: 'George Orwell', year: 1949 };
```

Use the spread operator to create a copy of `book`, but modify the `year` to `1950` in the new object `updatedBook`. Print both `book` and `updatedBook`.

**Expected Output:**

```plaintext
book: { title: '1984', author: 'George Orwell', year: 1949 }
updatedBook: { title: '1984', author: 'George Orwell', year: 1950 }
```

### 6. Using Spread with Function Arguments

**Exercise:**  

Define a function `sum` that takes any number of arguments and returns their sum. Use the spread operator to pass an array of numbers to this function:

```javascript
const numbers = [5, 10, 15];
console.log(sum(...numbers));
```

**Expected Output:**

```plaintext
30
```

### 7. Combining Arrays with New Elements

**Exercise:**  

Given two arrays:

```javascript
const colors1 = ['red', 'blue'];
const colors2 = ['green', 'yellow'];
```

Use the spread operator to combine `colors1` and `colors2` into a new array called `allColors`, but add `'purple'` at the end of the array. Print `allColors`.

**Expected Output:**

```plaintext
['red', 'blue', 'green', 'yellow', 'purple']
```

### 8. Rest Operator in Function Parameters

**Exercise:**  

Define a function `describePerson` that takes a `name` parameter followed by any number of hobbies (using the rest operator). The function should log the name and a list of hobbies. Call the function as shown:

```javascript
describePerson('Charlie', 'reading', 'coding', 'hiking');
```

**Expected Output:**

```plaintext
Name: Charlie, Hobbies: reading, coding, hiking
```

### 9. Destructuring with Rest Operator

**Exercise:**  

Given the array:

```javascript
const numbers = [10, 20, 30, 40, 50];
```

Use array destructuring with the rest operator to assign the first element to `firstNum` and the remaining elements to `otherNums`. Print `firstNum` and `otherNums`.

**Expected Output:**

```plaintext
firstNum: 10
otherNums: [20, 30, 40, 50]
```
