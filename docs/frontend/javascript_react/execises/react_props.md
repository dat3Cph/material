---
title: React Props
description: Exercises for Frontend Week I
layout: default
nav_order: 11
grand_parent: JS and React I
parent: Exercises
permalink: /frontend/javascript-react-intro/exercises/components-props/
---

# React 2: Composing Components

The next two exercises focus on props and how to pass props into components. So make sure to [read about props](https://react.dev/learn/passing-props-to-a-component) first, they are one of the top-5 MOST IMPORTANT PARTS to understand in React.

## 2.1 Props

Here you will make a react component in a separate file and export it. The component uses another component 3 times with different effect/content.

In the src folder, add a new file `file3.jsx`, and `import React` in the first line.
Copy the two functions below into this file (remember to export to your App component):

```react
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

```react
function MultiWelcome() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edith" />
    </div>
  );
}
```

Make sure you understand why the parenthesis is needed after the return statement in the `MultiWelcome` component, and not in the `Welcome` component.

In `App.js` create a new h2 headline for Ex3 and render the MultiWelcome component under the headline (remember to import it)

Hint: after `</h2>` put: `<MultiWelcome/>`

Verify that your new component is rendered

## 2.2 Props and Destructuring

Let's make the example above a bit more interesting.
First, open `file2.js` and add this export to the file:

```javascript
export const persons = [
{firstName:"Kurt",lastName:"Wonnegut",gender: "Male",email: "k@wonnegut.dk", phone: "12345"},
{firstName:"Jane",lastName:"Wonnegut",gender:"female",email:"j@wonnegut.dk", phone: "12345"},
{firstName:"ib",lastName: "Wonnegut",gender : "Male",email: "i@wonnegut.dk", phone: "12345"},
];
```

In `File3.js`, import persons  and add a new functional Component (below the Welcome Component) called `WelcomePerson`.

This component should take a full person object as parameter/props and it should render firstName, lastName and email for this person.

In the MultiWelcome component, below the three usages of the original Welcome component add three usages of the new component as sketched here:

```jsx
<WelcomePerson person={persons[0]}  />
```

Hint: In the `WelcomePerson` function, the person is available in the arguments as `props.person` or if using destructuring (`{person}`) just as person.

Handle list of persons of arbitrary sizes. In the example above your “list” could only handle exactly three persons. Use our old friend `map()` below the three hardcoded lines in the MultiWelcome component to something similar to this (fill in the few missing parts - where the dots are):

```javascript
{ persons.map((  ....    )=><WelcomePerson  ....      />) }
```

This will probably provide a nasty warning in the console. Read about [keys](https://react.dev/learn/rendering-lists) here (a topic for next week) to solve this problem.
