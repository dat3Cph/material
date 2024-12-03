---
title: Styling in React
description: Styling with react library styled-components
layout: default
nav_order: 15
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/styling
---

# Styling with React with Styled Components
Styling in React can be done in a variety of ways. One of the most popular ways is to use a library called styled-components. Styled-components allows you to write CSS in your JavaScript files, which can make your code more readable and maintainable.

## Installation
To get started with styled-components, you need to install it in your project. You can do this by running the following command:

```bash
npm install styled-components
```

## Usage
Once you have installed styled-components, you can start using it in your React components. Here is an example of how you can use styled-components to style a button component:

```jsx
import styled from 'styled-components';

const StyledButton = styled.button`
  background-color: #007bff;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
`;

function App() {
  return (
    <div>
      <StyledButton>Click me</StyledButton>
    </div>
  );
}

export default App;
``` 

## Extened Usage
An example of more styles in a single document. Where we have a header, a navigation menu, a content layout, and an error banner. This example is from an application that uses React Router for routing.

```jsx
import React, {useEffect} from "react";
import styled from "styled-components";
import { Link, useLocation, useNavigate } from "react-router-dom";
import { Outlet } from "react-router-dom"; // Assuming you're using Outlet for nested routes
import "./App.css";

// Header Component
const Header = styled.header`
  background-color: #2d3a3f;
  color: white;
  padding: 20px 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
`;

const Logo = styled.div`
  display: flex;
  align-items: center;
`;

const LogoImg = styled.img`
  height: 40px;
  margin-right: 15px;
`;

const LogoText = styled.h1`
  font-size: 1.8rem;
  color: white;
  margin: 0;
`;

const NavMenu = styled.nav`
  display: flex;
  gap: 30px;
`;

const NavItem = styled(Link)`
  color: white;
  text-decoration: none;
  font-size: 1.1rem;
  &:hover {
    text-decoration: underline;
    font-weight: bold;
  }
`;

// Content Layout
const Content = styled.div`
  display: flex;
  margin-top: 20px;
  height: calc(100vh - 80px);
  color: #333;
`;

const LeftMenu = styled.div`
  width: 200px;
  background-color: #f4f4f4;
  padding: 20px;
`;

const LeftMenuItem = styled(Link)`
  display: block;
  color: #333;
  text-decoration: none;
  margin-bottom: 10px;
  &:hover {
    text-decoration: underline;
  }
`;

const MainContent = styled.div`
  flex: 1;
  padding: 20px;
  background-color: #fafafa;
  border-left: 2px solid #ccc;
  overflow-y: auto; /* Allows scrolling inside the main content if needed */
`;

const ErrorBanner = styled.div`
  background-color: #f8d7da;
  color: #721c24;
  padding: 10px;
  margin-bottom: 20px;
  border-radius: 5px;
`;

const App = () => {
  const [errorMessage, setErrorMessage] = React.useState(null);
  const [showRenderError, setShowRenderError] = React.useState(false);
  // Use useLocation to listen for route changes
  const location = useLocation();
  const navigate = useNavigate();


  // Reset error message on route change
  useEffect(() => {
    setErrorMessage(null);
    setShowRenderError(false);
  }, [location]);

  return (
    <div>
      <Header>
        <Logo onClick={()=>navigate('/')}>
          <LogoImg
            src="https://neh.kea.dk/images/logos/cphbusiness_neg.png"
            alt="Logo"
          />
          {/* <LogoText>Styled App</LogoText> */}
        </Logo>
        <NavMenu>
          <NavItem to="/">Home</NavItem>
          <NavItem to="/about">About</NavItem>
          <NavItem to="/contact">Contact</NavItem>
        </NavMenu>
      </Header>

      <Content>
        <LeftMenu>
          <LeftMenuItem to="/error">Error handling</LeftMenuItem>
          <LeftMenuItem to="/images">Images</LeftMenuItem>
          <LeftMenuItem to="/stories">Stories</LeftMenuItem>
        </LeftMenu>
        <MainContent>
          {errorMessage && <ErrorBanner>{errorMessage}</ErrorBanner>}
          <Outlet
            context={{ setErrorMessage, setShowRenderError, showRenderError }}
          />
        </MainContent>
      </Content>
    </div>
  );
};

export default App;
```

### The main.jsx file
```jsx
import React from 'react';
import * as ReactDOM from "react-dom/client";
import { createBrowserRouter, createRoutesFromElements, Route, RouterProvider } from 'react-router-dom';
// import './index.css'
import App from './App.jsx'

const router = createBrowserRouter(
  createRoutesFromElements(
    <Route path="/" element={<App/>}> 
    <Route path="about" element={<h1>About</h1>} />
    <Route path="*" element={<h1>404 Not Found</h1>} />
    </Route>
  )
);

ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
      <RouterProvider router={router} />
  </React.StrictMode>
);
```