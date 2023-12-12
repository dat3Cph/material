
# Exam Questions for Frontend

## JavaScript

1. Explain the concept of prototypes in JavaScript.
2. What are higher-order functions in JavaScript? Give an example.
3. What are the purposes and differences between the package.json and package-lock.json files?
4. What is a callback function in JavaScript and when would you use one?
5. Explain the concept of promises in JavaScript. How do they differ from callbacks?
6. What is the difference between synchronous and asynchronous programming and how does async and await fit into this?
7. Explain the concept of event bubbling in JavaScript.
8. What is the difference between localStorage and sessionStorage in JavaScript?
9. What is the scope of a variable in JavaScript? Explain the difference between global and local scope.
10. What is the purpose of the window object in JavaScript?

## React

1. Component Basics:
- What is a React component?
-     Explain the benefits of using components compared to how you would build a web application in vanilla javascript.
2. JSX:
- What is JSX? Provide an example.
- How does JSX differ from HTML?
3. Props and State:
- Describe the purpose of props in React.
- Explain the role of state in a React component.
3. Component Lifecycle in functional components:
- What is the purpose of the useEffect hook?
- Explain the need for the deps array in the useEffect hook.
4. Handling Events:
- How are events handled in React compared to vanilla javascript?
- Show examples of how to handle form submit events, and how to handle input change events.
5. Conditional Rendering:
- Describe how conditional rendering is achieved in React.
- Provide an example of using the ternary operator for conditional rendering.
6. Lists and Keys:
- What is the purpose of the key attribute in React lists?
- Explain how the map function is used for rendering lists in React.
7. Forms in React:
- How are controlled components different from uncontrolled components in React forms?
- Explain the role of the onChange event in form handling and show examples.
8. React Hooks:
- What are React Hooks? Provide examples of at least two built-in hooks.
- Explain the difference between useState and useEffect.
9. Error Handling:
- Explain the following code:
```jsx
import React, { useState, useEffect } from 'react';

const ErrorBoundary = ({ children }) => {
  const [hasError, setHasError] = useState(false);

  useEffect(() => {
    // The effect runs when an error occurs in any child component
    const handleError = (error, info) => {
      console.error('Error caught by error boundary:', error, info);
      setHasError(true);
    };

    // Attach the error handler to the window's error event
    window.addEventListener('error', handleError);

    // Clean up the event listener when the component unmounts
    return () => {
      window.removeEventListener('error', handleError);
    };
  }, []); // Empty dependency array ensures the effect runs only once

  if (hasError) {
    // Render fallback UI when an error occurs
    return <h1>Something went wrong.</h1>;
  }

  // Render children as usual if no error occurred
  return children;
};

// Example usage of the error boundary
const MyComponent = () => {
  // Wrap the component tree with the error boundary
  return (
    <ErrorBoundary>
      {/* The rest of the component tree goes here */}
    </ErrorBoundary>
  );
};

```
- Show example of how you handle errors in React.
10. Lifting State Up:
- What is the purpose of lifting state up in React?
- Show how you would lift state up in a React application.


## React Router, security, styling, and deployment

### React Router

1.a. Explain what React Router is and its purpose in a React application.

1b. Show an example of how routing works in React

2.a. Explain how navigation works in React, and the difference from how it's done in a multipage application.

2.b. Show an example of how navigation can be implemented in React

3.a. Explain how sub routing is working

3.b. Show an example of using sub routing with the <Outlet/> element.

### Security in React and SPA

4.a. Describe conceptually the typical flow of using JWTs for user authentication in a React application.

5.a. Describe and show how we log in a user in React with JWT.

6.a. Describe conceptually what Same Origin Policy and CORS is, and how we avoid getting CORS errors when fetching data from an API.

### Styling

7.a. Describe the purpose of `flexbox` and `grid` in css, and show some examples of what can be achieved by applying them.

8.a. Describe the purpose of media queries, and show some examples of what can be achieved by applying them.

9.a. Describe some important design principles when developing a website that should be working well on mobile, tablet, as well as desktop browsers.
9.b. Show a few examples of responsive .

### Deployment

10.a. Describe conceptually how we deploy a React frontend application to a docker container on a virtual machine.

11.b. Describe how we get our own domain name working on our deployed website.

12.c. Describe conceptually what HTTPS is and how we got it working on our deployed websites.