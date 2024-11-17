---
title: Learning Objectives
description: React part 2 Learning Objectives
layout: default
nav_order: 1
has_children: false
parent: React II
permalink: /frontend/react-2/learningobjectives/
---

# Learning Objectives

## Week2: JS and React continued

### Day I

1. **useState**

- What is the purpose of the useState hook?
- How can you update a useState variable - and what happens as a result?
- Show how to implement useState
- Show how to initialize a useState variable with a value
- Show how to view the useState variable in jsx

2. **Props**

- What is the purpose of props?
- What can be communicated through props?
- Show how to use props
- Show how to extract props in a component by destructuring

3. **Lists and keys**

- Show how to create dynamic lists and rows in a table in react
- Show how to insert keys for each list item / row
- Explain why keys are necessary in React
- Show how to generate random keys and explain when to use them

4. **useEffect**

- Explain the purpose of the useEffect hook
- Show some examples of using the useEffect
- What is the purpose of the dependency array `[]` and `[state]`
- How do you clean up after things that might have been initiated in a useEffect, but should no longer be running?

### 5. Lifting State

- **Explain:** The concept of lifting state to share data between parent and child components.
- **Show how to:** Pass callback functions as props to update shared state.
- **Explain:** The implications of prop drilling and strategies to minimize its impact.
- **Explain:** The benefits of lifting state, such as improved maintainability and data consistency.

### Day II

### 1. Reacting to Input

- **Show how to:** Capture and handle user input events, such as clicks and keystrokes.
- **Show how to:** Update React component state based on user input.
- **Show how to:** Conditionally render content based on user interactions.
- **Explain:** The properties of event objects and how they can be utilized in event handlers.
- **Show how to:** Implement basic input validation for an enhanced user experience.

### 2. Controlled Forms/Components

- **Explain:** The concept of controlled components and their advantages.
- **Show how to:** Bind form elements to React state for controlled behavior.
- **Show how to:** Handle form submissions in React and prevent default form behavior.
- **Show how to:** Implement form validation in controlled components.
- **Show how to:** Handle and display errors in controlled forms for a user-friendly experience.


### 3. Simple CRUD

- **Explain:** The fundamental CRUD operations (Create, Read, Update, Delete).
- **Show how to:** Manage data within a React application for CRUD operations.
- **Show how to:** Implement creating new items or records in the application.
- **Show how to:** Update existing data based on user interactions.
- **Show how to:** Delete items or records from the application.

### 4. Fetching Data from Mock API server
- **Explain:** The concept of fetching data from an API server.
- **Show how to:** Setup a mock API server using JSON server.
- **Show how to:** Do CRUD operations on data from the mock API server