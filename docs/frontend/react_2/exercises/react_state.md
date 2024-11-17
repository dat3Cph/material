---
title: UseState
description: Exercises for Frontend Week II
layout: default
nav_order: 2
grand_parent: React II
parent: Exercises
permalink: /frontend/react-2/exercises/usestate
---

# React: useState and useEffect

In this exercise we will create a simple count component using the `useState` hook. We will also make sure that the counter will be persisted across sessions using the `local storage` in the browser.

## 1. Create a React project

1.1 Create a new React app using Vite ([use this guide](../../../toolbox/react/vite.md))

1.2 Open your new web application with visual code

1.3 Remove everything inside the App() function/Component in `App.js`

## 2. useState: Create a simple count component using the useState hook

2.1 Create a component called `Counter.jsx` that has a button which when pressed should increment a count value, initially by one, and print the result in the component. Insert the component in `App.jsx`.

2.2 Add a new button to the component which when pressed, should decrement the count value by one.

2.3 Change the component, so an initial value for count can be passed in via props

2.4 Change the component so the value used for increments can be passed in (if you pass in the number five, the count value should increment/decrement with 5 for each click)

## 3. useEffect and `local storage`

3.1 Add a side effect, using `useEffect`, that can store the count value in your Browsers `Local Storage` so that next time the user accesses the page (after having closed the browser) it will render the count value used last time he visited the page

### Hint

All modern browsers include a `Local Storage` and `Session Storage` area to store values for the current user or session. Open developer tools and check as sketched here.

![LocalStorage](./images/localstorage.png)

The JavaScript API, used to read/write is extremely simple, you can do it like this:

```javscript
localStorage.setItem("count", count);
localStorage.getItem("count") //Returns value as a string
```
