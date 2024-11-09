---
title: DOM selection
description: How to select elements in the DOM using JavaScript.
layout: default
nav_order: 1
parent: JavaScript
grand_parent: Toolbox
has_children: false
permalink: /toolbox/javascript/dom-selection/
---

# DOM selection

When working with the DOM in a browser, there are plenty of ways to select elements. The most common method is `document.getElementById(..)`, which selects an element by its ID attribute. However, there are other methods that provide more flexibility and power when selecting elements based on different criteria. In this article, we'll explore some alternatives to `getElementById(..)` and discuss their benefits.

### 1. **`document.querySelector(..)`**

- **Description**: Selects the first element that matches a specified CSS selector.
- **Example**:

     ```javascript
     const element = document.querySelector("#myId"); // Select by ID
     const elementByClass = document.querySelector(".myClass"); // Select by class
     const elementByAttribute = document.querySelector("[data-attribute='value']"); // Select by attribute
     ```

- **Benefit**: More flexible than `getElementById` because it works with any CSS selector, not just IDs.

### 2. **`document.querySelectorAll(..)`**

- **Description**: Selects all elements that match a specified CSS selector and returns a `NodeList` (similar to an array but not quite).
- **Example**:

     ```javascript
     const elements = document.querySelectorAll(".myClass"); // Selects all elements with class `myClass`
     elements.forEach(element => {
       // Do something with each element
     });
     ```

- **Benefit**: Great for working with multiple elements, enabling you to iterate over them with `forEach` or convert them to arrays if needed.

### 3. **`document.getElementsByClassName(..)`**

- **Description**: Selects all elements with a given class name and returns an `HTMLCollection` (a live collection, meaning it updates if the DOM changes).
- **Example**:

     ```javascript
     const elements = document.getElementsByClassName("myClass");
     ```

- **Benefit**: Fast and efficient for selecting multiple elements by class, but less flexible than `querySelectorAll` because it only works with class names.

### 4. **`document.getElementsByTagName(..)`**

- **Description**: Selects all elements with a specified tag name, such as `div`, `p`, or `input`.
- **Example**:

     ```javascript
     const divs = document.getElementsByTagName("div");
     ```

- **Benefit**: Useful when you need to select elements by tag, like all `div` or `input` elements.

### Summary

For most cases, `querySelector` and `querySelectorAll` are the best alternatives due to their flexibility with CSS selectors. They can select by ID, class, attribute, or any complex selector combination, making them more powerful and versatile than `getElementById`.
