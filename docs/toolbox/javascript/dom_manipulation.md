---
title: DOM manipulation
description: How to manipulate the DOM using JavaScript
layout: default
nav_order: 3
parent: JavaScript
grand_parent: Toolbox
has_children: false
permalink: /toolbox/javascript/dom-manipulation/
---

# How to manipulate the DOM

This is a brief overview of common ways to manipulate the DOM with JavaScript, including adding, modifying, and removing elements or attributes.

## 1. **Selecting Elements**

   Before manipulating the DOM, you need to select the elements you want to interact with. You can use methods like `getElementById`, `querySelector`, or `querySelectorAll`.

   ```javascript
   // Select element by ID
   const title = document.getElementById("title");

   // Select first element with class 'content'
   const content = document.querySelector(".content");

   // Select all paragraphs
   const paragraphs = document.querySelectorAll("p");
   ```

## 2. **Changing Content**

- **Text Content**: Use `textContent` to change the text inside an element.
- **HTML Content**: Use `innerHTML` to set or get the HTML content of an element.

   ```javascript
   // Changing text content
   title.textContent = "New Title";

   // Changing HTML content
   content.innerHTML = "<p>This is new content.</p>";
   ```

## 3. **Changing Attributes**

   Use `setAttribute`, `getAttribute`, or directly access the attribute to modify them.

   ```javascript
   // Set an attribute
   title.setAttribute("class", "new-class");

   // Get an attribute
   console.log(content.getAttribute("id"));

   // Modify directly
   title.id = "updatedTitle";
   ```

## 4. **Changing Styles**

- You can change CSS styles directly by using the `style` property.

   ```javascript
   title.style.color = "blue";
   content.style.fontSize = "20px";
   content.style.display = "none"; // Hide the element
   ```

## 5. **Adding, Removing, and Modifying Classes**

   Use `classList` to manipulate classes on elements.

   ```javascript
   // Add a class
   title.classList.add("highlight");

   // Remove a class
   title.classList.remove("highlight");

   // Toggle a class (adds if not present, removes if present)
   content.classList.toggle("hidden");

   // Check if an element has a class
   console.log(content.classList.contains("hidden"));
   ```

## 6. **Creating and Inserting Elements**

   You can create new elements using `document.createElement`, set their content, and then add them to the DOM using `appendChild` or `insertBefore`.

   ```javascript
   // Create a new paragraph element
   const newParagraph = document.createElement("p");
   newParagraph.textContent = "This is a new paragraph.";

   // Append to a parent element
   content.appendChild(newParagraph);

   // Insert before an existing element
   const firstParagraph = document.querySelector("p");
   content.insertBefore(newParagraph, firstParagraph);
   ```

## 7. **Removing Elements**

   To remove an element, select it and use `removeChild` on its parent or simply use `remove`.

   ```javascript
   // Remove an element by calling remove() on it
   newParagraph.remove();

   // Or use removeChild on the parent
   content.removeChild(firstParagraph);
   ```

## 8. **Event Handling and Manipulation**

   You can add event listeners to elements to make them interactive.

   ```javascript
   title.addEventListener("click", () => {
     alert("Title clicked!");
   });

   // Change content on button click
   const button = document.getElementById("myButton");
   button.addEventListener("click", () => {
     content.textContent = "Content changed on button click!";
   });
   ```

## Example: Putting It All Together

Here’s an example that ties all these manipulations into one script:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>DOM Manipulation Example</title>
</head>
<body>
  <h1 id="title">Original Title</h1>
  <div class="content">
    <p>This is the original content.</p>
  </div>
  <button id="myButton">Change Content</button>

  <script>
    // Select elements
    const title = document.getElementById("title");
    const content = document.querySelector(".content");
    const button = document.getElementById("myButton");

    // Change text and style
    title.textContent = "Updated Title";
    title.style.color = "green";

    // Add event listener to button
    button.addEventListener("click", () => {
      // Create a new element
      const newParagraph = document.createElement("p");
      newParagraph.textContent = "This is added content!";
      content.appendChild(newParagraph);

      // Toggle the title's color on click
      title.style.color = title.style.color === "green" ? "blue" : "green";
    });
  </script>
</body>
</html>
```

In this example:

- We modify the title’s text and color.
- Add a new paragraph each time the button is clicked.
- Toggle the title color between green and blue on each button click.

These techniques cover the most common ways to manipulate the DOM, giving you the tools to create dynamic, interactive web pages.
