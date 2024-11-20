---
title: React CodeLab  
description: React CodeLab Exercise  
layout: default  
nav_order: 5  
grand_parent: React II
parent: Exercises  
permalink: /frontend/react-2/exercises/codelab
---

# React CodeLab Exercise: Fetching and Displaying Trip Data  

![Codelab](./images/codelab.png){: .x .mx-auto .d-block .my-5 .md .d-md-none .w-50}
![Codelab](./images/codelab.png){: .d-none .d-md-inline-block .ml-3 .mb-5 .float-right width="200px"}

This CodeLab exercise is designed to help you practice creating React applications using Vite, fetching data from REST APIs, state management, conditional rendering, and creating dynamic UIs with interactive components. Collaboration and teamwork are emphasized, so consider pair programming where possible.

![codelab_school_exercise](../../../deepdive-1/exercises/images/pairprogramming.gif)  

## Exercise Overview  

## Instructions

### 1. Create a React Project  

1. Create a new React project using Vite:

    ```bash
    npm create vite@latest
    ```

2. Choose your project name and framework (`React`) and variant (`JavaScript`).
3. Navigate to your new project folder and install dependencies:

    ```bash
    cd [project-name]
    npm install
    npm run dev
    ```

4. Ensure your Vite development server is running successfully.

### 2. Fetch Data from the Trip API  

1. Fetch data from the provided API endpoint: [https://tripapi.cphbusinessapps.dk/api/trips](https://tripapi.cphbusinessapps.dk/api/trips).
2. Structure your `fetch` call to retrieve the list of trips when your React app loads. Use `useEffect` and `useState` hooks for managing state and lifecycle.
3. Verify the response data structure:

    ```json
    [
      {
        "id": 11,
        "starttime": "2025-01-25T12:34:06.865979",
        "endtime": "2025-01-28T12:34:06.865979",
        "longitude": 14.94,
        "latitude": 58.75,
        "name": "Test",
        "price": 10.0,
        "category": "CITY",
        "guide": {
          "id": 1,
          "firstname": "Andreas",
          "lastname": "Turkey",
          "email": "andreas@mail.com",
          "phone": "33293922",
          "yearsOfExperience": 10,
          "trips": ["Beach Holiday", "City Tour", "Snow boarding", "Living under a bridge"]
        }
      },
      ...
    ]
    ```

### 3. Display All Trips  

1. Render all trips on the left side of the screen as a list (or a table or as card layout or whatever you fancy).
2. Display key information for each trip, such as:
    - Trip name
    - Start and end dates
    - Price
    - Duration  

### 4. Category Filter  

1. Add a dropdown (`select` element) above the trip list that allows users to filter trips based on their `category`. Get the categories from here: [https://packingapi.cphbusinessapps.dk/packinglist/](https://packingapi.cphbusinessapps.dk/packinglist/)
2. When a category is selected, only trips belonging to that category should be displayed.

### 5. Trip Details View  

1. When a trip is clicked, display a `Trip Details` view on the right side of the screen. Details about a trip can be found by id like this: [https://tripapi.cphbusinessapps.dk/api/trips/11](https://tripapi.cphbusinessapps.dk/api/trips/2).
2. This view should display detailed trip information, including:
    - Trip name
    - Start and end dates
    - Price
    - Category
    - Guide details (name, email, phone, years of experience)

### 6. Packing Items Table  

1. If the selected trip includes packing items, render them in a table within the `Trip Details` view.
2. Display the following columns:
    - Item name
    - Weight in grams
    - Quantity
    - Description
    - Category
    - Available buying options (shop name, price)

### 7. Calculations  

1. Below the table, calculate and display:
    - The total summed weight of all packing items for the trip.
    - The total cheapest price for each packing item, if applicable.

---

Good luck and have fun! Remember to read instructions carefully, collaborate with your teammates, and ask for help if needed.
