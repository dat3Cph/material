---
title: Trip with Security
description: Exercises for Frontend Week III
layout: default
nav_order: 4
grand_parent: React III
parent: Exercises
permalink: /frontend/react-3/exercises/tripapp_security/
---

# Friday exercise - Trip App with Security

## Continue the tripapp from frontend react II - codelab

- API to use:
  - [https://tripapi.cphbusinessapps.dk/api/trips](https://tripapi.cphbusinessapps.dk/api/trips) (ANYONE)
  - [https://tripapi.cphbusinessapps.dk/api/guides](https://tripapi.cphbusinessapps.dk/api/guides) (ADMIN)
  - [https://tripapi.cphbusinessapps.dk/api/trips/3](https://tripapi.cphbusinessapps.dk/api/trips/3) (USER)
  - [https://tripapi.cphbusinessapps.dk/api/auth/login](https://tripapi.cphbusinessapps.dk/api/auth/login) (ANYONE)

- users in the system:
  - user {"username": "user", "password": "user123"} - role: USER
  - admin {"username": "admin", "password": "admin123"} - role: ADMIN

1. Use your solution to the codelab exercise in the second react week.

2. Install react router: `npm install react-router-dom@6.28.0`

3. Setup the router in `main.jsx` and setup a parent route with the App component as element surrounding all the other routes. Documentation for react router can be found [here](../../../toolbox/react/routing.md)

4. Setup 3 sub routes under the parent route:

    1. Trips (to show a list of all available trips)
    2. Guides (to show a list of all available guides - protected with the `Admin` role)
    3. Trip (to show a single trip with details about guide and packing list (if available) - protected with `User` role)

5. Setup a Header component used inside App (allways visible) with 2 links to `trips`, `guides` (and `trip/:id` will be shown when clicking a trip)

6. In the header component create a login form so that when logged in the form is replaced with the username of the logged in user

- use the apiFacade class from yesterday to do the login to the server.

7. Create the Trips Component to show a list of all the trips (use the code you have from the codelab)

8. Create the Guides Component to show a list of all guides

- Use the apiFacade to send the token with the `Authorization` header when making the request

9. Create the Trip Details Component with the `User` role
