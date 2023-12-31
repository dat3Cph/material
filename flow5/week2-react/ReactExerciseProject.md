# CRUD React Project

## Assignment

Together with your group, create a small CRUD application with help of React and the 
[JSON Server](https://www.npmjs.com/package/json-server). The application should be able to create, read, update 
and delete data from the server. Try to use all the skills you have learned so far in the course.

Here are some ideas for inspiration:

- A Budget App
- A Todo App
- A Recipe App
- A Workout App
- A Card Game App

<img src="./images/react-crud-api.png" width="800" height="400">

## Requirements

The project has to contain the following:

- A `README.md` file with a description of the project.
- A `package.json` file with all the dependencies.
- A `http` file with all the CRUD method calls.
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

Do a short video presentation of your project where you show your user interface, explain how it works and guide us 
through your code. Both your link to the video and code should be emailed to your group-teacher.
