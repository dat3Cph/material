---
title: Vet API
description: Exercise II with javalin and CRUD
layout: default
nav_order: 2
grand_parent: Rest API intro
parent: Exercises
has_children: false
permalink: /rest-intro/exercises/vet-api
---

# The Veterinarian Exercise

## Exercise with Javalin and CRUD

As a computer science student, you've been engaged by a local veterinarian clinic, "Paws & Whiskers," to develop a RESTful API that will help them manage their patient appointments and information. The clinic has specific requirements for GET methods to retrieve essential data.

![Cat and dog](./images/cats_and_dogs.jpg)

**Client: Paws & Whiskers Veterinary Clinic**

**Project Requirements:**

1. **Appointment Retrieval:**
    - Create an endpoint to retrieve a list of upcoming appointments.
    - Implement an endpoint to retrieve details of a specific appointment by appointment ID.

2. **Patient (Animal) Information:**
    - Create endpoints to retrieve patient details, including medical history (e.g., allergies, medications, etc.) by patient ID.
    - Develop an endpoint to retrieve a list of all patients.

3. **Endpoint Groups:**
    - Organize routes into two endpoint groups: "Appointments" and "Patients."
    - Set up the server so that all endpoints are under the path `/api/vet/`. <https://javalin.io/documentation#configuration>
      (For example, the endpoint to retrieve a list of all patients should be `localhost:7071/api/vet/patients`.)
    - Use path params and not query params for the endpoints.

4. **Handlers:**
    - Implement separate handlers (AppointmentHandler, PatientHandler) for each GET endpoint to manage the retrieval logic.

5. **Data Structures:**
    - Utilize Java Collections to manage appointment and patient data. No need to persist data to a database.

6. **HTTP Methods:**
    - All routes should use HTTP GET methods for retrieving information.

7. **Response Format:**
    - All endpoints should return JSON data, HTTP status codes and content type.
    - Use a http file to test the endpoints.

8. **DTOs (Data Transfer Objects):**
    - Create DTOs to facilitate data transfer between the client and server. A DTO that includes some of the patient's and appointment's information is sufficient.

9. **Error Handling:**
    - Make sure to return 404 when a patient or appointment is not found.

10. **Extras but not optional:**
    - Implement Javalin's `before()` and `after()`. It could be used to log the requests and responses.
    - Implement attribute() method in your project to add a custom attribute to the context. That attribute could be used somewhere else in the project. <https://javalin.io/documentation#context>

**Business Goals:**

- Enable clinic staff to quickly access essential information about appointments and patients.
- Streamline the process of retrieving patient records and appointment details.
- Improve the efficiency of managing patient data through a RESTful API.
