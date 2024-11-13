---
title: Promises
description: Using Promises in JavaScript
layout: default
nav_order: 12
parent: JavaScript
grand_parent: Toolbox
has_children: false
permalink: /toolbox/javascript/promises
---

# Promises in JavaScript

In JavaScript, a **Promise** is an object representing the eventual completion or failure of an asynchronous operation and its resulting value. Promises help manage asynchronous tasks (such as fetching data from an API) by allowing you to handle success or failure after the operation completes. They prevent the need for deeply nested callbacks (known as "callback hell") and offer a more streamlined syntax for asynchronous code.

## How Promises Work

A Promise has three possible states:

1. **Pending**: The initial state, where the Promise has been created but the operation hasn’t completed yet.
2. **Fulfilled (Resolved)**: The operation completed successfully, and the Promise has a resulting value.
3. **Rejected**: The operation failed, and the Promise has an error reason.

Once a Promise is fulfilled or rejected, it remains in that state and cannot change.

## Creating a Promise

You create a Promise by using the `new Promise` constructor, which accepts a function (executor) with two parameters, `resolve` and `reject`. You use `resolve` to mark the Promise as fulfilled and `reject` to mark it as rejected.

```javascript
const myPromise = new Promise((resolve, reject) => {
  let success = true;
  
  if (success) {
    resolve("Operation was successful!");
  } else {
    reject("Operation failed.");
  }
});
```

In this example:

- The Promise checks the `success` condition.
- If `success` is true, `resolve` is called, which completes the Promise successfully with the value `"Operation was successful!"`.
- If `success` is false, `reject` is called, which completes the Promise with an error message.

## Consuming Promises

You handle a Promise’s success or failure by chaining `.then()` and `.catch()` methods to the Promise.

### `.then()` for Success

The `.then()` method is called when the Promise is fulfilled. It takes a function that receives the result as an argument.

```javascript
myPromise.then(result => {
  console.log(result); // Logs "Operation was successful!" if resolved
});
```

### `.catch()` for Errors

The `.catch()` method is called if the Promise is rejected. It takes a function that receives the error message.

```javascript
myPromise
  .then(result => {
    console.log(result); // Only runs if the Promise is resolved
  })
  .catch(error => {
    console.error(error); // Only runs if the Promise is rejected
  });
```

### `.finally()` for Cleanup

The `.finally()` method is called after the Promise is settled (either fulfilled or rejected), useful for cleanup actions.

```javascript
myPromise
  .then(result => {
    console.log(result);
  })
  .catch(error => {
    console.error(error);
  })
  .finally(() => {
    console.log("Operation complete"); // Runs no matter the outcome
  });
```

## Chaining Promises

You can chain multiple `.then()` calls to perform sequential asynchronous operations, with each `.then()` receiving the result of the previous one.

```javascript
myPromise
  .then(result => {
    console.log(result);
    return "Next step"; // Passes "Next step" to the next `.then()`
  })
  .then(nextResult => {
    console.log(nextResult); // Logs "Next step"
  })
  .catch(error => {
    console.error(error);
  });
```

## Using `Promise.all` for Parallel Operations

`Promise.all()` allows you to execute multiple Promises in parallel. It waits until all Promises in an array are fulfilled, or it fails if any of them are rejected.

```javascript
const promise1 = Promise.resolve("First");
const promise2 = Promise.resolve("Second");
const promise3 = Promise.resolve("Third");

Promise.all([promise1, promise2, promise3])
  .then(results => {
    console.log(results); // Logs ["First", "Second", "Third"]
  })
  .catch(error => {
    console.error(error); // Only runs if any of the Promises are rejected
  });
```

## Summary

- **Creation**: A Promise is created with `new Promise((resolve, reject) => { ... })`.
- **Handling**: Use `.then()` for successful completion, `.catch()` for errors, and `.finally()` for cleanup.
- **Chaining**: Promises can be chained for sequential asynchronous tasks.
- **Parallel Execution**: Use `Promise.all()` for running multiple asynchronous operations concurrently.

Promises simplify managing asynchronous code by providing clear, organized handling of success, error, and cleanup scenarios.
