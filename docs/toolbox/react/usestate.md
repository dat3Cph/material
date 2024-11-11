---
title: UseState
description: What is UseState in React?
layout: default
nav_order: 6
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/usestate
---

![Codelab](./images/reactlogo.png){: style="display: block; margin: 0 auto; width:50%" }

# What is the UseState hook in React?

In React, the `useState` hook is a fundamental way to add **state** to functional components. It allows you to declare a state variable and provides a function to update that variable, enabling components to keep track of dynamic data and re-render when the data changes.

## How `useState` Works

The `useState` hook is called inside a functional component, and it returns an array with two elements:

1. The **current state value**.
2. A **function** that can be used to update this state.

Here’s the basic syntax for `useState`:

```javascript
const [state, setState] = useState(initialValue);
```

- `state` – The current value of the state variable.
- `setState` – A function used to update the state.
- `initialValue` – The initial value of the state, passed as an argument to `useState`.

When `setState` is called, React re-renders the component with the updated state.

## Example: Using `useState`

Let’s say we want to create a simple counter component.

```react
import React, { useState } from "react";

function Counter() {
  // Declare a state variable named "count" with an initial value of 0
  const [count, setCount] = useState(0);

  // Function to increment count by 1
  const increment = () => setCount(count + 1);

  return (
    <div>
      <p>Current Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}
```

In this example:

- We initialize `count` with `useState(0)`, so the initial count is `0`.
- We use `setCount(count + 1)` inside the `increment` function to update the count.
- Every time the button is clicked, `increment` is called, which increases `count` by 1 and triggers a re-render.

## Initializing `useState` with Dynamic Values

If the initial value of the state depends on some computation, you can pass a function to `useState`. This function will be called only once, at the initial render.

```javascript
const [value, setValue] = useState(() => computeInitialValue());
```

This avoids recalculating the initial value on every render.

## Updating State with Previous State

When updating state based on the previous state, use the function form of `setState`, which takes the previous state as an argument.

```javascript
const increment = () => setCount(prevCount => prevCount + 1);
```

This ensures that `count` is correctly updated, especially in cases where multiple updates happen in quick succession.

## Managing Complex State with `useState`

`useState` can also manage more complex state like objects or arrays. However, be cautious with objects and arrays because `useState` doesn’t merge state updates automatically (unlike `this.setState` in class components).

For example, with an object:

```javascript
const [user, setUser] = useState({ name: "Alice", age: 25 });

// To update the age
setUser(prevUser => ({ ...prevUser, age: 26 }));
```

Here, we spread the `prevUser` object (`{ ...prevUser }`) to keep the other properties intact, only updating `age`.

## Summary

- `useState` is used to add state to functional components.
- It takes an initial value and returns the current state and a function to update it.
- Updating state with the updater function causes the component to re-render with the new state.
- Use the function form of `setState` for updates based on previous state, and handle objects and arrays carefully by preserving the existing structure.

## Benefits of `useState`

The `useState` hook allows for more concise, readable code and enables functional components to manage state, making it the primary state management hook in functional React components. It’s particularly useful for handling interactive components and data-driven UIs in a straightforward and declarative way.
