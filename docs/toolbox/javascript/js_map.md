---
title: Map
description: How the reduce function works in JavaScript
layout: default
nav_order: 4
parent: JavaScript
grand_parent: Toolbox
has_children: false
permalink: /toolbox/javascript/map
---

# Map in JavaScript

The `map` function in JavaScript is a very commonly used method that creates a new array by transforming each element in an existing array. It’s ideal when you want to apply a function to every item in an array and get a new array with the transformed items, without changing the original array.

## Basic Syntax of `map`

```javascript
const newArray = array.map((currentValue, index, array) => {
    // logic to transform currentValue
});
```

1. **currentValue**: The current element in the array being processed.
2. **index** (optional): The index of the current element in the array.
3. **array** (optional): The original array that `map` was called on.

---

## How `map` Works

When you call `map` on an array, it loops through each element, applies a function (the transformation you define), and returns a new array with the transformed elements. The original array remains unchanged.

### Example Walkthrough

Here’s a simple example where we double each number in an array using `map`:

```javascript
const numbers = [1, 2, 3, 4];
const doubled = numbers.map((num) => num * 2);

console.log(doubled); // Output: [2, 4, 6, 8]
console.log(numbers); // Output: [1, 2, 3, 4] (original array unchanged)
```

**Explanation**:

- For each element in the `numbers` array, `map` applies the function `num * 2`, doubling the value.
- The `map` function returns a new array with the results, `[2, 4, 6, 8]`.

---

## Common Use Cases for `map`

1. **Transforming Data**:

   - `map` is often used to apply a transformation to each element in an array, such as converting strings to uppercase.

   ```javascript
   const words = ["hello", "world"];
   const uppercaseWords = words.map((word) => word.toUpperCase());
   // Output: ["HELLO", "WORLD"]
   ```

2. **Extracting Properties**:

   - If you have an array of objects, you can use `map` to extract a specific property from each object.

   ```javascript
   const users = [
     { name: "Alice", age: 25 },
     { name: "Bob", age: 30 },
     { name: "Charlie", age: 35 }
   ];
   const names = users.map((user) => user.name);
   // Output: ["Alice", "Bob", "Charlie"]
   ```

3. **Mapping Numbers to Strings**:

   - `map` is helpful for formatting or transforming numeric data, such as converting an array of numbers into an array of strings with specific units.

   ```javascript
   const prices = [5, 10, 15];
   const formattedPrices = prices.map((price) => `$${price}`);
   // Output: ["$5", "$10", "$15"]
   ```

4. **Creating HTML Elements (useful in React)**:

   - In frameworks like React, `map` is often used to render lists of components based on an array of data.

   ```javascript
   const items = ["Item 1", "Item 2", "Item 3"];
   const itemList = items.map((item) => `<li>${item}</li>`);
   // Output: ["<li>Item 1</li>", "<li>Item 2</li>", "<li>Item 3</li>"]
   ```

5. **Complex Transformations**:

   - `map` can apply more complex transformations that involve modifying each element’s structure.

   ```javascript
   const numbers = [1, 2, 3];
   const objects = numbers.map((num) => ({ value: num, doubled: num * 2 }));
   // Output: [{ value: 1, doubled: 2 }, { value: 2, doubled: 4 }, { value: 3, doubled: 6 }]
   ```

---

## Key Points about `map`

- **Non-mutative**: `map` doesn’t change the original array; it returns a new one.
- **One-to-one Transformation**: `map` always returns an array of the same length as the original.
- **Functional Programming**: `map` is widely used in functional programming for its simplicity and declarative nature, making code cleaner and often easier to understand.

The `map` function is especially useful when you need to work with data in a specific format or make similar modifications to each element in a list.
