---
title: Filter
description: How the filter function works in JavaScript
layout: default
nav_order: 5
parent: JavaScript
grand_parent: Toolbox
has_children: false
permalink: /toolbox/javascript/filter
---

# Filter in JavaScript

The `filter` function in JavaScript is used to create a new array containing only the elements that pass a specific condition or test. It’s perfect for scenarios where you want to keep some items in an array and exclude others based on certain criteria.

## Basic Syntax of `filter`

```javascript
const newArray = array.filter((currentValue, index, array) => {
    // condition to keep currentValue
});
```

1. **currentValue**: The current element in the array being processed.
2. **index** (optional): The index of the current element in the array.
3. **array** (optional): The original array that `filter` was called on.

The callback function passed to `filter` should return `true` to keep an element or `false` to exclude it from the resulting array.

---

## How `filter` Works

When you call `filter` on an array, it loops through each element and applies the condition specified in the callback function. Only the elements that satisfy the condition (`true` values) are kept in the new array, while all others are filtered out.

### Example Walkthrough

Here’s a simple example where we filter an array of numbers to keep only the even ones:

```javascript
const numbers = [1, 2, 3, 4, 5, 6];
const evenNumbers = numbers.filter((num) => num % 2 === 0);

console.log(evenNumbers); // Output: [2, 4, 6]
console.log(numbers);      // Output: [1, 2, 3, 4, 5, 6] (original array unchanged)
```

**Explanation**:

- For each element in the `numbers` array, `filter` checks if the number is even (`num % 2 === 0`).
- Only the numbers that satisfy this condition are added to the new `evenNumbers` array.

---

## Common Use Cases for `filter`

1. **Filtering Numbers**:
   - Use `filter` to keep numbers based on certain criteria, like selecting only even or odd numbers, or numbers within a range.

   ```javascript
   const numbers = [1, 2, 3, 4, 5, 6];
   const greaterThanThree = numbers.filter((num) => num > 3);
   // Output: [4, 5, 6]
   ```

2. **Filtering Objects by Property**:
   - `filter` is commonly used to filter arrays of objects by checking properties.

   ```javascript
   const users = [
     { name: "Alice", age: 25 },
     { name: "Bob", age: 20 },
     { name: "Charlie", age: 35 }
   ];
   const adults = users.filter((user) => user.age >= 21);
   // Output: [{ name: "Alice", age: 25 }, { name: "Charlie", age: 35 }]
   ```

3. **Filtering Strings**:
   - `filter` can be used to remove or select specific strings based on conditions, like length, content, or case.

   ```javascript
   const words = ["apple", "banana", "pear", "kiwi"];
   const longWords = words.filter((word) => word.length > 4);
   // Output: ["apple", "banana"]
   ```

4. **Removing Falsy Values**:
   - You can use `filter` to remove all falsy values from an array (e.g., `null`, `undefined`, `0`, `""`, `NaN`, `false`).

   ```javascript
   const values = [0, "hello", false, "", 42, null, "world"];
   const truthyValues = values.filter(Boolean);
   // Output: ["hello", 42, "world"]
   ```

5. **Filtering Unique Values**:
   - Using `filter` with `indexOf`, you can filter an array to contain only unique values.

   ```javascript
   const numbers = [1, 2, 2, 3, 4, 4, 5];
   const uniqueNumbers = numbers.filter((num, index, arr) => arr.indexOf(num) === index);
   // Output: [1, 2, 3, 4, 5]
   ```

---

## Key Points about `filter`

- **Non-mutative**: `filter` doesn’t change the original array; it returns a new one.
- **Variable Length**: Unlike `map`, which returns an array of the same length, `filter` can return an array of any length (or even an empty array) based on the criteria.
- **Boolean Test**: The callback function in `filter` should return `true` for elements to keep and `false` for elements to exclude.
- **Functional and Declarative**: Like `map`, `filter` fits well in a functional programming style, allowing concise, declarative code.

`filter` is very useful for selecting subsets of data and works well in combination with other array methods like `map` and `reduce` to create readable, functional code.
