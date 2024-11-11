---
title: JSX
description: What is JSX in React?
layout: default
nav_order: 3
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/jsx
---

![Codelab](./images/reactlogo.png){: style="display: block; margin: 0 auto; width:50%" }

# What is JSX in React?

JSX (JavaScript XML) is a syntax extension for JavaScript that is used in React to describe what the UI should look like. JSX looks similar to HTML but is actually JavaScript code that gets compiled to `React.createElement` function calls behind the scenes. This compilation allows React to create and update the DOM in a performant way. Here’s a breakdown of what JSX is and why it’s useful:

## Key Concepts of JSX

1. **HTML-Like Syntax in JavaScript**:
   JSX allows you to write HTML-like tags directly within JavaScript, making the code more readable and expressive. Instead of calling complex functions to create elements, you can write:

   ```jsx
   const element = <h1>Hello, world!</h1>;
   ```

   This code is intuitive and resembles the final HTML structure that it will render in the browser.

2. **Embedding JavaScript Expressions**:
   JSX lets you embed JavaScript expressions within curly braces `{ }`, enabling you to dynamically render values. For instance:

   ```jsx
   const name = 'Alice';
   const element = <h1>Hello, {name}!</h1>;
   ```

   Here, `{name}` dynamically inserts the value of the `name` variable within the `<h1>` tag.

3. **JSX Compiles to JavaScript**:
   JSX isn’t valid JavaScript; browsers can’t interpret it directly. During the build process, tools like Babel compile JSX into `React.createElement` calls. For example:

   ```jsx
   const element = <h1>Hello, world!</h1>;
   ```

   Compiles to:

   ```javascript
   const element = React.createElement('h1', null, 'Hello, world!');
   ```

   This compiled code is what React uses to efficiently manage the DOM.

4. **Attributes and Styling**:
   JSX attributes look similar to HTML attributes but with camelCase for multi-word properties. For example:

   ```jsx
   const element = <button className="btn" onClick={handleClick}>Click me</button>;
   ```

   - **className** is used instead of `class` (since `class` is a reserved word in JavaScript).
   - **onClick** is written in camelCase instead of `onclick`.

5. **JSX with Components**:
   JSX is commonly used to define components, which are the building blocks of a React application. A component can be a function that returns JSX:

   ```jsx
   function Greeting() {
     return <h1>Hello, world!</h1>;
   }
   ```

   Here, `Greeting` is a functional component that returns a `<h1>` element.

6. **Nested and Conditional JSX**:
   JSX can be nested within other JSX elements to create more complex structures. Additionally, conditional rendering can be done within JSX using JavaScript expressions:

   ```jsx
   function Greeting({ isLoggedIn }) {
     return (
       <div>
         {isLoggedIn ? <h1>Welcome back!</h1> : <h1>Please sign up.</h1>}
       </div>
     );
   }
   ```

## Why JSX is Used in React

- **Readability**: JSX makes it easier to visualize the structure of the UI directly in the JavaScript code.
- **Better Developer Experience**: It allows developers to work within a single file for both logic and UI, streamlining development.
- **Direct Mapping to UI Elements**: With JSX, there’s a straightforward mapping from components to the DOM elements they render.

## Summary

JSX bridges the gap between JavaScript and the DOM by allowing a familiar HTML-like syntax within JavaScript. It’s compiled to `React.createElement` calls, enabling React to manage the virtual DOM efficiently and keeping the UI in sync with the underlying data.
