# Exercise: React and Routing

Open the React Router tutorial: [React Router Tutorial](https://reactrouter.com/en/6.20.1/start/tutorial) for reference.

1. Create a new project with Vite and clean up in the usual way before you continue.
2. Install `react-router-dom`.

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
11. Change the book links to be `NavLinks` as in [here](https://reactrouter.com/en/6.20.1/components/nav-link).

## Deploy the Project
1. Create a Dockerfile for the frontend.
  - Use the template as done in this [video](https://cphbusiness.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=429ca57d-e870-406c-8fae-b0ca010eb5ea)
2. Create a `.github/workflows` folder and add a `deploy.yml` file.
  - Make sure to build a docker image from github actions and push it to docker hub (as described in the video above).