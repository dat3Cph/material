---
title: Styled Components
description: Styled components in React
layout: default
nav_order: 14
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/styled_components
---

# Styled Components in React

![Codelab](./images/reactlogo.png){: style="display: block; margin: 0 auto; width:50%" }

### What is Styled-Components?

Styled-components is a popular **CSS-in-JS** library for React and React Native applications. It allows you to write CSS directly in your JavaScript code, scoped to specific components, ensuring clean and modular styling.

### Key Features

1. **CSS-in-JS**:
   - Write CSS styles directly within your JavaScript files using template literals.
   - Combine styles and logic in the same component, improving maintainability.

2. **Scoped Styles**:
   - Automatically generates unique class names for each component, ensuring no CSS conflicts.

3. **Dynamic Styling**:
   - Styles can adapt to props, enabling conditional and theme-based styling.

4. **Theme Support**:
   - Offers a built-in `ThemeProvider` for managing light/dark modes or global styling themes.

5. **Component-Based Styling**:
   - Each styled component is self-contained, promoting reuse and modular design.

6. **Server-Side Rendering (SSR)**:
   - Fully compatible with SSR frameworks like Next.js, ensuring styled-components work well for SEO and performance.

---

### How Styled-Components Work

0. **Installation**:
   Install styled-components using npm or yarn.

   ```bash
   npm install styled-components
   ```

1. **Creating a Styled Component**:
   Styled-components generates unique class names and injects the styles into the DOM at runtime.

   ```react
   import styled from 'styled-components';

   const Button = styled.button`
     background-color: blue;
     color: white;
     padding: 10px 20px;
     border-radius: 5px;
     border: none;
     cursor: pointer;

     &:hover {
       background-color: darkblue;
     }
   `;

   function App() {
     return <Button>Click Me</Button>;
   }
   ```

2. **Dynamic Styling with Props**:
   Styles can react to props passed to the component.

   ```react
   const Button = styled.button`
     background-color: ${({ primary }) => (primary ? 'blue' : 'gray')};
     color: white;
     padding: 10px 20px;
     border-radius: 5px;
   `;

   function App() {
     return (
       <div>
         <Button primary>Primary Button</Button>
         <Button>Default Button</Button>
       </div>
     );
   }
   ```

3. **Global Styles**:
   Use `createGlobalStyle` to define styles that apply globally to the application.

   ```react
   import { createGlobalStyle } from 'styled-components';

   const GlobalStyle = createGlobalStyle`
     body {
       margin: 0;
       font-family: Arial, sans-serif;
     }
   `;

   function App() {
     return (
       <>
         <GlobalStyle />
         <h1>Hello World</h1>
       </>
     );
   }
   ```

4. **Theming**:
   Styled-components support a `ThemeProvider` for managing themes.

   ```react
   import { ThemeProvider } from 'styled-components';

   const theme = {
     colors: {
       primary: 'blue',
       secondary: 'gray',
     },
   };

   const Button = styled.button`
     background-color: ${({ theme }) => theme.colors.primary};
     color: white;
     padding: 10px 20px;
   `;

   function App() {
     return (
       <ThemeProvider theme={theme}>
         <Button>Click Me</Button>
       </ThemeProvider>
     );
   }
   ```

---

### Benefits of Styled-Components

1. **Encapsulation**:
   - Ensures styles are scoped to components, preventing accidental CSS overrides.

2. **Dynamic Styling**:
   - Easily adapt styles based on props or application state.

3. **Developer Experience**:
   - Offers syntax highlighting, auto-completion, and linting support.

4. **Maintainability**:
   - Combines styles and components, reducing the need for separate CSS files.

5. **Performance**:
   - Minimizes unused CSS by injecting only the styles needed for the components rendered.

---

### Use Cases

- **Themed Applications**: Managing light/dark mode or custom themes.
- **Component Libraries**: Building reusable UI components with scoped styles.
- **Rapid Prototyping**: Quickly styling components without external stylesheets.

---

### Comparison to Traditional CSS

| Feature                     | Styled-Components      | Traditional CSS         |
|-----------------------------|------------------------|-------------------------|
| **Scoping**                 | Automatic (unique class names) | Manual (BEM, CSS Modules) |
| **Dynamic Styling**          | Built-in (via props)  | Requires JavaScript logic |
| **Theme Management**         | Built-in             | Manual implementation    |
| **Code Separation**          | Styles in JS         | Styles in separate files |
| **CSS Conflicts**            | Avoided              | Possible without scoping |

---

Styled-components simplifies the process of managing styles in modern React applications, promoting modularity, reusability, and a seamless developer experience.
