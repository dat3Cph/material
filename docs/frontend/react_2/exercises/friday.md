---
title: CRUD Students and Classes
description: Exercise for practicing React and CRUD operations with json-server
layout: default
nav_order: 7
grand_parent: React II
parent: Exercises
permalink: /frontend/react-2/exercises/students-classes
---

# React CRUD: Students and Classes

In this exercise, you will create a **React Application** to manage **Students** and their **Classes**. The application will:

1. Fetch data about students and their classes from a mock API powered by `json-server`.
2. Display a list of students and their assigned classes.
3. Allow users to perform `CRUD` operations (Create, Read, Update, Delete) on the data.

## Objectives

- **GET**: Fetch and display students and classes.
- **POST**: Add new students.
- **PUT**: Update existing student information.
- **DELETE**: Remove students from the list.
- Utilize **json-server** for backend mock data.

## Steps to Complete the Exercise

### Step 1: Set Up Your React Application

Use [Vite](../../../toolbox/react/vite.md) to create, and then remove irrelevant code from the source code.

### Step 2: Set Up `json-server`

1. **Install `json-server` in the project:**

```bash
npm install json-server --save-dev
```

2. **Create a `db.json` file** in a new `data` folder with the following content:

```json
{
  "students": [
    {
      "id": 1,
      "name": "Alice",
      "age": 20,
      "email": "alice@example.com",
      "classes": [1,2]
    },
    {
      "id": 2,
      "name": "Bob",
      "age": 20,
      "email": "bob@example.com",
      "classes": [1,2]
    },
    {
      "id": 3,
      "name": "Charlize",
      "age": 20,
      "email": "char@example.com",
      "classes": [2]
    },
    {
      "id": 4,
      "name": "Eric",
      "age": 22,
      "email": "eric@example.com",
      "classes": [1]
    }
  ],
  "classes": [
    {
      "id": 1,
      "name": "Math 101",
      "teacher": "Mr. Smith"
    },
    {
      "id": 2,
      "name": "History 201",
      "teacher": "Mrs. Johnson"
    }
  ]
}
```

Add a script to `package.json` to run the JSON server:

```json
"scripts": {
  "jsonserver": "json-server --watch data/db.json --port 3000"
}
```

### Step 3: Creating the Components

- The PersonForm Component. Use below code as inspiration (replace the select options with the actual classes fetched from the API):

```html
<form>
  <label htmlFor="id">Id</label>
  <input id="id" type="number" readOnly placeholder="id" />
  <label htmlFor="name">Name</label>
  <input id="name" type="text" placeholder="Enter name" />
  <label htmlFor="age">Age</label>
  <input id="age" type="number" min="1" max="120" placeholder="Enter age" />
  <label htmlFor="email">Email</label>
  <input id="email" type="email" placeholder="Enter email" />
  <label htmlFor="class">Class</label>
  <select id="class">
    <option value="Math 101">Math 101</option>
    <option value="History 201">History 201</option>
  </select>
</form>
```
- See if you can find a way to be able to add multiple classes to a student.

- StudentList Component should contain a table with the following structure:

```html
<table>
  <thead>
    <tr>
      <th>Id</th>
      <th>Name</th>
      <th>Age</th>
      <th>Email</th>
      <th>Classes</th>
      <th>Actions</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>Alice</td>
      <td>20</td>
      <td>alice@example.com</td>
      <td>Math 101, History 201</td>
      <td>
        <button>Edit</button>
        <button>Delete</button>
      </td>
    </tr>
  </tbody>
</table>
```
- In the above structure, the classes should be displayed as a comma-separated list of classes attained by the student.


### Step 4: Setting Up Fetch Functions

- Create a utils folder and add a fetchData.js file:

```jsx
export function fetchData(url, callback, method, body) {
  const headers = {
    'Accept': 'application/json',
  };

  if (method === 'POST' || method === 'PUT') {
    headers['Content-Type'] = 'application/json';
  }

  const options = {
    method,
    headers,
  };

  if (body) {
    options.body = JSON.stringify(body);
  }

  fetch(url, options)
    .then((res) => res.json())
    .then((data) => callback(data))
    .catch((err) => {
      if (err.status) {
        err.fullError.then((e) => console.log(e.detail));
      } else {
        console.log("Network error");
      }
    });
}
```

### Step 5: Fetching and Displaying Data

- In your main App.js file, use the fetchData function to display students:

### Step 6: Creating CRUD Operations

- Adding a Student (POST)
- Updating a Student (PUT)
- Deleting a Student (DELETE)
- Adding a class to a student (PATCH)

### Step 7: Styling Your Application

- Use CSS to style your application, and make it nice and easy to use.
