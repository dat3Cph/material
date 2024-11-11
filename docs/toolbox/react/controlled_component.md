---
title: Controlled Components
description: What is a controlled component in React?
layout: default
nav_order: 9
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/controlled-component
---

![Codelab](./images/reactlogo.png){: style="display: block; margin: 0 auto; width:50%" }

# What is a Controlled Component in React?

In React, a **controlled component** is a form component (such as an `<input>`, `<textarea>`, or `<select>`) whose value is controlled by the component’s state. This means that the component’s value is stored in the React state, and it can only be updated through a React event handler that modifies the state.

By using controlled components, you gain full control over the form data, enabling validation, conditional rendering, and integration with other React features.

## Key Characteristics of Controlled Components

1. **React State as the Single Source of Truth**: The input’s value is set by the state, meaning the form component’s data is always in sync with the component’s state.
2. **Two-Way Binding**: When a user types or changes the input, an event handler updates the state, and the component re-renders to reflect the latest state.

## Example of a Controlled Component

Let’s create a simple controlled component with an `<input>` field and a button to display the entered name.

```react
import React, { useState } from "react";

function NameForm() {
  const [name, setName] = useState("");  // React state to store input value

  // Handler to update state when input changes
  const handleChange = (event) => {
    setName(event.target.value);
  };

  const handleSubmit = (event) => {
    event.preventDefault();
    alert(`Hello, ${name}!`);
  };

  return (
    <form onSubmit={handleSubmit}>
      <label>
        Name:
        <input type="text" value={name} onChange={handleChange} />
      </label>
      <button type="submit">Submit</button>
    </form>
  );
}

export default NameForm;
```

In this example:

- **State**: `name` is initialized to an empty string and holds the input’s value.
- **Event Handler**: The `handleChange` function updates the `name` state whenever the input value changes (`onChange`).
- **Value Attribute**: The `input` field has a `value` attribute set to `name`, meaning its displayed value is controlled by the `name` state.
- **Submit Button**: When the form is submitted, the `handleSubmit` function uses the current `name` state to display a greeting.

With this approach, the input field is completely controlled by React's state, creating a predictable, reactive form element.

## Why Use Controlled Components?

1. **Immediate Validation**: You can validate and provide feedback to the user as they type.
2. **Single Source of Truth**: Since the component state holds the form data, you can manage, validate, and manipulate it in one place.
3. **Conditional Rendering**: React can conditionally render content based on the form data’s state.
4. **Enhanced UX**: It’s easier to provide features like auto-formatting, displaying error messages, and more because you control the component’s value directly.

## Additional Examples of Controlled Components

### Example: Controlled Textarea

```react
function TextAreaForm() {
  const [message, setMessage] = useState("");

  const handleChange = (event) => {
    setMessage(event.target.value);
  };

  return (
    <form>
      <label>
        Message:
        <textarea value={message} onChange={handleChange} />
      </label>
      <p>Message Preview: {message}</p>
    </form>
  );
}
```

In this example, the `<textarea>` value is bound to `message` state, and it updates as the user types.

### Example: Controlled Select Dropdown

```react
function SelectForm() {
  const [favoriteColor, setFavoriteColor] = useState("red");

  const handleChange = (event) => {
    setFavoriteColor(event.target.value);
  };

  return (
    <form>
      <label>
        Pick your favorite color:
        <select value={favoriteColor} onChange={handleChange}>
          <option value="red">Red</option>
          <option value="blue">Blue</option>
          <option value="green">Green</option>
        </select>
      </label>
      <p>Your favorite color is: {favoriteColor}</p>
    </form>
  );
}
```

In this example, the `<select>` dropdown’s value is controlled by `favoriteColor` state, which updates based on the user's selection.

## Important Points to Note

- **onChange Handler is Required**: To make an input controlled, you must handle changes to keep the component’s state and the input field in sync.
- **Initial Value**: Set an initial value in the state, otherwise, the controlled input may behave unpredictably.
- **Controlled vs. Uncontrolled Components**: An uncontrolled component lets the DOM handle its state (e.g., using `ref` to access values), while a controlled component relies on React state.

## Controlled vs. Uncontrolled Components

Controlled components use React’s state to control input values, providing consistency and control, while uncontrolled components rely on the DOM’s internal state.

### Controlled Component

```jsx
<input type="text" value={name} onChange={(e) => setName(e.target.value)} />
```

### Uncontrolled Component

```jsx
<input type="text" ref={nameRef} />
```

In general, controlled components are preferred in React because they make managing and syncing form data easier and provide more control over the input elements. Uncontrolled components can be useful for certain cases where minimal control is needed or when working with non-React libraries.

## Summary

- A **controlled component** in React has its value controlled by React state, making React the “single source of truth.”
- **Two-way data binding** between state and input means the component re-renders with every state change, ensuring the input displays the correct data.
- Controlled components offer greater control over user input, allowing for validation, conditional rendering, and improved user experience.
