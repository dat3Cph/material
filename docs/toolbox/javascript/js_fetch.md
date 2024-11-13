---
title: Fetch
description: How to fetch endpoints in JavaScript
layout: default
nav_order: 13
parent: JavaScript
grand_parent: Toolbox
has_children: false
permalink: /toolbox/javascript/fetch
---

# Fetching data from APIs

The `fetch` API in JavaScript is a modern way to make HTTP requests, providing a flexible and more powerful alternative to `XMLHttpRequest`. It returns a `Promise` that resolves to the `Response` object, representing the result of the request.

Here’s a basic overview of how `fetch` works and how to add headers:

## Basic Syntax

The `fetch` function accepts two main arguments:

1. **URL** – The endpoint you’re requesting.
2. **Options** – An optional configuration object that lets you customize the request, like setting the HTTP method, headers, body, etc.

## Basic Example

```javascript
fetch('https://api.example.com/data')
  .then(response => response.json()) // parse the JSON from the response
  .then(data => console.log(data))   // work with the data
  .catch(error => console.error('Error:', error)); // handle any errors
```

In this example:

- `fetch` requests data from the given URL.
- `response.json()` extracts the JSON body content.
- `.catch()` handles any network errors that occur during the request.

## Adding Headers

Headers are metadata you send along with the request to provide information like authentication tokens, content type, etc. They are specified in the `headers` property of the options object.

###

 Example with Headers

```javascript
fetch('https://api.example.com/data', {
  method: 'GET', // or POST, PUT, DELETE, etc.
  headers: {
    'Content-Type': 'application/json',      // specify the content type
    'Authorization': 'Bearer your-token-here' // include an authorization token
  }
})
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('Fetch error:', error));
```

## Important Headers and Options

- **Content-Type**: Tells the server the type of data you’re sending, such as `'application/json'`.
- **Authorization**: Often used to include tokens for protected routes.
- **Accept**: Specifies the type of response data the client expects (e.g., `'application/json'`).

## Sending Data with `fetch`

When sending data, such as in a POST request, you typically include the `body` option with a stringified JSON object and set the `Content-Type` to `application/json`:

```javascript
fetch('https://api.example.com/submit', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer your-token-here'
  },
  body: JSON.stringify({ name: 'John', age: 30 }) // data to send in request
})
  .then(response => response.json())
  .then(data => console.log('Response:', data))
  .catch(error => console.error('Fetch error:', error));
```

## Common Errors and Handling

1. **Network Errors**: The `catch` block handles network errors that prevent `fetch` from completing.
2. **Response Status**: Even if the network request succeeds, the response might indicate a failure (e.g., a 404 or 500 status). Check `response.ok` or `response.status` to handle these cases.

To handle `response.ok` and `response.status` in a `fetch` request, you typically want to check these properties to determine whether the request was successful or if it returned an error. This is especially useful to handle various HTTP status codes and customize your response handling.

### Example of Handling `response.ok` and `response.status`

The `response.ok` property is a shorthand boolean that’s `true` for successful responses (status codes between 200 and 299) and `false` for other status codes. By checking `response.ok`, you can create conditional logic to handle both success and failure scenarios.

Here’s how to do it:

```javascript
fetch('https://api.example.com/data')
  .then(response => {
    // Check if the response is OK (status is 200-299)
    if (!response.ok) {
      // Handle errors here
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    // If response is OK, parse the JSON data
    return response.json();
  })
  .then(data => {
    // Process the data
    console.log('Data:', data);
  })
  .catch(error => {
    // Catch and handle any network or response errors
    console.error('Fetch error:', error.message);
  });
```

### Explanation

1. **Checking `response.ok`**:

   - If `response.ok` is `false`, we throw an error with the status code to stop further execution in the `.then()` chain.
   - This error will be caught by the `.catch()` block, where you can log or handle the error accordingly.

2. **Using `response.status`**:

   - You can use `response.status` to handle specific HTTP status codes differently. For example, you might want to handle 404 errors uniquely to show a "not found" message or handle 500 errors as server issues.

### Example Handling Specific Status Codes

```javascript
fetch('https://api.example.com/data')
  .then(response => {
    if (!response.ok) {
      if (response.status === 404) {
        throw new Error('Resource not found (404)');
      } else if (response.status === 500) {
        throw new Error('Server error (500)');
      } else {
        throw new Error(`HTTP error! status: ${response.status}`);
      }
    }
    return response.json();
  })
  .then(data => {
    console.log('Data:', data);
  })
  .catch(error => {
    console.error('Error:', error.message);
  });
```

In this example:

- **404 (Not Found)**: Displays a custom message for missing resources.
- **500 (Server Error)**: Custom message for server-related errors.
- **Other errors**: Any other status codes can be handled with a general error message.

### Summary

- Use `response.ok` to quickly determine if the request was successful.
- Use `response.status` to handle specific status codes with custom messages or actions.
- Catch errors with `.catch()` to handle both network errors and failed responses.

This approach gives you granular control over how to handle success and error cases in `fetch` requests.
