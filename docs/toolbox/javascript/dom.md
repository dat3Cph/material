---
title: The DOM
description: What is the DOM?
layout: default
nav_order: 1
parent: JavaScript
grand_parent: Toolbox
has_children: false
permalink: /toolbox/javascript/dom/
---

# What is the DOM?

The **DOM (Document Object Model)** is a programming interface for web documents. It represents the structure of an HTML or XML document as a **tree of nodes** where each part of the document (elements, attributes, text content) is a node. This structure allows programming languages, like JavaScript, to interact with and manipulate the document dynamically.

### Key Characteristics of the DOM

1. **Tree Structure**:
   - The DOM organizes a web document into a hierarchical structure known as a **DOM tree**.
   - The tree structure starts with the **document node** at the top, and branches down to elements, attributes, and text nodes.
   - Every HTML tag becomes an **element node**, each attribute within those tags becomes an **attribute node**, and any text becomes a **text node**.

   For example, consider this HTML document:

   ```html
   <!DOCTYPE html>
   <html>
     <body>
       <h1>Hello, world!</h1>
       <p>This is a paragraph.</p>
     </body>
   </html>
   ```

   The corresponding DOM tree structure would look like this:

   ```plaintext
   Document
   └── html
       └── body
           ├── h1
           │   └── "Hello, world!"
           └── p
               └── "This is a paragraph."
   ```

2. **Nodes**:
   - In the DOM, each part of the document is represented by a **node**.
   - There are different types of nodes:
     - **Element Nodes**: Represent HTML tags (like `<body>`, `<h1>`, `<p>`).
     - **Text Nodes**: Represent the text within elements.
     - **Attribute Nodes**: Represent the attributes of elements (like `class="example"`).
     - **Document Node**: The top-level node representing the entire document.

3. **JavaScript and the DOM**:
   - The DOM is a **bridge between JavaScript and HTML**.
   - JavaScript can use the DOM to:
     - Select elements and read or modify their content and attributes.
     - Add or remove elements and nodes dynamically.
     - Respond to user events (like clicks, keyboard input) by modifying the DOM in real-time.

4. **Live Representation**:
   - The DOM is a **live** representation of the document. If the document changes (either through user actions or JavaScript code), the DOM updates to reflect those changes instantly.
   - This live representation enables dynamic, interactive webpages where elements can be modified, added, or removed in response to user interactions.

5. **The Browser’s Role**:
   - When a web page is loaded, the browser reads the HTML and constructs the DOM tree. JavaScript running in the browser can then access this tree structure and manipulate it.
   - Each browser provides the DOM as part of its **Web API**, enabling developers to interact with HTML and CSS in a standardized way.

### Why the DOM is Important

The DOM is crucial for creating **dynamic, interactive webpages**. By giving JavaScript access to the structure and content of a webpage, it allows developers to:

- Change the content, style, and layout of a webpage without reloading.
- Add or remove elements in response to user actions.
- Manage events, animations, and other interactive features.

In essence, the DOM transforms a static HTML document into an interactive, programmable structure that JavaScript can control, making it the foundation of modern web development.

## How to Access the DOM

JavaScript provides several methods to access and manipulate the DOM. Here are some common ways select DOM elements:

- [DOM selection](./dom_selection.md)

Once you have selected an element, you can interact with it in various ways:

- [DOM manipulation](./dom_manipulation.md)
