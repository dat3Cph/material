---
title: What is React
description: What is React?
layout: default
nav_order: 2
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/what_is_react
---
![Codelab](./images/reactlogo.png){: style="display: block; margin: 0 auto; width:50%" }

# What is React?

React.js is a JavaScript library developed by Facebook for building user interfaces, especially single-page applications where you want parts of the page to update dynamically without reloading the entire page. Here’s an explanation geared toward someone familiar with Java, HTML, CSS, and some JavaScript:

## What is React?

React is a **JavaScript library for building user interfaces**. Its main purpose is to simplify the process of creating interactive and dynamic web applications, where parts of the page update based on user interaction or changes in data.

Think of React as a tool that helps you create complex, responsive, and fast web pages without manually manipulating the HTML with JavaScript every time something needs to change.

## Key Concepts of React

1. **Components**:
   - React applications are made up of **components**, which are like building blocks. Each component represents a part of the UI (like a button, a form, or a navigation bar).
   - A component in React is similar to a **class** or **function** in Java. It encapsulates all the necessary code to render a part of the UI, including the HTML structure (using JSX), style, and behavior.
   - For example, you might have a `Header` component that displays a navigation bar, or a `ProfileCard` component that displays user information.
   - React encourages reusable components, making it easy to build complex interfaces by combining simpler components.

2. **JSX (JavaScript XML)**:
   - React uses **JSX**, a syntax that looks like HTML but is actually JavaScript. This makes it easy to write the structure of your UI in a more readable and intuitive way.
   - JSX looks like HTML but lives in JavaScript files. React then compiles this JSX code into JavaScript that the browser can understand.

   ```react
   function Greeting() {
     return <h1>Hello, world!</h1>;
   }
   ```

   Here, `<h1>Hello, world!</h1>` is written in JSX and compiles into JavaScript.

3. **Virtual DOM (Document Object Model)**:
   - React uses a concept called the **Virtual DOM** to efficiently update the UI. In a typical HTML page, updating an element requires changes directly to the DOM, which can be slow.
   - The Virtual DOM is like a lightweight copy of the actual DOM. When data changes in a React app, it first updates the Virtual DOM. Then, React figures out the minimal number of changes needed to update the actual DOM, making updates very fast.
   - This approach means that React can handle updates more efficiently, allowing for fast, smooth UIs.

4. **State and Props**:
   - In React, **state** is data that can change over time, like a user's input in a form, or the result of an API call.
   - Each component can manage its own state, and when the state changes, React automatically re-renders that component to reflect the new data.
   - **Props** (short for "properties") are a way of passing data from one component to another. For example, a `ProfileCard` component might receive `user` data as a prop and render the user's name and profile picture accordingly.
   - In Java terms, props are like parameters passed to a class constructor, while state is like instance variables that can be modified over time.

5. **Hooks (e.g., `useState`, `useEffect`)**:
   - **Hooks** are special functions in React that allow you to use features like state and lifecycle methods in functional components (as opposed to class components).
   - **`useState`** is a hook that lets you add state to a functional component.
   - **`useEffect`** is a hook that lets you run side effects in a component, such as fetching data from an API when the component loads.
   - Hooks make it easier to manage state and handle side effects (e.g., updating the DOM or fetching data) in components.

6. **Declarative UI**:
   - React follows a **declarative approach** to building UIs, meaning that you describe what the UI should look like for a given state, and React takes care of updating the DOM as needed.
   - In traditional JavaScript, you would use imperative code to select elements and change them manually. In React, you simply define how the UI should appear based on the current state, and React updates the DOM for you.

## Why Use React?

- **Reusability**: Components make it easy to reuse code and create consistent designs across a project.
- **Efficiency**: The Virtual DOM optimizes rendering, making React applications faster, even with lots of updates.
- **Separation of Concerns**: By breaking the UI into small, manageable components, it’s easier to work on different parts of the UI independently.
- **Declarative Syntax**: You can describe what you want in your UI, and React will handle the underlying updates, allowing you to focus more on logic than DOM manipulation.

## Quick Example

Here’s a simple React component:

```react
import React from 'react';

function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}

// Usage
<Welcome name="Alice" />
```

- **`Welcome`** is a component that receives `name` as a prop and displays a greeting.
- When used in an application, `Welcome` will render as `<h1>Hello, Alice!</h1>`.

React can feel different at first, especially with JSX and the component-based structure, but it provides a powerful and efficient way to build dynamic, responsive user interfaces.
