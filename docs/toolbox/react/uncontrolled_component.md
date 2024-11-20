---
title: Uncontrolled Components
description: What is a uncontrolled component in React?
layout: default
nav_order: 9
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/uncontrolled-component
---

![Codelab](./images/reactlogo.png){: style="display: block; margin: 0 auto; width:50%" }

# What is an Un-Controlled Component in React?

In React, **uncontrolled components** refer to components where form data is handled by the DOM itself, rather than React state. The form fields (like `<input>`, `<textarea>`, `<select>`, etc.) rely on the browser to manage their state. React simply references these DOM elements when needed.

---

## **How Uncontrolled Components Work in Your Example**

### **Key Points in the Example:**

1. **No `state` Management in React:**

   - The form fields (`<input>`, `<checkbox>`, etc.) do not use `useState` or `setState` to track their values.
   - Instead, the browser manages their state natively, and React interacts with them when necessary.

2. **Default Values:**

   - You use attributes like `defaultValue` and `defaultChecked` to set the initial values for the form fields:
     - `defaultValue="Some initial value"` for the text input.
     - `defaultChecked={true}` for the checkbox and radio buttons.
   - These attributes provide the initial value without locking the input to React state.

3. **Reading Values on Submission:**

   - Instead of tracking values using React's state (controlled components), the values are read directly from the DOM when the form is submitted.
   - The `handleSubmit` function reads the data using the `FormData` API:

     ```javascript
     const form = e.target;
     const formData = new FormData(form);
     ```

     This allows you to collect all form field values as key-value pairs at the time of submission.

4. **Interoperability with Fetch and JSON:**

   - The `FormData` object can be directly passed as the body of a `fetch` request, or it can be converted to a plain object with:

     ```javascript
     const formJson = Object.fromEntries(formData.entries());
     ```

   - This ensures that the form data is processed dynamically at submission, rather than being managed in React.

---

## **Advantages of Uncontrolled Components**

1. **Minimal React State Management:**

   - Since the browser handles form states, you don’t need to set up `useState` for every input.
   - Great for simple forms or legacy codebases transitioning to React.

2. **Native Form Handling:**

   - Leveraging the native `FormData` API makes it easy to handle form submissions, especially when sending data to an API or backend.

3. **Less Boilerplate Code:**

   - No need to write `onChange` handlers for every field or update React state on every user interaction.

---

### **Default vs. Controlled Fields**

| **Attribute**       | **Uncontrolled Component**           | **Controlled Component**                    |
|----------------------|---------------------------------------|---------------------------------------------|
| **Initial Value**    | `defaultValue` / `defaultChecked`    | `value` / `checked`                         |
| **Value Management** | Managed by the DOM                   | Managed via React `useState` or props       |
| **Use Case**         | Simple forms, less frequent updates  | Complex forms, real-time validation or updates |

---

## **What Happens in the Example?**

### **Text Input:**

- `<input name="myInput" defaultValue="Some initial value" />`
  - `defaultValue` sets the initial value to `"Some initial value"`.
  - The user can freely update the input, but React does not track its state.
  - At form submission, the value is retrieved via the `FormData` API.

### **Checkbox:**

- `<input type="checkbox" name="myCheckbox" defaultChecked={true} />`
  - `defaultChecked` initializes the checkbox as checked.
  - The checkbox's state is independent of React and is updated directly by the user.

### **Radio Buttons:**

- `<input type="radio" name="myRadio" value="option2" defaultChecked={true} />`
  - The `defaultChecked` attribute pre-selects "Option 2".
  - Only one radio button is selected at a time based on the group (`name="myRadio"`).

### **Form Submission:**

1. When the form is submitted, the `handleSubmit` function:
   - Prevents the default browser behavior (`e.preventDefault()`).
   - Reads the values of all form fields using the `FormData` API.
   - Logs the form data or sends it via `fetch`.

---

## **Why Use Uncontrolled Components?**

1. **Simple Forms:** Great for basic forms where you don't need to monitor or manipulate field values in real-time.
2. **Native Browser Features:** Allows you to use browser form features like `autofill`, `validation`, and resetting with minimal React involvement.
3. **Performance:** No React state updates on every keystroke; the browser handles the state efficiently.

---

## **When to Use Controlled Components Instead?**

- **Real-Time Validation:** If you need to validate inputs as the user types.
- **Dynamic Form Behavior:** If the UI reacts to form field changes (e.g., enabling/disabling a button based on input).
- **Pre-Filled Inputs with Updates:** If initial values are fetched from a server and can change dynamically.

In summary, **uncontrolled components** like in your example work by delegating state management to the DOM, with React handling events and submission. This approach is simple and effective for basic forms.

## Example from React.dev

```react
export default function MyForm() {
  function handleSubmit(e) {
    // Prevent the browser from reloading the page
    e.preventDefault();

    // Read the form data
    const form = e.target;
    const formData = new FormData(form);

    // You can pass formData as a fetch body directly:
    fetch('/some-api', { method: form.method, body: formData });

    // Or you can work with it as a plain object:
    const formJson = Object.fromEntries(formData.entries());
    console.log(formJson);
  }

  return (
    <form method="post" onSubmit={handleSubmit}>
      <label>
        Text input: <input name="myInput" defaultValue="Some initial value" />
      </label>
      <hr />
      <label>
        Checkbox: <input type="checkbox" name="myCheckbox" defaultChecked={true} />
      </label>
      <hr />
      <p>
        Radio buttons:
        <label><input type="radio" name="myRadio" value="option1" /> Option 1</label>
        <label><input type="radio" name="myRadio" value="option2" defaultChecked={true} /> Option 2</label>
        <label><input type="radio" name="myRadio" value="option3" /> Option 3</label>
      </p>
      <hr />
      <button type="reset">Reset form</button>
      <button type="submit">Submit form</button>
    </form>
  );
}
```
