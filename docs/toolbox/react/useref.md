---
title: UseRef
description: What is UseRef in React?
layout: default
nav_order: 8
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/useref
---

![Codelab](./images/reactlogo.png){: style="display: block; margin: 0 auto; width:50%" }

# What is the UseRef hook in React?

The `useRef` hook in React is used to create a **mutable reference** that persists across renders without causing a re-render when updated. It’s commonly used to directly access or manipulate DOM elements, store mutable values, or keep track of data that doesn’t need to cause re-renders.

## How `useRef` Works

When you call `useRef`, it returns a **ref object** with a single property: `.current`. This property holds the reference value, which can be read and updated without triggering a re-render. The ref object itself stays the same across re-renders, but its `.current` property can be changed as needed.

Here’s the syntax for `useRef`:

```javascript
const ref = useRef(initialValue);
```

- `ref.current` holds the reference value.
- `initialValue` is the initial value for `.current`, which can be `null` or any other value you wish to store.

## Example: Accessing DOM Elements with `useRef`

One of the most common use cases for `useRef` is to access DOM elements directly, like focusing an input field.

```react
import React, { useRef } from "react";

function InputFocus() {
  const inputRef = useRef(null);

  const focusInput = () => {
    // Directly accesses the DOM element to focus it
    inputRef.current.focus();
  };

  return (
    <div>
      <input ref={inputRef} type="text" placeholder="Type here..." />
      <button onClick={focusInput}>Focus Input</button>
    </div>
  );
}
```

In this example:

- `useRef(null)` creates a ref and initializes `inputRef.current` with `null`.
- We assign `ref={inputRef}` to the `<input>`, linking the DOM element to `inputRef`.
- When `focusInput` is called, `inputRef.current.focus()` directly calls the `.focus()` method on the input element.

## Example: Persisting Values Across Renders

`useRef` is also useful for storing values that need to persist between renders but don’t need to trigger a re-render if they change. A common example is storing a timer ID in an interval.

```react
import React, { useRef, useState } from "react";

function Timer() {
  const [seconds, setSeconds] = useState(0);
  const timerId = useRef(null);  // Ref to store the timer ID

  const startTimer = () => {
    if (!timerId.current) {
      timerId.current = setInterval(() => {
        setSeconds(prev => prev + 1);
      }, 1000);
    }
  };

  const stopTimer = () => {
    clearInterval(timerId.current);
    timerId.current = null;
  };

  return (
    <div>
      <p>Elapsed Time: {seconds} seconds</p>
      <button onClick={startTimer}>Start</button>
      <button onClick={stopTimer}>Stop</button>
    </div>
  );
}
```

In this example:

- We use `timerId.current` to store the interval ID created by `setInterval`.
- `timerId.current` persists across re-renders, allowing us to start and stop the timer without causing unnecessary re-renders.
- We don’t update the component’s state with `timerId` because changing it doesn’t need to trigger a re-render.

## Key Use Cases for `useRef`

1. **Accessing DOM Elements**: `useRef` is often used to directly interact with DOM elements (e.g., focusing an input field, scrolling to a specific element).
2. **Storing Mutable Values**: Store data that should persist across renders but doesn’t need to trigger re-renders, like timer IDs, counters, or cached values.
3. **Keeping Track of Previous State or Props**: Track the previous value of a state or prop across renders.

## Example: Storing Previous Value

You can use `useRef` to store the previous value of a state or prop without causing re-renders.

```react
import React, { useRef, useEffect, useState } from "react";

function PreviousCounter() {
  const [count, setCount] = useState(0);
  const prevCount = useRef(count);  // Create a ref to hold the previous count

  useEffect(() => {
    prevCount.current = count;  // Update ref with the latest count after each render
  }, [count]);  // Runs only when `count` changes

  return (
    <div>
      <p>Current Count: {count}</p>
      <p>Previous Count: {prevCount.current}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

In this example:

- `prevCount` holds the previous value of `count` across renders.
- After every render, the `useEffect` hook updates `prevCount.current` to the latest `count` value.
- Unlike setting a state, updating `prevCount.current` doesn’t trigger a re-render.

## Summary

- **`useRef`** creates a ref object that holds a `.current` property for mutable data.
- Updating `.current` doesn’t trigger a re-render, making `useRef` ideal for storing DOM elements or values that don’t affect rendering.
- Common use cases include:
  - Direct access to DOM elements (e.g., for focusing, scrolling).
  - Storing mutable values like interval IDs, timers, or cached values.
  - Keeping track of previous state or prop values.

## When to Use `useRef`

- When you need to directly interact with or control a DOM element.
- For keeping track of data between renders without causing re-renders.
- When managing non-reactive data that should persist across renders.

The `useRef` hook provides an efficient and straightforward way to handle mutable values in functional components, helping keep your components clean and efficient by avoiding unnecessary re-renders.
