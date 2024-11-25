---
title: JS Basics
description: Exercises for Frontend Week I
layout: default
nav_order: 1
grand_parent: JS and React I
parent: Exercises
permalink: /frontend/javascript-react-intro/exercises/js-basics
---

# Exercise 1: Getting comfortable with arrays, filter, map, and forEach

**Make this exercise in Visual Studio Code and node.js.**

1.1 Declare a JavaScript array and initialize it with some names (Lars, Jan, Peter, Bo, Frederik etc.). Use the filter method to create a new array with only names of length `<=3`.
Use the forEach method to iterate and print (console.log) both the original and the new array.

1.2 Use the names-array created above, and, using its map method, create a new array with all names uppercased.

1.3 Use map, join + just a little bit more to create a function, which given the array of names, for example: ["Lars", "Peter", "Jan", "Ian"] returns a string with the HTML for the names in an `<ul>` as sketched below:

```html
<ul>
  <li>Lars</li>
  <li>Peter</li>
  <li>Jan</li>
  <li>Ian</li>
<ul>
```

The output above was shown with newlines for readability, but this is actually what we want (why):

```html
<ul><li>Lars</li><li>Peter</li><li>Jan</li><li>Ian</li><ul>
```

In exercise 2, we will use DOM manipulation and place this into a “running” web-page.

1.4  Given this JavaScript array:

```javascript
let cars = [
  { id: 1, year: 1997, make: 'Ford', model: 'E350', price: 3000 },
  { id: 2, year: 1999, make: 'Chevy', model: 'Venture', price: 4900 },
  { id: 3, year: 2000, make: 'Chevy', model: 'Venture', price: 5000 },
  { id: 4, year: 1996, make: 'Jeep', model: 'Grand Cherokee', price: 4799 },
  { id: 5, year: 2005, make: 'Volvo', model: 'V70', price: 44799 }
];
```

1.4.1 Use the filter function to get arrays with only:

- Cars newer than 1999
- All  Volvo’s
- All cars with a price below 5000

1.4.2 Use `map`, `join` + just a little bit more to implement a function, that given the cars array used above, will create, and return a string with valid SQL statements to insert the data into a table with matching column names (id, year, make, model, price) as sketched below:

```sql
INSERT INTO cars (id,year,make,model,price) VALUES ( 1, 1997 'Ford','E350', 3000 );
...
```
