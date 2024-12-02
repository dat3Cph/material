---
title: Errorhandling in React
description: 3 types of errors and how to handle them in a React application
layout: default
nav_order: 14
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/error-handling
---

# Error handling in a react application

## 3 types of errors
1. **JS runtime errors**: These are errors that occur when the code is running. These are the most common type of errors and are usually caused by a mistake in the code.
2. **Network errors**: These are errors that occur when the application is trying to communicate with a server. These errors are usually caused by a problem with the network connection.
3. **React render errors**: These are errors that occur when the React application is rendering. These errors are usually caused by a problem with the React code.

## How to handle errors in React
1. **JS runtime errors**: To handle JS runtime errors, you can use the `try...catch` statement. This statement allows you to catch errors that occur in a block of code and handle them gracefully. In this example the ErrorProvoker component shows 3 buttons.
  - 1. button throws a JS runtime error
  - 2. button throws a network error
  - 3. button throws a React render error

The 2 first errors are shown in an error banner at the top of the App component. The last error is shown in the error page provided with the react router routes errorElement

- This way we can handle React render errors only on pages where it is more likely to occur because of the complexity of the page or the use of third-party libraries that might throw errors.

## Globally handle type 1 and 2 errors
```javascript

  // Global error handler (window.onerror and unhandledrejection)
  function setupGlobalErrorHandlers() {
    window.onerror = (message, source, lineno, colno, error) => {
      console.error("Global error caught:", { message, source, lineno, colno, error, });
      
      setErrorMessage("A global JavaScript error occurred!", error.message);
    };

    //
    window.onunhandledrejection = (event) => {
      console.error("Unhandled promise rejection:", event.reason);
      setErrorMessage("An unhandled promise rejection occurred!", event.reason);
    };
  }
  // Call this setup when the app starts
  setupGlobalErrorHandlers();
  export { setupGlobalErrorHandlers };

```

## Setup a test component to handle the errors
```javascript
const ErrorProvoker = ({setErrorMessage, setShowRenderError}) => {

  // Handle runtime JS errors in event handlers
  const handleThrowError = () => {
    try {
      throw new Error("An error occurred in the event handler!");
    } catch (error) {
      console.error("Caught in event handler:", error);
      setErrorMessage(error.message); // Update error message
    }
  };

  // Handle async HTTP errors
  const handleAsyncError = async () => {
    try {
      const response = await fetch("https://jsonplaceholder.typicode.com/404");
      if (!response.ok) {
        throw new Error(
          `HTTP Error: ${response.status} - ${response.statusText}`
        );
      }
      await response.json();
    } catch (error) {
      console.error("Caught async error:", error);
      setErrorMessage(error.message); // Update error message
    }
  };

  const handleRenderError = () => {
    console.error("Triggering React render error...");
      setShowRenderError(true);
  };

    return (<>
      <h1>React Error Handling Demo</h1>

      {/* Buttons to trigger different errors */}
      <button onClick={handleThrowError}>Throw JS Error</button>
      <button onClick={handleAsyncError} style={{ marginLeft: "10px" }}> Trigger Async HTTP Error </button>
      <button onClick={handleRenderError} style={{ marginLeft: "10px" }} > Trigger React Render Error </button>

      

    </>);
}
export default ErrorProvoker;
```

### App.jsx with error banner
```jsx
import { useState } from "react";
import "./App.css";
import { Outlet } from "react-router-dom";

import ErrorBanner from "./ErrorBanner";
import ErrorProvoker from "./ErrorProvoker";
import { setupGlobalErrorHandlers } from "./globalErrorHandling";

setupGlobalErrorHandlers();

function App() {
  const [errorMessage, setErrorMessage] = useState(null); // Track error messages
  const [showRenderError, setShowRenderError] = useState(false); // Trigger render error


  return (
    <div>
      <ErrorBanner errorMessage={errorMessage} />
      <ErrorProvoker setErrorMessage={setErrorMessage} setShowRenderError={setShowRenderError} />

      <Outlet context={{showRenderError}}/>
    </div>
  );
}

export default App;
```

### ErrorBanner.jsx
```jsx
function ErrorBanner({ errorMessage }) {
  return (
    errorMessage && (
      <div style={{ backgroundColor: "red", color: "white", padding: "10px" }}>
        <strong>Error:</strong> {errorMessage}
      </div>
    )
  );
}

export default ErrorBanner;

```

### Router with errorElement in main.jsx
```jsx
import "./index.css";
import {
  createBrowserRouter,
  Route,
  createRoutesFromElements,
  RouterProvider,
} from "react-router-dom";
import ReactDOM from "react-dom/client";
import React from "react";
import App from "./App";
import { useRouteError } from "react-router-dom";
import Content from "./Content";

export default function ErrorPage() {
  const error = useRouteError();
  console.error(error);

  return (
    <div id="error-page">
      <h1>Oops!</h1>
      <p>Sorry, an unexpected error has occurred.</p>
      <p>
        <i>{error.statusText || error.message}</i>
      </p>
    </div>
  );
}

const router = createBrowserRouter(
  createRoutesFromElements(
    <Route path="/" element={<App />}  >
      <Route index element={<Content/>} errorElement={<ErrorPage/>}/>
    </Route>
  )
);


ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
      <RouterProvider router={router} />
  </React.StrictMode>
);

```

### Content.jsx
```jsx
import { useOutletContext } from "react-router-dom";

// A component that throws a React render error
function ErrorThrowingComponent() {
  throw new Error("Our custom error occurred in the React component!");
}
const Content = () => {
  const { showRenderError } = useOutletContext();
  console.log(showRenderError);
  return (
    <div>
      <h1>Content</h1>
      {showRenderError}
      {/* Provoke the React render error */}
      {showRenderError && <ErrorThrowingComponent />}


    </div>
  );
}

export default Content;
```
