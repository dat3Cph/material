# CRUD React Project

## Assignment

Together with your group, create a small CRUD application using React and the 
[JSON Server](https://www.npmjs.com/package/json-server). The application should be able to create, read, update 
and delete data from the server. The data should be persisted in the server. Think about what kind of data you 
want to store in the server. It could be a list of books, movies, cars, etc.


Here are some ideas for inspiration:

- A Budget App
- A Todo App
- A Recipe App
- A Workout App
- A Card Game App

## Requirements

The project has to contain the following:

- A `README.md` file with a description of the project.
- A `package.json` file with all the dependencies.
- Use React hooks like `useState`, `useEffect` etc.
- Use the `fetch` API to communicate with the server.
- Use the `json-server` to persist data.
- All four CRUD operations should be implemented.
- All CRUD functions should be separated into a separate file.

## Tips

- Start by creating a new React project using Vite.
- Create a new folder called `api` and add a file called `api.js` inside it. This file should contain all the CRUD functions.
- Create a new folder called `components` and add all your components inside it.

How to implement the json-server:

- Install the json-server using `npm install json-server`.
- Create a new file called `db.json` in the root of your project.
- Add some data to the `db.json` file.
- In the `package.json` file, add a new script called `server` and set the value to `json-server --watch db.json --port 3001`.

## Handing in the assignment

The assignment should be handed in as a link to a GitHub repository.