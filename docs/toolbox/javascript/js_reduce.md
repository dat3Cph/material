---
title: Reduce
description: How the reduce function works in JavaScript
layout: default
nav_order: 6
parent: JavaScript
grand_parent: Toolbox
has_children: false
permalink: /toolbox/javascript/reduce
---

# Reduce in JavaScript

The `reduce` function in JavaScript is a powerful tool for processing an array and reducing it to a single value, whether that’s a number, string, object, or even another array. Here’s a breakdown of how it works and why it’s so useful.

### Basic Syntax of `reduce`

```javascript
array.reduce((accumulator, currentValue, index, array) => {
    // logic to accumulate values
}, initialValue);
```

1. **Accumulator**: The first parameter of the callback function. This is the value that carries over between each step as the array is processed. It “accumulates” the result.
2. **Current Value**: The current element in the array being processed.
3. **Index** (optional): The index of the current element.
4. **Array** (optional): The original array that `reduce` was called on.
5. **Initial Value**: The initial value of the accumulator. This value is optional, but if you don't provide it, `reduce` will use the first element of the array as the accumulator and start from the second element.

---

### Example Walkthrough

Let’s look at a simple example where we sum an array of numbers using `reduce`:

```javascript
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((accumulator, currentValue) => {
  return accumulator + currentValue;
}, 0);

console.log(sum); // Output: 10
```

**Explanation**:

- The `reduce` function starts with an `accumulator` set to the initial value, which is `0` in this case.
- Then it iterates over each element in the `numbers` array, updating the `accumulator` by adding the `currentValue` to it.
  
**Steps**:

1. **First iteration**: `accumulator` = 0, `currentValue` = 1 → New `accumulator` = 0 + 1 = 1
2. **Second iteration**: `accumulator` = 1, `currentValue` = 2 → New `accumulator` = 1 + 2 = 3
3. **Third iteration**: `accumulator` = 3, `currentValue` = 3 → New `accumulator` = 3 + 3 = 6
4. **Fourth iteration**: `accumulator` = 6, `currentValue` = 4 → New `accumulator` = 6 + 4 = 10

After the final iteration, `reduce` returns the `accumulator`, which is `10`.

---

### Common Use Cases for `reduce`

1. **Summing an Array**:

   ```javascript
   const sum = numbers.reduce((acc, curr) => acc + curr, 0);
   ```

2. **Finding the Maximum**:

   ```javascript
   const max = numbers.reduce((acc, curr) => (curr > acc ? curr : acc), numbers[0]);
   ```

3. **Flattening an Array of Arrays**:

   ```javascript
   const arrays = [[1, 2], [3, 4], [5]];
   const flatArray = arrays.reduce((acc, curr) => acc.concat(curr), []);
   // Output: [1, 2, 3, 4, 5]
   ```

4. **Counting Occurrences**:

   ```javascript
   const fruits = ["apple", "banana", "apple", "orange", "banana", "apple"];
   const count = fruits.reduce((acc, fruit) => {
     acc[fruit] = (acc[fruit] || 0) + 1;
     return acc;
   }, {});
   // Output: { apple: 3, banana: 2, orange: 1 }
   ```

5. **Transforming to an Object**:

   ```javascript
   const pairs = [["name", "Alice"], ["age", 25], ["city", "New York"]];
   const obj = pairs.reduce((acc, [key, value]) => {
     acc[key] = value;
     return acc;
   }, {});
   // Output: { name: "Alice", age: 25, city: "New York" }
   ```

---

### Why Use `reduce`?

- **Versatile**: It can accomplish various transformations and aggregations.
- **Functional Programming**: It allows for concise, declarative code and often eliminates the need for explicit loops.
- **Single Source of Result**: It’s efficient for producing a single output from a collection, whether it’s an object, number, or array.
