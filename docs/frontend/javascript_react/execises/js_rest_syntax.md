---
title: JS Rest Parameters
description: Exercises for Frontend Week I
layout: default
nav_order: 5
grand_parent: JS and React I
parent: Exercises
permalink: /frontend/javascript-react-intro/exercises/js-rest-syntax/
---

# Exercise 4: The Rest Parameter Syntax JavaScript

**Make this exercise in Visual Studio Code and node.js.**

These exercises practice the spread rest syntax, which will be valuable when you start learning React.

[Documentation on MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)

Here’s an exercise designed to introduce students to JavaScript’s rest syntax. This exercise involves both function parameters and array destructuring, giving students a chance to see the versatility of the rest syntax.

---

## Objective

To understand and apply JavaScript's rest syntax to handle a variable number of arguments in functions and destructure arrays.

## Instructions

1. **Task 1: Sum of Numbers**

   - Write a function `sumAll` that takes any number of arguments and returns the sum of all arguments.
   - Use the rest parameter syntax to capture all arguments as an array.

   ```javascript
   function sumAll(...numbers) {
     // your code here
   }
   
   console.log(sumAll(1, 2, 3)); // Output: 6
   console.log(sumAll(10, 20, 30, 40)); // Output: 100
   ```

2. **Task 2: Concatenate Strings**

   - Create a function `concatStrings` that takes a required first string and then any number of additional strings. The function should concatenate all strings and return the result.
   - Use the rest syntax to capture the additional strings.

   ```javascript
   function concatStrings(first, ...others) {
     // your code here
   }
   
   console.log(concatStrings("Hello", "World!")); // Output: "Hello World!"
   console.log(concatStrings("I", "love", "JavaScript")); // Output: "I love JavaScript"
   ```

3. **Task 3: Destructure with Rest**

   - Given an array, use destructuring with the rest syntax to separate the first two elements from the rest.
   - Write a function `separateFirstTwo` that accepts an array and returns an object with two properties: `firstTwo` (an array of the first two elements) and `remaining` (an array of the remaining elements).

   ```javascript
   function separateFirstTwo(array) {
     // your code here
   }
   
   console.log(separateFirstTwo([1, 2, 3, 4, 5]));
   // Output: { firstTwo: [1, 2], remaining: [3, 4, 5] }
   ```

### Bonus Challenge

4. **Task 4: Group People by Age**

   - Write a function `groupByAge` that accepts a minimum age and then any number of people objects. Each person object has a `name` and `age` property.
   - The function should return an object with two arrays: `older` for people who are the minimum age or older and `younger` for those younger than the minimum age.

   ```javascript
   function groupByAge(minAge, ...people) {
     // your code here
   }
   
   const people = [
     { name: "Alice", age: 25 },
     { name: "Bob", age: 20 },
     { name: "Charlie", age: 35 },
     { name: "David", age: 18 }
   ];
   
   console.log(groupByAge(21, ...people));
   // Output: { older: [{name: "Alice", age: 25}, {name: "Charlie", age: 35}], younger: [{name: "Bob", age: 20}, {name: "David", age: 18}] }
   ```
