---
title: React CRUD with Students and Classes
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

Run the following commands to create and start your React project:

```bash
npx create-react-app student-class-app cd student-class-app
```

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
      "class": [1,2]
    },
    {
      "id": 2,
      "name": "Bob",
      "age": 20,
      "email": "bob@example.com",
      "class": [1,2]
    },
    {
      "id": 3,
      "name": "Charlize",
      "age": 20,
      "email": "char@example.com",
      "class": [2]
    },
    {
      "id": 4,
      "name": "Eric",
      "age": 22,
      "email": "eric@example.com",
      "class": [1]
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

Add a script to package.json to run the JSON server:

```json
"scripts": {
  "jsonserver": "json-server --watch data/db.json --port 3000 --host 127.0.0.1"
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

- PersonList Component

<table>
  <thead>
    <tr>
      <th>Id</th>
      <th>Name</th>
      <th>Age</th>
      <th>Email</th>
      <th>Class</th>
      <th>Actions</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>Alice</td>
      <td>20</td>
      <td>alice@example.com</td>
      <td>Math 101</td>
      <td>
        <button>Edit</button>
        <button>Delete</button>
      </td>
    </tr>
  </tbody>
</table>
```

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

In your main App.js file, use the fetchData function to display students:

```jsx
import React, { useState, useEffect } from 'react';
import { fetchData } from './utils/fetchData';

function App() {
  const [students, setStudents] = useState([]);

  useEffect(() => {
    fetchData('/api/students', setStudents, 'GET');
  }, []);

  return (
    <div>
      <h1>Students List</h1>
      <PersonList students={students} />
    </div>
  );
}

export default App;
```

### Step 6: Creating CRUD Operations
- Adding a Student (POST)

- Create a function to add a new student:

const newStudent = {
  name: "Charlie",
  age: 19,
  email: "charlie@example.com",
  class: "Math 101"
};

```jsx
fetchData('/api/students', setStudents, 'POST', newStudent);
```

- Updating a Student (PUT)

- Update the student data like this:

```jsx
const updatedStudent = {
  name: "Alice",
  age: 21,
  email: "alice_updated@example.com",
  class: "History 201"
};

fetchData('/api/students/1', setStudents, 'PUT', updatedStudent);
```

- Deleting a Student (DELETE)

- Delete a student using this method:

```jsx
fetchData('/api/students/1', setStudents, 'DELETE');
```

### Step 7: Styling Your Application
- Use CSS (or a CSS framework like Bootstrap or Tailwind) to style your application.


