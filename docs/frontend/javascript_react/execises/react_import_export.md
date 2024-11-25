---
title: React Import/Export
description: Exercises for Frontend Week I
layout: default
nav_order: 10
grand_parent: JS and React I
parent: Exercises
permalink: /frontend/javascript-react-intro/exercises/import-export/
---



# React 1: Import/export + spread, and destructuring

This exercise is about structuring your React app into parts and learning more about Javascript.

## 1.1 Create a React project

1.1 Create a new React app using Vite ([use this guide](../../../toolbox/react/vite.md))

1.2 Open your new web application with visual code

1.3 Remove everything inside the App() function/Component in `App.js`

## 1.2 Understanding ES6 Modules – import and export

This exercise is about splitting a Javascript file into several parts, and putting the pieces together in a modular fashion.

Skim through this article on [import and export of modules in Javascript](https://www.freecodecamp.org/news/javascript-modules/).

1.2.1 In the src folder, create a new JavaScript file called `file1.js` and paste in the following content:

```javascript
export const text1 = "Hello";
export const text2 = "Hello World";
export const text3 = "Hello Wonderful World";

export default function upper(str){
  return str.toUpperCase();
}
```

Observe how we export "many" named values using the export keyword, and a single value using export default. Usually, it's not recommended to mix default exports with “named” exports. However, for simplicity, we do it here.
What you export as default (only one value pr. file) must be imported like this:

```javascript
import upper from "./file1";
```

What you export as named (non-default) exports will be exported as one single object (containing the three properties `text1`, `text2`, `text3`) and must be included with the Object Destructuring syntax, see below:

```javascript
import {text1,text2, text3} from "./file1";
```

You can import it all, as sketched below:

```javascript
import upper, {text1,text2, text3} from "./file1";
```

1.2.2 Import the three strings, and the function in `App.js`, and add a h2 element: `<h2>Ex 1</h2>` and four `<p>` tags that will print the imported variables. Remember the default export is a function, so call it with a default value like:

```jsx
<p>{upper("please uppercase me")}</p>
```

## 3 Spread operator: Object and Array Destructuring

1.3.1 Skim this article first for a "[dead Simple intro to Destructuring JavaScript Objects](http://wesbos.com/destructuring-objects/)" and this "[Spread syntax (...)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)"

3.2 Create a new file: `file2.js` to hold only a single object and export it like below:

```javascript
const obj = {
  firstName: "Kurt",
  lastName: "Wonnegut",
  gender : "Male",
  email: "kurt@wonnegut.dk"
  }
export default obj
```

In `App.js` import the object from `file2.js` and put it in a variable: `person`

Implement a one-liner (using destructuring ...) to initialize (only) two variables, firstName and email.

Add a new `h2` element with headline: Ex2 and a `<p>` element, that prints firstName, email.

Add these lines to `file2.js`:

```javascript
export const males = ["Peter","Jan"];
export const females = ["Janne","Sarah"];
```

And import them in `App.js`

Use array destructuring and the spread syntax to create a few one-liners that will print out (use console.log()) these values (in the given order):

```javascript
["Peter", "Jan", "Janne", "Sarah"]
```

And this:

```javascript
["Peter", "Jan", "Kurt", "Helle", "Janne", "Sarah", "Tina"]
```

(Extra) Use Object Destructuring and the spread syntax, to create a new object `personV2` from person, but with two new fields: phone and friends. The last one must be initialized with the values from males and females (must be done as a simple one-liner). Console log the value, which should print something similar to this:

```console
email: "kurt@wonnegut.dk"
firstName: "Kurt
friends: ["Peter", "Jan", "Janne", "Sarah"]
gender: "Male"
lastName: "Wonnegut"
phone: 123456
```
