---
title: Functional Components
description: Functional components in React
layout: default
nav_order: 13
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/functional_components
---

# Functional Components in React

![Codelab](./images/reactlogo.png){: style="display: block; margin: 0 auto; width:50%" }

In React, a **functional component** is a type of component defined as a JavaScript function. It accepts props as an argument and returns JSX, which describes what should be rendered to the DOM. Functional components are simpler, more concise, and have become the standard way to write components in React, especially with the introduction of **React Hooks**, which allow functional components to manage state and lifecycle methods.

## Defining a Functional Component

A functional component is a plain JavaScript function that returns JSX, without the need to extend from `React.Component` as you would with class components.

### Example

```react
import React from 'react';

function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

export default Greeting;
```

Or, using an arrow function:

```react
import React from 'react';

const Greeting = (props) => {
  return <h1>Hello, {props.name}!</h1>;
};

export default Greeting;
```

In this example:

- `Greeting` is a functional component that receives `props` as an argument.
- It returns JSX (`<h1>Hello, {props.name}!</h1>`), which will display a greeting based on the `name` prop.

## Key Features of Functional Components

1. **Simpler Syntax**: Functional components are simple functions without the need for `this` or other complex syntax.
2. **No `this` Keyword**: In functional components, `this` is not used to access props or state, making the code less error-prone and easier to understand.
3. **Better Performance**: Since they don’t have the overhead of creating a React component instance, functional components can be slightly more performant than class components.

## State and Lifecycle in Functional Components (React Hooks)

Previously, functional components were stateless, but with the introduction of **Hooks** (React 16.8+), functional components can now have state and lifecycle methods. The most commonly used Hooks are `useState` and `useEffect`.

### Adding State with `useState`

The `useState` Hook allows you to add state to a functional component.

```react
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // Declare a state variable

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}

export default Counter;
```

In this example:

- `useState(0)` initializes a state variable, `count`, with a starting value of `0`.
- `setCount` is a function that updates the `count` state when called.

### Using Lifecycle Methods with `useEffect`

The `useEffect` Hook allows you to perform side effects in functional components, similar to lifecycle methods in class components like `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`.

```react
import React, { useState, useEffect } from 'react';

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds(s => s + 1);
    }, 1000);
    
    return () => clearInterval(interval); // Clean up the interval on unmount
  }, []);

  return <div>Seconds: {seconds}</div>;
}

export default Timer;
```

In this example:

- `useEffect` sets up a timer that increments `seconds` every second.
- The cleanup function `return () => clearInterval(interval);` stops the interval when the component is unmounted, mimicking the behavior of `componentWillUnmount`.

## Benefits of Functional Components

1. **Easier to Read and Test**: Functional components are often simpler to understand, especially for smaller components.
2. **Hooks**: With React Hooks, functional components can manage state, use lifecycle methods, and more, making them as powerful as class components.
3. **Concise and Flexible**: Functional components avoid the overhead of `this` and make use of JavaScript closures, reducing complexity.
4. **Performance**: Functional components are generally faster as they don’t have to instantiate or inherit from React’s component classes.

## Summary

- A **functional component** is a JavaScript function that takes `props` as an argument and returns JSX.
- **React Hooks** (like `useState` and `useEffect`) make it possible to use state and lifecycle methods in functional components, providing full functionality without needing classes.
- Functional components are the recommended way to write components in modern React, as they’re simpler, more concise, and just as powerful.
