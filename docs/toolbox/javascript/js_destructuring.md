---
title: Destructuring
description: How destructuring works in JavaScript
layout: default
nav_order: 8
parent: JavaScript
grand_parent: Toolbox
has_children: false
permalink: /toolbox/javascript/destructuring
---

# Destructuring in JavaScript

In JavaScript, **destructuring** is a convenient way to extract values from arrays and properties from objects into distinct variables. This syntax allows for cleaner, more readable code, especially when working with complex data structures.

## Array Destructuring

Array destructuring lets you unpack values from an array into separate variables based on their positions in the array.

### Basic Example

```javascript
const colors = ["red", "green", "blue"];

// Destructure the array into individual variables
const [firstColor, secondColor, thirdColor] = colors;

console.log(firstColor);  // Output: "red"
console.log(secondColor); // Output: "green"
console.log(thirdColor);  // Output: "blue"
```

In this example, `firstColor`, `secondColor`, and `thirdColor` take the values at the respective positions in the `colors` array.

### Skipping Elements

You can skip elements in the array by leaving empty slots.

```javascript
const numbers = [1, 2, 3, 4, 5];

// Only take the first and third elements
const [first, , third] = numbers;

console.log(first);  // Output: 1
console.log(third);  // Output: 3
```

### Using Rest with Destructuring

You can use the **rest operator** (`...`) to gather the remaining elements into a new array.

```javascript
const numbers = [1, 2, 3, 4, 5];

// Destructure the first two elements and gather the rest
const [first, second, ...rest] = numbers;

console.log(first);  // Output: 1
console.log(second); // Output: 2
console.log(rest);   // Output: [3, 4, 5]
```

### Default Values

You can assign default values in case the array doesn’t contain enough elements.

```javascript
const numbers = [10];

// Destructure with default values
const [a = 1, b = 2, c = 3] = numbers;

console.log(a);  // Output: 10
console.log(b);  // Output: 2
console.log(c);  // Output: 3
```

## Object Destructuring

Object destructuring allows you to extract properties from an object and assign them to variables with the same names as the object’s keys.

### Basic Example

```javascript
const person = {
  name: "Alice",
  age: 25,
  city: "New York"
};

// Destructure the object
const { name, age, city } = person;

console.log(name); // Output: "Alice"
console.log(age);  // Output: 25
console.log(city); // Output: "New York"
```

In this example, `name`, `age`, and `city` are assigned the values of the corresponding properties in the `person` object.

### Using Different Variable Names

You can rename variables during destructuring by using a colon (`:`).

```javascript
const person = {
  name: "Alice",
  age: 25,
  city: "New York"
};

// Destructure with renaming
const { name: personName, age: personAge } = person;

console.log(personName); // Output: "Alice"
console.log(personAge);  // Output: 25
```

Here, `personName` and `personAge` are the new variable names, and they take the values of `name` and `age` from the object.

### Default Values

You can assign default values to variables if the property doesn’t exist in the object.

```javascript
const person = {
  name: "Alice",
  age: 25
};

// Destructure with default values
const { name, city = "Unknown" } = person;

console.log(name); // Output: "Alice"
console.log(city); // Output: "Unknown"
```

### Nested Destructuring

For objects with nested structures, you can destructure deeply.

```javascript
const user = {
  id: 1,
  info: {
    name: "Alice",
    address: {
      city: "New York",
      zip: "10001"
    }
  }
};

// Destructure nested properties
const {
  info: {
    name,
    address: { city, zip }
  }
} = user;

console.log(name); // Output: "Alice"
console.log(city); // Output: "New York"
console.log(zip);  // Output: "10001"
```

### Using Rest with Object Destructuring

You can use the rest operator to collect remaining properties into a new object.

```javascript
const person = {
  name: "Alice",
  age: 25,
  city: "New York"
};

// Destructure with rest operator
const { name, ...rest } = person;

console.log(name); // Output: "Alice"
console.log(rest); // Output: { age: 25, city: "New York" }
```

## Practical Examples

### Function Parameters with Destructuring

Destructuring can be particularly useful for function parameters, allowing you to pass an object and immediately extract values.

```javascript
function greet({ name, age }) {
  console.log(`Hello, ${name}! You are ${age} years old.`);
}

const person = {
  name: "Alice",
  age: 25
};

greet(person); // Output: "Hello, Alice! You are 25 years old."
```

### Swapping Variables with Array Destructuring

Array destructuring provides a simple way to swap variables without a temporary variable.

```javascript
let a = 1;
let b = 2;

[a, b] = [b, a];

console.log(a); // Output: 2
console.log(b); // Output: 1
```

## Summary

- **Array destructuring** is position-based and is ideal for extracting elements based on index.
- **Object destructuring** is key-based and allows you to extract values based on property names.
- You can use **default values**, **renaming**, **nested destructuring**, and the **rest operator** with both array and object destructuring.
- Destructuring is helpful in simplifying function parameters and makes code more readable, especially when dealing with complex data structures.
