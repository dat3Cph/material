---
title: Codelab 
description: Exercises for Frontend Week IV
layout: default
nav_order: 2
grand_parent: React IV
parent: Exercises
permalink: /frontend/react-4/exercises/codelab/
---

# Practicing styling with styled-components and error handling

![Codelab](./images/codelab.png){: .x .mx-auto .d-block .my-5 .md .d-md-none .w-50}
![Codelab](./images/codelab.png){: .d-none .d-md-inline-block .ml-3 .mb-5 .float-right width="200px"}

This CodeLab exercise is designed to help you practice the concepts you have learned in the Frontend Week IV module. 
You will be working with a partner to complete the tasks in this exercise. 

<img src="./images/Truck.png" width="800"/>

![Truck](./images/Truck.png)


## The assignment
### Basic setup with pages
1. Create a new React application using `npm create vite@latest` and choose the React template.
2. Install the following dependencies:
   - `styled-components`
   - `react-router-dom@6.28.0`
3. Create 2 new folders called `components` and `pages` in the `src` folder.
4. In package.json add a new script called `json-server` that runs `json-server --watch db.json --port 3000`.
5. Get the `db.json` file from [here](https://gist.githubusercontent.com/Thomas-Hartmann/94381753fbe703ae0da350eaa63cd31d/raw/7560510b42bc8c0cfdf6b4a800b2080269f81601/db.json) and place it in the root of your project.
6. Create the following pages:
   - `Home` page that Shows an image of a truck and explains what the app is about (Administering a trucking company).
   - `Trucks` a page that displays a list of trucks. Each truck should have a name and a description with weight and capacity.
   - `Drivers` a page that displays a list of drivers. Each driver should have a name, and a description (with driver details)
   - `RegisterDriver` a page that allows you to register a new driver. Something like [this](https://gist.githubusercontent.com/Thomas-Hartmann/94381753fbe703ae0da350eaa63cd31d/raw/c55e1beb132b7725cd1b379ba3fc9590b31c5ba2/form)

### Components

7. Create a `Header` component that displays a navigation bar with links to the different pages.
8. Create a `Footer` component that displays the text "© 2024 Trucking Company".
9. Create a `TruckCard` component that displays a truck with a name, description, and picture. The card should have its own route and be displayed when you click on a truck.
10. Create a `DriverCard` component that displays a driver with a name, description, and picture. The card should have its own route and be displayed when you click on a driver.

### Styling and error handling

11. Style everything using `styled-components`. Add a theme object with colors and fonts and use it in your components with the `ThemeProvider`.
12. Add error handling to the `TruckCard` and `DriverCard` components. If the truck or driver does not exist, display an error message in an error banner in the main Outlet component.
13. Add a 404 page that displays a message saying "Page not found" and a link to the home page.
14. Add a 500 error page that displays a message saying "Server error" when a component can not render due to an error.
15. Add try-catch blocks to the fetch requests in the `TruckCard` and `DriverCard` components to catch errors and display the error message in the error banner.

### Extra

16. Implement buttons to delete or edit trucks and drivers. The edit button should take you to a form where you can edit the truck or driver.
