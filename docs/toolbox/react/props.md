---
title: Props
description: How does props work in React
layout: default
nav_order: 11
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/props
---

![Codelab](./images/reactlogo.png){: style="display: block; margin: 0 auto; width:50%" }

# How does Props work in React?

In React, **props** (short for "properties") are a way to pass data from one component to another, typically from a parent component to its child component. Props are **read-only** and help make components more flexible and reusable by allowing you to pass in dynamic values that can be displayed or used within a child component.

## Key Characteristics of Props

- **Immutable**: Props cannot be modified by the child component receiving them; they are read-only.
- **Passed from Parent to Child**: Props flow **down** the component tree, from parent to child components.
- **Reusable**: Components can be made more reusable by allowing different props to be passed in.
- **Flexible**: Props can be any data type (e.g., strings, numbers, arrays, objects, functions).

## Basic Example of Using Props

Let’s create a simple example with a parent component that passes props to a child component.

```react
import React from "react";

// Child component receiving props
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}

// Parent component passing props to child
function App() {
  return (
    <div>
      <Greeting name="Alice" />
      <Greeting name="Bob" />
    </div>
  );
}

export default App;
```

In this example:

- The `App` component renders two `Greeting` components.
- Each `Greeting` component receives a `name` prop (either "Alice" or "Bob").
- The `Greeting` component then uses `props.name` to display a personalized greeting.

## Using Destructuring with Props

You can simplify props access by destructuring them directly in the function parameter, making the code cleaner.

```react
function Greeting({ name }) {
  return <h1>Hello, {name}!</h1>;
}
```

With destructuring, we access `name` directly instead of using `props.name`.

## Passing Multiple Props

You can pass multiple props to a component, such as `name`, `age`, and `city`.

```react
function UserProfile({ name, age, city }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>Age: {age}</p>
      <p>City: {city}</p>
    </div>
  );
}

function App() {
  return (
    <div>
      <UserProfile name="Alice" age={25} city="New York" />
      <UserProfile name="Bob" age={30} city="San Francisco" />
    </div>
  );
}
```

In this example:

- `UserProfile` receives three props: `name`, `age`, and `city`.
- Each `UserProfile` instance renders different data based on the props passed from `App`.

## Passing Functions as Props

Props can also be used to pass functions to child components. This is useful for handling events, like button clicks, in the parent component.

```react
function Button({ onClick, label }) {
  return <button onClick={onClick}>{label}</button>;
}

function App() {
  const handleClick = () => {
    alert("Button clicked!");
  };

  return <Button onClick={handleClick} label="Click Me" />;
}
```

Here:

- `App` defines a function `handleClick` that displays an alert.
- `App` passes `handleClick` as the `onClick` prop to the `Button` component.
- When the button is clicked, the `Button` component calls `onClick`, triggering `handleClick` in the parent component.

## Passing Objects as Props

You can pass an entire object as a prop, which is helpful for passing a lot of data in a single prop.

```react
function UserProfile({ user }) {
  return (
    <div>
      <h2>{user.name}</h2>
      <p>Age: {user.age}</p>
      <p>City: {user.city}</p>
    </div>
  );
}

function App() {
  const user = { name: "Alice", age: 25, city: "New York" };
  
  return <UserProfile user={user} />;
}
```

In this example:

- The `App` component creates an object `user` with multiple properties.
- It passes the `user` object as a single prop to `UserProfile`.
- `UserProfile` accesses `user` properties using `user.name`, `user.age`, and `user.city`.

## Conditional Rendering with Props

Props can be used to conditionally render elements within a component.

```react
function Status({ isOnline }) {
  return (
    <p>{isOnline ? "User is online" : "User is offline"}</p>
  );
}

function App() {
  return (
    <div>
      <Status isOnline={true} />
      <Status isOnline={false} />
    </div>
  );
}
```

In this example:

- `Status` uses the `isOnline` prop to conditionally render different text.
- Based on the value of `isOnline` (either `true` or `false`), it displays either "User is online" or "User is offline."

## Summary

- **Props** are data passed from a parent component to a child component, making components flexible and reusable.
- They are **read-only** in the child component.
- **Destructuring** props simplifies syntax.
- **Functions, objects, and conditional values** can be passed as props, allowing for dynamic and flexible components.

Props are a core concept in React for passing data and enabling inter-component communication, making it easier to build complex, data-driven UIs.
