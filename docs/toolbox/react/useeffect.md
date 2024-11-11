---
title: UseEffect
description: What is UseEffect in React?
layout: default
nav_order: 7
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/useeffect
---

![Codelab](./images/reactlogo.png){: style="display: block; margin: 0 auto; width:50%" }

# What is the UseEffect hook in React?

The `useEffect` hook in React allows you to perform **side effects** in functional components. A side effect can be anything that affects something outside of the component, such as data fetching, subscriptions, timers, or manually manipulating the DOM.

## How `useEffect` Works

The `useEffect` hook takes two parameters:

1. A **function** that contains the side effect code.
2. An optional **dependency array** that tells React when to run the effect.

Here’s the basic syntax for `useEffect`:

```react
useEffect(() => {
  // Side effect code here
  return () => {
    // Cleanup code here (optional)
  };
}, [dependencies]);
```

- **Effect function**: The first argument is a function where you put your side-effect code. This function runs after the component renders.
- **Cleanup function**: If you return a function from the effect, React treats it as a cleanup function, which runs before the effect re-runs or when the component unmounts.
- **Dependency array**: The second argument is an array of dependencies that tells React when to run the effect. If dependencies change, the effect re-runs. If you omit this array, the effect will run after every render.

## Example: Using `useEffect` for Data Fetching

Here’s a simple example of fetching data when a component mounts.

```react
import React, { useState, useEffect } from "react";

function DataFetcher() {
  const [data, setData] = useState(null);

  useEffect(() => {
    // Side effect: fetch data
    fetch("https://api.example.com/data")
      .then(response => response.json())
      .then(data => setData(data))
      .catch(error => console.error("Error fetching data:", error));
  }, []);  // Empty dependency array: run effect only once on mount

  return (
    <div>
      {data ? <p>Data: {JSON.stringify(data)}</p> : <p>Loading...</p>}
    </div>
  );
}
```

In this example:

- We use `useEffect` with an empty dependency array `[]`, so the effect runs only once when the component mounts.
- The effect fetches data when the component mounts, and `setData` updates the state when the data is loaded.
- The component re-renders with the fetched data once it’s available.

## Dependencies in `useEffect`

The dependency array controls when the effect re-runs. Here are a few key scenarios:

1. **No Dependency Array**: `useEffect(() => { ... });`
   - The effect will run after **every render** (initial and subsequent renders).
2. **Empty Dependency Array**: `useEffect(() => { ... }, []);`
   - The effect will run **only once**, when the component mounts, similar to `componentDidMount`.
3. **With Dependencies**: `useEffect(() => { ... }, [dependency]);`
   - The effect will run **only when the specified dependencies change**.

### Example with Dependency Array

```react
function Counter({ count }) {
  useEffect(() => {
    console.log(`Count changed to ${count}`);
  }, [count]);  // Effect re-runs only when `count` changes

  return <p>Count: {count}</p>;
}
```

In this example, the effect will only run when the `count` prop changes. This is useful for responding to specific changes without re-running the effect on every render.

## Cleanup in `useEffect`

If your effect requires cleanup (e.g., removing event listeners, canceling timers, or unsubscribing from services), you can return a function inside the effect. This cleanup function runs either when the component unmounts or before the effect re-runs.

### Example with Cleanup Function

```react
function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    // Set up a timer
    const intervalId = setInterval(() => {
      setSeconds(prevSeconds => prevSeconds + 1);
    }, 1000);

    // Cleanup function to clear the timer
    return () => clearInterval(intervalId);
  }, []);  // Empty dependency array: runs only on mount and unmount

  return <p>Elapsed time: {seconds} seconds</p>;
}
```

In this example:

- `setInterval` creates a timer that updates the `seconds` state every second.
- The cleanup function `clearInterval(intervalId)` stops the timer when the component unmounts, preventing memory leaks.

## Summary

- `useEffect` allows you to perform side effects in functional components, such as data fetching, timers, and event listeners.
- It runs after the component renders and can re-run if dependencies change.
- You can control when `useEffect` runs by providing a dependency array:
  - No dependencies: Runs after every render.
  - Empty array `[]`: Runs only once on mount.
  - Specified dependencies `[dep1, dep2]`: Runs when any of these dependencies change.
- The optional cleanup function handles tasks like clearing timers, unsubscribing, and removing event listeners.

## When to Use `useEffect`

- **Data fetching** (e.g., calling APIs or fetching resources).
- **Subscribing and unsubscribing** (e.g., event listeners, WebSocket connections).
- **Timers and intervals** (e.g., countdowns, animations).
- **DOM manipulation** (e.g., focus, scroll position) – although this should be done sparingly in React.

By managing side effects with `useEffect`, you ensure that your React components stay reactive to changes, update as needed, and clean up resources efficiently, keeping the component lifecycle predictable and efficient.
