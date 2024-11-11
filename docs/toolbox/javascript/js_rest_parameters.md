---
title: Rest Parameters
description: How the rest parameters works in JavaScript
layout: default
nav_order: 10
parent: JavaScript
grand_parent: Toolbox
has_children: false
permalink: /toolbox/javascript/rest-parameters
---

# Rest Parameters in JavaScript

The **rest parameter** in JavaScript allows you to collect multiple elements or arguments into an array. It’s represented by three dots (`...`) followed by a parameter name, and it can be useful for handling a variable number of arguments or for collecting “the rest” of the elements in array or object destructuring.

## How the Rest Parameter Works

The rest parameter (`...`) collects "the rest" of the values. It can only be used in function parameters and in destructuring assignments.

## 1. Using the Rest Parameter in Functions

When used in function parameters, the rest parameter collects all additional arguments passed to the function into an array. This is especially useful when you don’t know how many arguments a function will receive.

### Example: Collecting Extra Arguments

```javascript
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(1, 2, 3));       // Output: 6
console.log(sum(10, 20, 30, 40)); // Output: 100
```

In this example:

- `sum` takes a rest parameter `...numbers`, which collects all arguments into an array called `numbers`.
- This array can then be used within the function (e.g., in `reduce` to calculate the sum).

### Example: Named Parameters with Rest Parameter

You can combine regular parameters with the rest parameter, but the rest parameter must always be the **last parameter**.

```javascript
function introduce(firstName, lastName, ...titles) {
  console.log(`Name: ${firstName} ${lastName}`);
  console.log(`Titles: ${titles.join(", ")}`);
}

introduce("Alice", "Smith", "Engineer", "Author", "Musician");
// Output:
// Name: Alice Smith
// Titles: Engineer, Author, Musician
```

Here:

- `firstName` and `lastName` are regular parameters.
- `...titles` collects any additional arguments into an array, which is used to list all titles.

## 2. Using the Rest Parameter in Array Destructuring

In array destructuring, the rest parameter can collect the remaining elements into a new array after specific elements are extracted.

### Example: Destructuring with Rest in Arrays

```javascript
const colors = ["red", "green", "blue", "yellow"];

const [first, second, ...remainingColors] = colors;

console.log(first);           // Output: "red"
console.log(second);          // Output: "green"
console.log(remainingColors); // Output: ["blue", "yellow"]
```

In this example:

- `first` and `second` capture the first two elements.
- `...remainingColors` collects the rest of the elements into a new array.

## 3. Using the Rest Parameter in Object Destructuring

With object destructuring, the rest parameter can collect any remaining properties into a new object.

### Example: Destructuring with Rest in Objects

```javascript
const person = { name: "Alice", age: 25, city: "New York", profession: "Engineer" };

const { name, age, ...details } = person;

console.log(name);   // Output: "Alice"
console.log(age);    // Output: 25
console.log(details); // Output: { city: "New York", profession: "Engineer" }
```

In this example:

- `name` and `age` are extracted as individual variables.
- `...details` collects all remaining properties (i.e., `city` and `profession`) into a new object.

## Important Points to Remember

1. **Rest Parameter Placement**: The rest parameter must always be the last parameter in function definitions and destructuring assignments.
2. **Rest in Functions**: It collects all remaining arguments into an array, making it useful for functions with a variable number of arguments.
3. **Rest in Destructuring**: It allows you to gather remaining elements or properties after specific ones have been extracted.

## Practical Use Cases for the Rest Parameter

1. **Handling Variable Arguments in Functions**: Easily accept an unknown number of arguments in functions like `sum`, `average`, or logging utilities.
2. **Collecting Remaining Array Elements**: When you only need specific items from an array, you can use rest to collect the rest, simplifying access to remaining items.
3. **Cloning and Merging Objects**: When copying objects or removing properties, the rest parameter makes it easy to create new objects without certain keys.

## Summary

- The **rest parameter** (`...`) collects multiple elements into an array in functions, or collects remaining properties or elements in destructuring.
- In **functions**, it allows you to handle an arbitrary number of arguments by collecting them into an array.
- In **array and object destructuring**, it gathers the remaining elements or properties into a new array or object, respectively.

The rest parameter is a powerful tool for handling dynamic or flexible data structures, making your code cleaner and more readable.
