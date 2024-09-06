---
title: JSON
description: Example of a JSON object and array
layout: default
parent: Data Integration
grand_parent: Toolbox
nav_order: 2
permalink: /toolbox/dataintegration/json/
---


# What is JSON?

**JSON** (JavaScript Object Notation) is a lightweight data-interchange format that's easy for humans to read and write, as well as simple for machines to parse and generate. It is commonly used for transmitting data in web applications between a server and a client.

### Characteristics of JSON

1. **Data Format:** Text-based format that represents data as key-value pairs.
2. **Language-Independent:** While originally based on JavaScript, JSON is language-independent and supported by most programming languages.
3. **Structure:** It uses two main structures:
   - A collection of key-value pairs (often called an object, represented by curly braces `{}`).
   - An ordered list of values (often called an array, represented by square brackets `[]`).

### Basic Syntax of JSON

- Data is represented in key-value pairs.
- Keys are strings (enclosed in double quotes) and are followed by a colon `:`.
- Values can be strings, numbers, arrays, objects, or boolean values (`true`, `false`), or null.
- Objects are enclosed in curly braces `{}`.
- Arrays are enclosed in square brackets `[]`.
- Elements in arrays and key-value pairs in objects are separated by commas.

### Example of a JSON object

```json
{
  "name": "Alice",
  "age": 30,
  "isStudent": false,
  "courses": ["Math", "Computer Science"],
  "address": {
    "street": "123 Main St",
    "city": "New York",
    "postalCode": "10001"
  }
}
```

### Example of a JSON array

```json
[
  { "name": "Alice", "age": 30 },
  { "name": "Bob", "age": 25 },
  { "name": "Charlie", "age": 35 }
]
```

### Common Use Cases of JSON

1. **Web APIs:** JSON is widely used in [RESTful APIs](./rest_api.md) to transmit data between the server and client in web applications.

   - Example: When fetching data from a web server using JavaScript (e.g., `fetch()` or `XMLHttpRequest`), the data is often returned in JSON format.

   Example of a response from a REST API:

   ```json
   {
     "status": "success",
     "data": {
       "userId": 12345,
       "username": "john_doe",
       "email": "john@example.com"
     }
   }
   ```

2. **Configuration Files:** Many applications use JSON for configuration files (e.g., Node.js uses `package.json` to store project metadata and dependencies).

   ```json
   {
     "name": "my-app",
     "version": "1.0.0",
     "dependencies": {
       "express": "^4.17.1",
       "mongoose": "^5.9.10"
     }
   }
   ```

3. **Storing Data in Databases:** Some NoSQL databases like MongoDB store data in a format similar to JSON (BSON - Binary JSON), allowing for easy retrieval and storage of complex objects.

4. **Data Serialization:** JSON is commonly used to serialize data for communication between services, or for local storage (e.g., browser’s `localStorage` or `sessionStorage`).

JSON has become a standard format for data exchange across modern web and mobile applications because of its simplicity and readability.
