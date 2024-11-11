---
title: Spread Operator
description: How the spread operator works in JavaScript
layout: default
nav_order: 9
parent: JavaScript
grand_parent: Toolbox
has_children: false
permalink: /toolbox/javascript/spread-operator
---

# Spread Operator in JavaScript

Certainly! The **spread operator** (`...`) in JavaScript is a versatile syntax used to unpack (or "spread") the elements of an array, the properties of an object, or even arguments in function calls. It makes it easy to work with collections and creates clean, readable code, especially for copying, merging, and passing values.

## How the Spread Operator Works

The spread operator essentially "spreads" the contents of an array or object into individual elements or properties. The usage depends on the context:

1. **With arrays**: It spreads array elements.
2. **With objects**: It spreads object properties.
3. **With functions**: It spreads elements as individual arguments.

## Spread Operator with Arrays

### 1. Copying Arrays

Using the spread operator, you can create a shallow copy of an array.

```javascript
const numbers = [1, 2, 3];
const copy = [...numbers];

console.log(copy); // Output: [1, 2, 3]
```

This method copies each element of the `numbers` array into a new array, `copy`. Changes to `copy` won’t affect `numbers`, and vice versa.

### 2. Merging Arrays

The spread operator makes it easy to combine arrays.

```javascript
const first = [1, 2];
const second = [3, 4];
const combined = [...first, ...second];

console.log(combined); // Output: [1, 2, 3, 4]
```

Here, `[...first, ...second]` merges the two arrays by spreading the elements of `first` and `second` into a new array.

### 3. Adding or Removing Elements in Arrays

You can add elements at any position in an array using the spread operator.

```javascript
const numbers = [2, 3];
const newArray = [1, ...numbers, 4];

console.log(newArray); // Output: [1, 2, 3, 4]
```

In this example, `1` and `4` are added before and after `...numbers`, respectively.

## Spread Operator with Objects

The spread operator can also copy and merge objects by spreading their properties into new objects.

### 1. Copying Objects

Using the spread operator, you can create a shallow copy of an object.

```javascript
const person = { name: "Alice", age: 25 };
const copy = { ...person };

console.log(copy); // Output: { name: "Alice", age: 25 }
```

This approach copies each property of `person` into `copy`. Similar to arrays, this is a **shallow copy**, so nested objects aren’t deeply copied.

### 2. Merging Objects

You can merge objects by spreading their properties into a new object.

```javascript
const details = { age: 25, city: "New York" };
const contact = { email: "alice@example.com" };
const merged = { ...details, ...contact };

console.log(merged); // Output: { age: 25, city: "New York", email: "alice@example.com" }
```

In this example, `...details` and `...contact` spread their properties into `merged`, resulting in a single merged object.

### 3. Overriding Properties

When merging objects, if properties overlap, the latter object’s properties override the previous ones.

```javascript
const person = { name: "Alice", age: 25 };
const updatedPerson = { ...person, age: 26 };

console.log(updatedPerson); // Output: { name: "Alice", age: 26 }
```

Here, `{ ...person, age: 26 }` copies `person` but overrides `age` with the new value `26`.

## Spread Operator with Functions

When used in function calls, the spread operator allows you to pass an array of arguments as individual parameters.

### Example: Passing Array Elements as Arguments

```javascript
const numbers = [1, 2, 3];

function sum(a, b, c) {
  return a + b + c;
}

console.log(sum(...numbers)); // Output: 6
```

In this example, `...numbers` spreads the array `[1, 2, 3]` so that each element is passed as an individual argument to `sum`, equivalent to calling `sum(1, 2, 3)`.

### Example: Using Spread with Math Functions

The spread operator is handy when you want to pass an array to a function that expects multiple arguments, like `Math.max`.

```javascript
const scores = [89, 76, 95, 82];
const highestScore = Math.max(...scores);

console.log(highestScore); // Output: 95
```

Here, `Math.max(...scores)` spreads `scores` as individual arguments to `Math.max`, which finds the highest score.

## Practical Use Cases for the Spread Operator

1. **Copying and Cloning**: Quickly create shallow copies of arrays or objects.
2. **Merging Data**: Combine multiple arrays or objects into a single array or object.
3. **Adding Elements to Arrays**: Add new elements at the beginning, middle, or end of an array.
4. **Converting NodeLists to Arrays**: Convert `NodeList` or `arguments` objects to arrays for array methods.

   ```javascript
   const listItems = document.querySelectorAll("li");
   const itemsArray = [...listItems]; // Now `itemsArray` is an array
   ```

5. **Function Arguments**: Pass elements of an array as individual arguments to a function.

## Important Points to Remember

- **Shallow Copy**: The spread operator only creates a shallow copy. For nested objects or arrays, only the top-level properties are copied, while nested objects or arrays are still referenced.
- **Overriding Properties**: When spreading objects, later properties in the spread order will override earlier ones if there are conflicts.
- **Usage Context**: The spread operator cannot be used everywhere (e.g., it works with arrays and objects but not with numbers or strings directly, unless they are part of an array or object structure).

## Summary

- **Arrays**: Use the spread operator to copy arrays, merge them, and add or remove elements.
- **Objects**: Use it to copy objects, merge them, and override specific properties.
- **Functions**: Use it to spread array elements as individual arguments when calling a function.

The spread operator is a powerful and concise tool in JavaScript, helping you manage collections of data with cleaner and more readable syntax.
