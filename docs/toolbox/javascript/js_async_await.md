---
title: Async/Await
description: Using Async/Await in JavaScript
layout: default
nav_order: 14
parent: JavaScript
grand_parent: Toolbox
has_children: false
permalink: /toolbox/javascript/async-await
---

# Async / Await

`async` and `await` are keywords in JavaScript that help you work with asynchronous code in a more readable and manageable way. They allow you to write asynchronous code that looks like synchronous code, making it easier to read and understand. Here’s a breakdown of how they work:

## `async` Function

An `async` function is a function that always returns a `Promise`. By declaring a function as `async`, you are signaling that it contains asynchronous code and may rely on data that is not immediately available.

```javascript
async function fetchData() {
  return 'Data fetched!';
}

fetchData().then(data => console.log(data)); // Logs "Data fetched!"
```

In this example:

- `fetchData` is declared with `async`, so it automatically returns a `Promise`, even though it returns a plain string.
- The returned `Promise` resolves to `"Data fetched!"`, which can then be handled with `.then()`.

## `await` Keyword

The `await` keyword is used inside an `async` function and pauses the execution of the function until the `Promise` is resolved. Once the promise is resolved, `await` returns the resolved value, and the function continues to execute.

### Example

```javascript
async function fetchData() {
  const response = await fetch('https://api.example.com/data');
  const data = await response.json();
  console.log(data);
}

fetchData();
```

In this example:

- The `await` keyword pauses the execution of `fetchData` until `fetch` completes its request to `https://api.example.com/data`.
- Once the `fetch` promise is resolved, the response is processed, and `await response.json()` pauses execution again until the `json()` promise resolves.
- Finally, the data is logged to the console.

## Benefits of `async` and `await`

Using `async` and `await` provides several benefits over using `.then()` and `.catch()`:

1. **Readability**: Code reads top-to-bottom, making it look synchronous and easier to follow.
2. **Error Handling**: You can use `try...catch` blocks to handle errors more cleanly.
3. **Chaining**: `await` allows you to perform asynchronous operations in sequence without excessive nesting.

## Error Handling with `try...catch`

One of the main advantages of `async`/`await` is that you can handle errors in a more intuitive way using `try...catch` blocks.

```javascript
async function fetchData() {
  try {
    const response = await fetch('https://api.example.com/data');
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error('Error fetching data:', error.message);
  }
}

fetchData();
```

In this example:

- `try...catch` catches any errors that occur during the execution of the `await`ed code, whether it's a network error or an unexpected HTTP status.
- If an error occurs, it’s handled in the `catch` block, keeping error handling concise and organized.

## Parallel Asynchronous Operations with `await`

When you need to perform multiple asynchronous operations that don't depend on each other, you can run them in parallel using `Promise.all()` with `await`.

```javascript
async function fetchMultipleData() {
  const [data1, data2] = await Promise.all([
    fetch('https://api.example.com/data1').then(res => res.json()),
    fetch('https://api.example.com/data2').then(res => res.json())
  ]);
  console.log(data1, data2);
}

fetchMultipleData();
```

## Summary

- **`async` functions**: Always return a `Promise` and signal that the function contains asynchronous code.
- **`await`**: Pauses function execution until a `Promise` is resolved, returning the resolved value.
- **Error Handling**: Use `try...catch` for easier error handling within `async` functions.
- **Parallel Execution**: Use `Promise.all()` with `await` to run multiple asynchronous operations in parallel.

This approach provides a more readable, manageable, and error-resistant way to handle asynchronous operations in JavaScript.
