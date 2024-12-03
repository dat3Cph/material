---
title: Styled Components Theming
description: Styled components in React
layout: default
nav_order: 15
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/styled_components_theming
---
# Light / Dark Theme with Styled Components in React

Creating a light/dark theme for a simple React website using styled-components involves the following steps:

## 1. **Install Styled-Components**

If you haven't already, install styled-components in your React project:

```bash
npm install styled-components
```

## 2. **Set Up a Theme Provider**

Use the `ThemeProvider` from styled-components to apply themes throughout your app.

### Create a theme file

Create a `theme.js` file (or name it as you prefer) in your project:

```javascript
// theme.js
export const lightTheme = {
  body: '#FFFFFF',
  text: '#000000',
  toggleBorder: '#FFF',
  background: '#363537',
};

export const darkTheme = {
  body: '#000000',
  text: '#FFFFFF',
  toggleBorder: '#6B8096',
  background: '#999',
};
```

## 3. **Create Global Styles**

Define global styles that react to the theme. Use the `createGlobalStyle` function:

```javascript
// GlobalStyles.js
import { createGlobalStyle } from 'styled-components';

export const GlobalStyles = createGlobalStyle`
  body {
    background-color: ${({ theme }) => theme.body};
    color: ${({ theme }) => theme.text};
    font-family: 'Arial', sans-serif;
    transition: all 0.25s linear;
  }
`;
```

## 4. **Set Up Theme Toggling Logic**

Create a component or context for toggling between light and dark themes:

```react
// ThemeToggle.js
import React, { useState } from 'react';
import { ThemeProvider } from 'styled-components';
import { lightTheme, darkTheme } from './theme';
import { GlobalStyles } from './GlobalStyles';

const ThemeToggle = ({ children }) => {
  const [theme, setTheme] = useState('light');

  const toggleTheme = () => {
    setTheme((current) => (current === 'light' ? 'dark' : 'light'));
  };

  const currentTheme = theme === 'light' ? lightTheme : darkTheme;

  return (
    <ThemeProvider theme={currentTheme}>
      <GlobalStyles />
      <button onClick={toggleTheme}>
        Switch to {theme === 'light' ? 'Dark' : 'Light'} Mode
      </button>
      {children}
    </ThemeProvider>
  );
};

export default ThemeToggle;
```

## 5. **Use the ThemeToggle Component**

Wrap your app in the `ThemeToggle` component:

```react
// App.js
import React from 'react';
import ThemeToggle from './ThemeToggle';

function App() {
  return (
    <ThemeToggle>
      <div>
        <h1>Hello, World!</h1>
        <p>This is a light/dark themed website.</p>
      </div>
    </ThemeToggle>
  );
}

export default App;
```

## 6. **Style Specific Components**

You can use the `theme` prop in styled-components to create styled elements that adapt to the theme:

```react
// ExampleComponent.js
import styled from 'styled-components';

const StyledButton = styled.button`
  background-color: ${({ theme }) => theme.body};
  color: ${({ theme }) => theme.text};
  border: 2px solid ${({ theme }) => theme.toggleBorder};
  padding: 10px 20px;
  cursor: pointer;

  &:hover {
    background-color: ${({ theme }) => theme.background};
  }
`;

export default StyledButton;
```

Use `StyledButton` in your app:

```react
import React from 'react';
import StyledButton from './ExampleComponent';

const AppContent = () => (
  <div>
    <h2>Styled Component Example</h2>
    <StyledButton>Click Me</StyledButton>
  </div>
);

export default AppContent;
```

## Result

This setup enables a toggle between light and dark themes. The colors and styles defined in your `theme.js` file dynamically update throughout the app based on the current theme.
