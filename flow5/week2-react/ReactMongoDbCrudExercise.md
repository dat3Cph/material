### Fetch data from a REST-endpoint (Mongo-DB Docker Server)

In this exercise, we will fetch data from a REST-endpoint using the `fetch` function. The REST-endpoint is a Docker container running a Mongo-DB server.
The data is stored in a collection called `students` and the REST-endpoint is running on port 3000.

- LinkClone the following repository: https://github.com/dat3startcode/mockserver/tree/main/mockserver_crud_exercises
- Create a new folder called CrudExercises and create a new javascript file called `index.js` in it.
- The endpoint documentation is here: https://app.swaggerhub.com/apis-docs/tysker/student/1.0.0
- Create a function called `getAllStudents` which fetches all students from the endpoint and returns the JSON data.
- Create a function called `getStudentById` which fetches a student with a given id from the endpoint and returns the JSON data.
- Create a function called `addStudent` which adds a student to the endpoint and returns the JSON data.
- Create a function called `deleteStudent` which deletes a student with a given id from the endpoint and returns the JSON data.
- Create a function called `updateStudent` which updates a student with a given id from the endpoint and returns the JSON data.


# Not finished yet