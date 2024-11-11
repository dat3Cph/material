---
title: React Lifecycle
description: How does the lifecycle work in React
layout: default
nav_order: 10
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/lifecycle
---

![Codelab](./images/reactlogo.png){: style="display: block; margin: 0 auto; width:50%" }

# How does the lifecycle work in React?

Understanding the **React component lifecycle** is crucial for building efficient, responsive applications, especially as you work with data fetching, animations, timers, and other side effects. React’s lifecycle includes phases that happen from the moment a component is created (mounted), updated, and eventually removed (unmounted).

## 1. Lifecycle Phases Overview

React’s lifecycle has three main phases:

- **Mounting**: When the component is created and added to the DOM.
- **Updating**: When the component re-renders due to changes in props or state.
- **Unmounting**: When the component is removed from the DOM.

## 2. Key Lifecycle Events in Functional Components

With React hooks (e.g., `useEffect`), we can manage these lifecycle stages in functional components. Here’s a breakdown of each stage with `useEffect` usage and key things to keep in mind.

---

### Mounting Phase

The mounting phase occurs when a component is created and inserted into the DOM. During this phase, you might want to **initialize data** (like fetching data from an API), **set up event listeners**, or **run animations**.

**Key Points for Mounting:**

- `useEffect` with an empty dependency array (`[]`) runs once after the component mounts.
- This is similar to `componentDidMount` in class components.

**Example:**

```react
import React, { useState, useEffect } from 'react';

function MyComponent() {
  const [data, setData] = useState(null);

  useEffect(() => {
    // Fetch data when component mounts
    fetch("https://api.example.com/data")
      .then(response => response.json())
      .then(data => setData(data))
      .catch(error => console.error("Error fetching data:", error));
  }, []);  // Empty dependency array means it only runs once after the first render

  return <div>{data ? JSON.stringify(data) : "Loading..."}</div>;
}
```

**Takeaway**: Use `useEffect` with an empty dependency array to run code only once when the component mounts.

---

### Updating Phase

The updating phase occurs whenever the component’s **state** or **props** change, which triggers a re-render. During this phase, you might want to **re-fetch data** based on new props, **update the DOM**, or **trigger animations** in response to changes.

**Key Points for Updating:**

- `useEffect` with dependencies (e.g., `[prop1, state1]`) runs whenever any of the dependencies change.
- Use this to manage side effects that need to update based on changes in state or props.

**Example:**

```react
function MyComponent({ userId }) {
  const [userData, setUserData] = useState(null);

  useEffect(() => {
    // Fetch user data when userId changes
    fetch(`https://api.example.com/user/${userId}`)
      .then(response => response.json())
      .then(data => setUserData(data));
  }, [userId]);  // Effect re-runs when `userId` changes

  return <div>{userData ? userData.name : "Loading user data..."}</div>;
}
```

**Takeaway**: Use dependencies in `useEffect` to run code only when specific props or state variables change.

---

### Unmounting Phase

The unmounting phase occurs when the component is removed from the DOM. Here, you might want to **clean up side effects** like timers, event listeners, or subscriptions.

**Key Points for Unmounting:**

- Use the cleanup function in `useEffect` to handle cleanup tasks. The cleanup function is defined as a return statement within `useEffect`.
- Cleanup runs right before the component unmounts, preventing memory leaks and ensuring efficient resource usage.

**Example:**

```react
function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    // Start a timer when component mounts
    const timerId = setInterval(() => setSeconds(prev => prev + 1), 1000);

    // Cleanup function to stop the timer when component unmounts
    return () => clearInterval(timerId);
  }, []);  // Empty dependency array ensures this effect only runs on mount and unmount

  return <div>Elapsed time: {seconds} seconds</div>;
}
```

**Takeaway**: Use a cleanup function in `useEffect` to release resources when a component unmounts, such as stopping timers, removing event listeners, or canceling API requests.

---

## Summary of Key Lifecycle Points for Beginners

1. **Mounting (component creation)**: Use `useEffect(() => { ... }, [])` to run code only once when the component mounts.
   - Good for initial data fetching, setting up subscriptions, or initializing component state.

2. **Updating (props/state changes)**: Use `useEffect(() => { ... }, [dependencies])` to run code when specific values change.
   - Good for re-fetching data or running side effects in response to updated props or state.

3. **Unmounting (component removal)**: Use a cleanup function in `useEffect` to remove subscriptions, timers, or other resources.
   - Good for preventing memory leaks by cleaning up resources like event listeners or timers.

## Common Pitfalls and Tips for Beginners

1. **Avoid Infinite Loops in `useEffect`**:

   - If you don’t include a dependency array, `useEffect` will run after every render, which can lead to infinite loops.
   - Always include a dependency array and make sure it contains only necessary dependencies.

2. **State Changes Trigger Re-Renders**:

   - Changing state triggers a re-render, so be mindful of excessive state updates within `useEffect`.

3. **Only Add Necessary Dependencies**:

   - If you add too many dependencies to the dependency array, `useEffect` might re-run more often than intended.
   - Use only the variables that the effect function actually depends on.

4. **Don’t Forget Cleanups**:

   - For effects that set up subscriptions, timers, or other long-running tasks, always include a cleanup function to avoid memory leaks.

5. **Debugging with Console Logs**:

   - Use `console.log` statements to track when `useEffect` runs, which is helpful to understand the lifecycle flow during development.

6. **React Strict Mode**:

   - React’s Strict Mode intentionally mounts and unmounts components more often to help catch unintentional side effects.
   - Be aware of this during development, as it may cause effects to run more frequently than they would in production.

By mastering these lifecycle stages and understanding the `useEffect` hook, you’ll gain greater control over how and when your components interact with external resources and handle data changes, making your applications more efficient and predictable.
