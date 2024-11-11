---
title: DOM Event Bubbling 
description: How to catch events in child elements in the DOM
layout: default
nav_order: 4
parent: JavaScript
grand_parent: Toolbox
has_children: false
permalink: /toolbox/javascript/dom-event-bubbling/
---

# How to catch events in child elements in the DOM

In JavaScript, event bubbling is a mechanism in the Document Object Model (DOM) where an event triggered on a child element "bubbles up" through its ancestors, all the way up to the root of the DOM (typically the `document` object). This means that if an event is triggered on a child element, any ancestor elements with handlers for the same event type can also receive and handle that event.

## How Event Bubbling Works

1. **Triggering an Event**: When a user action (like a `click`) occurs on an element, the event is triggered on that element first.

2. **Bubbling Phase**: After the event is triggered on the initial element, it starts bubbling up through the parent elements, moving through each ancestor, until it reaches the top of the DOM hierarchy (usually `document`).

3. **Event Propagation**: At each ancestor level, if an event handler for the same event type exists, it will be executed. The event keeps propagating upward unless explicitly stopped.

## Example

Consider this HTML structure:

```html
<div id="parent">
  <button id="child">Click Me</button>
</div>
```

And JavaScript with event handlers on both elements:

```javascript
document.getElementById("parent").addEventListener("click", function() {
  console.log("Parent Div clicked");
});

document.getElementById("child").addEventListener("click", function() {
  console.log("Button clicked");
});
```

When the button (`#child`) is clicked:

1. The `click` event is triggered on the button itself, and "Button clicked" is logged.
2. Then, because of bubbling, the event propagates to the parent div, and "Parent Div clicked" is also logged.

## Stopping Event Bubbling

To stop the event from bubbling up to parent elements, you can use the `stopPropagation` method on the event object:

```javascript
document.getElementById("child").addEventListener("click", function(event) {
  console.log("Button clicked");
  event.stopPropagation(); // Stops the event from bubbling up
});
```

With `stopPropagation`, only "Button clicked" will be logged, as the event is prevented from reaching the parent element.

## Use Cases and Considerations

Event bubbling is useful for event delegation, where a single event listener on a parent element can handle events for multiple child elements. However, it’s also essential to manage bubbling properly, as unwanted propagation can lead to unexpected behavior if parent elements handle events unintentionally.

To access DOM elements within the child element that triggered the bubbling, you can utilize the `event` object passed into the event handler. The `event.target` property provides a reference to the exact element that triggered the event (the *source element*), allowing you to work directly with its properties or child elements, even when the event handler is set on a parent due to event bubbling.

## Accessing the Child Element and Its Children

In a scenario where an event handler is attached to a parent element, but a child element triggers the event, you can access the child element that actually initiated the event using `event.target`. Here’s an example illustrating how this works:

```html
<div id="parent">
  <button id="child">Click Me</button>
</div>
```

And in JavaScript:

```javascript
document.getElementById("parent").addEventListener("click", function(event) {
  console.log("Event triggered by:", event.target); // Access the child element that triggered the event
  if (event.target.tagName === "BUTTON") {  // Check if the event came from a button
    console.log("Button text is:", event.target.textContent); // Access content of the button
  }
});
```

## Explanation

- **`event.target`**: This property always references the element that directly triggered the event, even when the handler is set up on a parent element due to bubbling. In this case, `event.target` will be the `<button id="child">` element if the button is clicked.

- **`event.currentTarget`**: In contrast, `event.currentTarget` refers to the element to which the event handler is actually attached. So, in the example above, `event.currentTarget` will always be the `#parent` div, regardless of which child element within `#parent` triggered the event.

## Working with Child Elements within the Triggering Element

If you need to access specific child elements within the `event.target`, you can use standard DOM methods on it, like `querySelector`, `querySelectorAll`, or any other DOM traversal methods.

For instance, if `event.target` has child elements, you could do something like this:

```javascript
document.getElementById("parent").addEventListener("click", function(event) {
  console.log("Event triggered by:", event.target);
  if (event.target.tagName === "BUTTON") {
    // Access a child within the button, assuming it has a span or other nested element
    let innerSpan = event.target.querySelector("span");
    if (innerSpan) {
      console.log("Span content:", innerSpan.textContent);
    }
  }
});
```

## Example Use Case: Event Delegation with Access to Specific Children

Event bubbling allows for efficient event handling through delegation, where a single listener on a parent can manage events for multiple children. Here's a more advanced example:

```html
<ul id="list">
  <li data-id="1">Item 1</li>
  <li data-id="2">Item 2</li>
  <li data-id="3">Item 3</li>
</ul>
```

JavaScript for handling clicks on list items via a single parent handler:

```javascript
document.getElementById("list").addEventListener("click", function(event) {
  if (event.target.tagName === "LI") { // Check if an LI was clicked
    console.log("Clicked item ID:", event.target.dataset.id); // Access data attribute on LI
    console.log("Clicked item content:", event.target.textContent); // Access content of the clicked item
  }
});
```

Here, using `event.target.dataset.id`, we can access the `data-id` attribute directly from the list item that triggered the event, without needing to add a separate listener for each item.

## Summary

- Use `event.target` to access the specific child element that triggered the event.
- Use `event.currentTarget` to access the element on which the event handler is bound.
- You can access the child elements within `event.target` by using DOM methods (`querySelector`, `dataset`, etc.) directly on `event.target`.
