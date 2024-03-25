# SchoolHack Workshop API

## Overview

The SchoolHack Workshop API is a RESTful API that allows you to create, read, update, and delete events.
The idea is to provide a way to manage the events/workshops that are going to be held in the SchoolHack platform.
The platform could be a website, mobile app, or any other platform that needs to manage those events.
On the platform, students can see the events/workshops that are going to be held and register for them.

Your job is to implement the API that will allow the platform to manage the events/workshops. NO FRONTEND IS REQUIRED!
The platform will be responsible for consuming the API and displaying the events/workshops to the students.

**The platform needs to have the following properties:**

- **Title**: The title of the event/workshop.
- **Description**: A brief description of the event/workshop.
- **Date**: The date when the event/workshop will be held.
- **Time**: The time when the event/workshop will start.
- **Duration**: The duration of the event/workshop in hours.
- **Capacity**: The maximum number of students that can register for the event/workshop.
- **Location**: The location where the event/workshop will be held.
- **Instructor**: The name of the instructor that will be teaching the event/workshop.
- **Price**: The price of the event/workshop.
- **Category**: The category of the event/workshop. It could be a workshop, a talk, a course, etc.
- **Image**: The image of the event/workshop.
- **Status**: The status of the event/workshop. It could be active, inactive, or canceled.
- **Created at**: The date when the event/workshop was created. (This field should be automatically filled by the API)
- **Updated at**: The date when the event/workshop was last updated. (This field should be automatically filled by the
  API)
- **Deleted at**: The date when the event/workshop was deleted. (This field should be automatically filled by the API)
- **Name**: The name of the user.
- **Email**: The email of the user.
- **Phone**: The phone number of the user.
- **Role**: The role of the user. It could be a student, an instructor, or an admin.
- **Password**: The password of the user.

1. You first need to create the database schema (EER) that will store the events/workshops and the users.
2. After that you need to create all Java entities and the DAOs that will allow you to interact with the database.
3. Then you need to implement the API that will allow the platform to manage the events/workshops and the users.

Remember only to use a DTO when sending data to the frontend. Authentication and authorization should be implemented as shown in the previous project.
For all Date and time properties, do not use a string. Use the `LocalDateTime` class from the `java.time` package.

The above properties are guidelines, you can add and change the properties as you see fit.

Think about the relationships between the entities and how you can implement them in the database. For example, an event
can have multiple registrations, and a user can have multiple registrations. How can you implement this relationship in
the database?

Think about the security of the API. How can you make sure that only users with the correct role can access the
endpoints?
How can you make sure that the passwords are secure and hashed before being stored in the database?

**Remember to test your endpoints and DAO methods to make sure they are working correctly.**

***

## API Endpoints

The API should have the following endpoints:

- **Events**
    - `GET /events`: Get all events.
    - `GET /events/:id`: Get a single event.
    - `POST /events`: Create a new event.
    - `PUT /events/:id`: Update an event.
    - `DELETE /events/:id`: Delete an event.

- **Users**
    - `GET /users`: Get all users.
    - `GET /users/:id`: Get a single user.
    - `POST /users`: Create a new user.
    - `PUT /users/:id`: Update a user.
    - `DELETE /users/:id`: Delete a user.

- **Registrations**
    - `GET /registrations/:id`: Get all registrations for an event.
    - `GET /registration/:id`: Get a single registration.
    - `POST /registrations/:id`: Register a user for an event.
    - `DELETE /registrations/:id`: Cancel a user's registration for an event.

- **Authentication**
    - `POST /login`: Login a user.
    - `POST /logout`: Logout a user.
    - `POST /register`: Register a new user.
    - `POST /reset-password`: Reset the user's password.

## User Stories

The following user stories should be implemented:

**Student Stories**

- As a user, I want to see all the events/workshops that are going to be held.
- As a user, I want to see the details of a specific event/workshop.
- As a user, I want to register for an event/workshop.
- As a user, I want to cancel my registration for an event/workshop.
- As a user, I want to be able to reset my password. ( How can you make sure that the user is the one who is resetting
  the password? )

**Instructor Stories**

- As an instructor, I want to create a new event/workshop.
- As an instructor, I want to update an event/workshop.
- As an instructor, I want to cancel an event/workshop.
- As an instructor, I want to see all the events/workshops that I am teaching.
- As an instructor, I want to see all the registrations for an event/workshop.

**Admin Stories**

- As an admin, I want to see all the users.
- As an admin, I want to see all the events/workshops.

**General Stories**

- Implement a way to filter events by category and status.

Remember that the API should be secure and only allow users with the correct role to access the endpoints. Also, the
passwords should be hashed before being stored in the database.

**Documentation (README.md)**:

- Add the finished EER diagram to the README.md file.
- The API should have proper documentation that explains how to use the API and what each endpoint does.


**Below is an example of how the API documentation should look like:**

| HTTP method | REST Resource      |                                   | Comment                     |
|-------------|--------------------|-----------------------------------|-----------------------------|
| GET         | `/api/test`        | `response:` [{response body}]     | Retrieve all tests          |
| GET         | `/api/test/{id}`   | `response:` {response body}       | Retrieve a test by its ID   |
| GET         | `/api/test1/test2` | `response:` [{response body}]     | Retrieve test by some value | 
| POST        | `/api/test`        | `request payload:` {request body} | Add a new test.             |
| PUT         | `/api/test/{id}`   | `request payload:` {request body} | Update a test ID            |






