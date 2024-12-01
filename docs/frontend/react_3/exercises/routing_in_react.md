---
title: Routing in React
description: Exercises for Frontend Week III
layout: default
nav_order: 1
grand_parent: React III
parent: Exercises
permalink: /frontend/react-3/exercises/routing-in-react/
---

# Exercise: React and Routing

Open the React Router tutorial: [React Router Tutorial](https://reactrouter.com/6.28.0/start/tutorial) for reference. If you are [using version 7, use this instead](https://reactrouter.com/start/library/installation).

1. Create a new project with Vite and clean up in the usual way before you continue.
2. Install `npm install react-router-dom@6.28.0` or [version 7](https://reactrouter.com/start/library/installation)

We are going to create a book viewing app.

3. Create a navigation bar with links to:

   - Books (showing a list of books)
   - Add a book (With a form to add a new book)
   - Find a book (With an input field to write an id number to show a book)

4. Add appropriate routes with components for each link.
5. Use the `BookFacade` from [here](https://github.com/dat3startcode/router-start-code#2-create-a-new-file-bookfacadejs-and-add-the-following-content-to-the-file) for methods to use on the book list.
6. Implement the `Books` component to show a list of all the books.

   - Make each book a clickable link.

7. Add a `Details` component that can show details about a book when the book is clicked on in the list of books.

8. Implement the `AddBook` component with a form that can add another book to the list.

9. Implement the `FindBook` component with a single input field to enter a book id and a button to load book data below the input field.

10. Add a `NoMatch` component and add a route to let it handle "unknown" routes.

11. Change the book links to be `NavLinks` as in [here](https://reactrouter.com/start/library/navigating).

12. 