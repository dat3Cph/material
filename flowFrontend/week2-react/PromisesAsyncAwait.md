# Promises and Async/Await

## Promises

A Promise is a feature in JavaScript that represents the eventual completion (or failure) of an asynchronous operation and its resulting value.
It is a way of handling asynchronous code in a more readable and organized manner.

To explain Promises think about the following analogy: Imagine you're ordering a pizza. You call the pizza place and they tell you it will take 30 minutes
to prepare and deliver the pizza. Instead of waiting on the phone for 30 minutes, you tell the pizza place to call you back when the pizza is ready.
This is similar to how Promises work.

In JavaScript, a Promise is an object that represents the eventual completion (or failure) of an asynchronous operation.
It has three states: pending, fulfilled, or rejected. When a Promise is pending, it means that the operation is still in progress.
When a Promise is fulfilled, it means that the operation was successful and the resulting value is available. When a Promise is rejected,
it means that the operation failed and the reason for the failure is available.

To use a Promise in JavaScript, you create a new Promise object and pass in a function that contains the asynchronous operation.
This function takes two parameters: resolve and reject. When the operation is complete, you call either resolve with the resulting
value or reject with an error message.

One of the key benefits of using Promises in JavaScript is that they simplify the handling of asynchronous code. Instead of using
callbacks or nested functions, you can chain Promises together using the then method and handle errors with the catch method.
This makes the code more readable and easier to maintain.

To summarize, a Promise in JavaScript is an object that represents the eventual completion (or failure) of an asynchronous operation.
It simplifies the handling of asynchronous code and makes the code more readable and organized.

Example:

```js   
const promise = new Promise((resolve, reject) => {
  const x = "foo";
  const y = "bar";
  if (x === y) {
    resolve();
  } else {
    reject();
  }
});
promise
  .then(() => console.log("Success!"))
  .catch(() => console.log("Error!"));
```

## Async/Await

Async/await is a modern feature in JavaScript that provides a more readable and organized way to write asynchronous code.
It is built on top of Promises and allows you to write asynchronous code that looks and behaves like synchronous code.

To understand async/await, think about the following analogy: Imagine you're waiting for a bus. Normally,
you would wait at the bus stop until the bus arrives. With async/await, you can wait for the bus at home and do other things until
the bus arrives. When the bus arrives, you can go to the bus stop and catch it. This is similar to how async/await works.

In JavaScript, async/await allows you to write asynchronous code that looks and behaves like synchronous code. It uses the async
keyword to mark a function as asynchronous, and the await keyword to wait for the result of an asynchronous operation before moving on to the next line of code.

Here's an example of how to use async/await in JavaScript:

```JS
async function fetchUserData() {
  try {
    const response = await fetch('https://example.com/userdata');
    const userData = await response.json();
    console.log(userData);
  } catch (error) {
    console.log(error);
  }
}

```

In this example, the fetchUserData function is marked as asynchronous using the async keyword. Inside the function,
the await keyword is used to wait for the response of the fetch operation, and then to wait for the response to be converted to JSON format.
Finally, the userData is logged to the console.

One of the key benefits of using async/await in JavaScript is that it makes asynchronous code more readable and easier to understand.
It also makes error handling easier, as you can use try/catch blocks to handle errors in a more synchronous-like manner.

To summarize, async/await is a modern feature in JavaScript that allows you to write asynchronous code that looks and behaves like synchronous code.
It is built on top of Promises and makes asynchronous code more readable and easier to understand.

## Synchronous vs Asynchronous

In JavaScript, synchronous and asynchronous are two ways of executing code. Synchronous code is executed in sequence, one line at a time, and blocks the execution until
the current line of code is completed. Asynchronous code, on the other hand, allows other code to execute while it is waiting for a response, and does not block the execution of the program.

To understand the difference between synchronous and asynchronous you can think of the following analogy: Imagine you're at a restaurant and you order a pizza.
If the restaurant is synchronous, the chef will start making the pizza right away and will not start on another order until your pizza is done.
This means that the other orders have to wait until your pizza is ready. If the restaurant is asynchronous, the chef can start making your pizza,
but can also start making other orders while your pizza is cooking. This means that the other orders can be completed while your pizza is being made,
and the chef can come back to your pizza when it's ready.

In JavaScript, synchronous code is executed in a blocking manner, which means that the code is executed one line at a time, and the program does not continue
until the current line of code is completed. This can cause problems if the code takes a long time to execute, such as when making a network request or waiting for user input.

Asynchronous code, on the other hand, is executed in a non-blocking manner, which means that the program can continue executing while it waits for a response.
This is achieved using callbacks, promises, and async/await, which allow the program to continue executing other code while it waits for the response.

One of the key benefits of using asynchronous code in JavaScript is that it allows the program to continue executing while it waits for a response,
which can improve performance and user experience. It also makes it easier to handle complex tasks, such as making multiple network requests at once.

To summarize, synchronous code is executed in a blocking manner, which means that the program waits for each line of code to be completed before moving
on to the next. Asynchronous code, on the other hand, is executed in a non-blocking manner, which allows the program to continue executing while it
waits for a response.

Example:

```js   
// Synchronous
console.log("Hello");
console.log("World");

// Asynchronous
setTimeout(() => console.log("Hello"), 1000);
console.log("World");
```
