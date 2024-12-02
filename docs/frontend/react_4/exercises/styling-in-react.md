---
title: Styled Components
description: Exercises for Frontend Week IV
layout: default
nav_order: 1
grand_parent: React IV
parent: Exercises
permalink: /frontend/react-4/exercises/styling-in-react/
---

# Exercise: Styling with StyledComponents

Open the StyledComponents documentation: [StyledComponents Documentation](https://styled-components.com/docs) for reference.

We also have a brief introduction to StyledComponents in the Toolbox: [Styled Components](../../../toolbox/react/styled_components.md)

1. Create a [new project with Vite](../../../toolbox/react/vite.md) and clean up in the usual way before you continue.
2. Install StyledComponents using:

      ```bash
      npm install styled-components
      ```

## Styled Todo App v. II

We built a [Todo App](../../react_2/exercises/react_shared_state.md) two weeks ago. Now we will take it further and style it using StyledComponents. We also want to recap the use of shared state, react-router, props, css, and more.

**Objective**: Build a styled Todo App using React and styled-components.

1. **Main Components to Create**:
   - `TodoList`: Displays a list of todos.
   - `AddTodo`: A form to add new todos.

2. **Navigation Bar**

   - Create a styled navigation bar with links to `Home`, `Todos`, and `Login`.
   - Use styled-components to style the navigation bar.
   - Create placeholder pages for `Home`, `Todos` and `Login`.
   - Use `React Router` to navigate between pages.

3. **TodoList Styling**

   - Each todo should be displayed in a styled card with a title and description.
   - Add hover effects using styled-components (e.g., change background color or scale the card).

4. **AddTodo Form**

   - Create a styled form with input fields for title and description, and a submit button.
   - Style the button with hover and active states using styled-components.
   - Implement validation to ensure both fields are filled.

5. **Dynamic Styling with Props**

   - Add a "Toggle Theme" button to switch between light and dark themes.
   - Use props to apply different styles based on the selected theme (e.g., background, text color).

6. **Global Styles**

   - Use `createGlobalStyle` to define default fonts and colors.
   - Dynamically update the background color based on the current theme.

7. **Theming**

   - Define light and dark theme objects with properties like `background`, `text`, and `button`.
   - Pass the theme object to components using `ThemeProvider`.

8. **Bonus: Animations**

   - Animate todo appearance with `keyframes` (e.g., fade in).
   - Add hover animations to make the todo cards visually engaging.

9. **Testing**

   - Ensure the theme switch toggles correctly.
   - Style additional components to reinforce the use of styled-components.

---

### Additional hints

- **State Management**: Use `useState` for managing todos and theme selection.
- **Prop-Driven Styling**: Demonstrate how to pass `props` to styled-components for dynamic styles.
- **Code Organization**: Structure your components logically and separate concerns (e.g., `components`, `styles`, `pages`). Place your styled-components where they make most sense.

### To consider

1. What is the benefit of using styled-components over traditional CSS?
2. How does the `ThemeProvider` simplify theming in styled-components?
3. How can you optimize the styling of your components to reduce redundancy?
