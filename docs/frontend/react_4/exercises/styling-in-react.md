---
title: Styling in React with StyledComponents
description: Exercises for Frontend Week III
layout: default
nav_order: 1
grand_parent: React IV
parent: Exercises
permalink: /frontend/react-3/exercises/styling-in-react/
---

# Exercise: Styling with StyledComponents

Open the StyledComponents documentation: [StyledComponents Documentation](https://styled-components.com/docs) for reference.

1. Create a new project with Vite and clean up in the usual way before you continue.
2. Install StyledComponents using:
```bash
npm install styled-components
```

## We are going to create a simple Styled Todo App.

1. Set up your app with the following components:
   - TodoList (to display the list of todos)
   - AddTodo (to add a new todo)

1. Create a styled navigation bar at the top of your app:
   - The navigation bar should have links to Home, Todos and Login.
   - Style the navigation bar using styled-components.

1. Style the TodoList component:
   - Each todo should be displayed in a styled card with a title and a description.
   - Use StyledComponents to apply hover effects to the todo cards.

1. Style the AddTodo form:
   - Use a styled form component with input fields and a submit button.
   - Ensure the button has hover and active states styled using styled-components.

1. Use props to dynamically style a button component:
   - Add a button that toggles the theme (e.g., light or dark mode).
   - Use props in your styled components to apply different styles for light and dark themes.

1. Add a global style using createGlobalStyle from styled-components to:
   - Set a default font and background color for the app.
   - Change the background color based on the theme.

1. Use theming with the ThemeProvider component:
   - Define a light theme and a dark theme.
   - Pass the theme object using ThemeProvider and apply it to your styled components.

1. Bonus: Add animations to the todos using keyframes and styled-components.

1. Example:
    Animate the appearance of a todo item when it is added to the list.
    Add a hover animation effect to make the todo cards visually dynamic.

1. Test your application by styling additional components and ensuring that the theme switch works seamlessly.