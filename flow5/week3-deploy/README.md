# Deployment Front 
## Learning Objectives monday: frontend deployment and error handling
1. Understand Docker Basics:
  -  Define what Docker is and understand its role in containerization.
  -  Learn the fundamental concepts, such as images, containers, and Dockerfile.

Create a Dockerfile for a React App:
  -  Write a Dockerfile for a React application to package it into a Docker image.
  -  Understand the necessary steps for installing dependencies and building the app within the Docker container.

Set Up GitHub Actions Workflow:
  -  Configure a GitHub Actions workflow for continuous integration and deployment.
  -  Understand the syntax of GitHub Actions YAML files and their components.

Automate Docker Image Builds:
  -  Use GitHub Actions to automatically build Docker images whenever changes are pushed to the repository.
  -  Ensure that the Docker image is built consistently in a CI/CD environment.

Push Docker Images to Container Registry:
  -  Integrate GitHub Actions with a container registry (e.g., Docker Hub).
  -  Automatically push the newly built Docker image to the registry for easy retrieval.

Deploy React App with Docker Compose:
  -  Learn how to use Docker Compose to define and manage multi-container Docker applications.
  -  Create a docker-compose.yml file to orchestrate the deployment of the React app along with other services.

### Error handling
Vi have the following endpoints:
- `GET http://46.101.183.184:3005/api/v1/cars` - get all cars
- `GET http://46.101.183.184:3005/api/v1/cars/:id` - get car by id
- `POST http://46.101.183.184:3005/api/v1/cars` - post a new car

```
### POST CAR
POST http://localhost:3003/api/v1/cars
Accept: application/json
Content-Type: application/json

{
 "name": "Blue Corolla", 
  "speed": 120,
  "color": "Blue",
  "model": "Corolla",
  "year": 2022,
  "price": 30000,
  "available": true,
  "brand": "Toyota",
  "description": "A nice car"
}

### GET ALL
GET http://localhost:3003/api/v1/cars
Accept: application/json

### GET ONE
GET http://localhost:3003/api/v1/cars/656337c7e59f6df22aa458d9
Accept: application/json
```

#### Writing error messages in react apps
Common ways to handle errors in react apps:

```javascript
const [error, setError] = useState(null);

const handleCreateCar = async (car) => {
  try {
    const response = await fetch('http://some-url/api/v1/cars', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(car)
    });
    if (response.ok) {
      const data = await response.json();
      ...do something with the data
    } else {
      const data = await response.json();
      setError(data.message);
    }
  } catch (error) {
    setError(error.message);
  }
}
```
The problem in the above code is we have to repeat the same error handling code in every function that makes a request to the backend. We can solve this by creating a custom hook that handles errors for us:

```javascript
import { useState } from 'react';

export const useFetch = () => {
  const [error, setError] = useState(null);

  const handleHttpErrors = async (res) => {
    if (!res.ok) {
      return Promise.reject({ status: res.status, fullError: res.json() })
    }
    return res.json();
  }

  const makeOptions = (method, withToken, body) => {
    method = method ? method : 'GET';
    var opts = {
      method: method,
      headers: {
        ...(['PUT', 'POST'].includes(method) && { //using spread operator to conditionally add member to headers object.
          "Content-type": "application/json"
        }),
        "Accept": "application/json"
      }
    }
    if (withToken && loggedIn()) {
      opts.headers["x-access-token"] = getToken();
    }
    if (body) {
      opts.body = JSON.stringify(body);
    }
    return opts;
  }

  const fetchAny = async (url, handleData, handleError, method, withToken, body) => {
    if (properties.backendURL)
      url = properties.backendURL + url;
    const options = makeOptions(method, withToken, body);
    try {
      const res = await fetch(url, options);
      const data = await handleHttpErrors(res);
      handleData(data);
    } catch (error) {
      if (error.status) {
        error.fullError.then(e => {if(handleError) handleError(error.status+': '+e.message)});
        console.log("ERROR:",error.status);
      }
      else { console.log("Network error"); }
    }
    console.log(options);
  }

  return { error, fetchAny };
}
```

Now we can use the custom hook in our components:

```javascript
const { error, fetchAny } = useFetch();

const handleCreateCar = async (car) => {
  fetchAny('http://some-url/api/v1/cars', (data) => {
    ...do something with the data
  }, (error) => {
    setError(error);
  }, 'POST', car, false);
}
```

#### Class exercise
- See what error messages you get from posting insufficent data to the cars api
- See what error messages you get from using a wrong id when getting a car
- Clone the [starter code](https://github.com/HartmannDemoCode/errorhandlingex.git) for the Cars app
- Create an input field for a car id and a button to get a car by id. Show the car details as a list of key value pairs
- If a car with the given id does not exist, show an error message and the status code

### CORS
Cross-Origin Resource Sharing (CORS) is a mechanism that uses additional HTTP headers to tell browsers to give a web application running at one origin, access to selected resources from a different origin. A web application executes a cross-origin HTTP request when it requests a resource that has a different origin (domain, protocol, or port) from its own.

In order to make a request from a different origin, the server must add the following headers to the response:
- `Access-Control-Allow-Origin: *` - allow all origins
- `Access-Control-Allow-Methods: GET, POST, PUT, DELETE, OPTIONS` - allow all methods
- `Access-Control-Allow-Headers: Content-Type` - allow the Content-Type header

In Javalin we can do this by adding the following code to the app for all public routes:
```java
app.updateConfig(config -> {
  config.accessManager((handler, ctx, permittedRoles) -> {
    ctx.header("Access-Control-Allow-Origin", "*");
    ctx.header("Access-Control-Allow-Methods", "GET, POST, PUT, PATCH, DELETE, OPTIONS");
    ctx.header("Access-Control-Allow-Headers", "Content-Type, Authorization");
    ctx.header("Access-Control-Allow-Credentials", "true");

    if (ctx.method().equals("OPTIONS"))
      ctx.status(200).result("OK");
  });
```

#### Class exercise
- Find one of your old working projects with javalin. 
- Run the project and make a get request to one of the endpoints
- Open the developer tools in the browser and check the response headers
- Add the code above to the app and check the response headers again
- Can you see the difference?

### Deployment guide
This is a guide to deploy a react vite app to Digital Ocean using Docker and Github Actions.

#### Steps
1. Create a droplet on Digital Ocean
2. Create a new project on Github
3. Create a new repository on Github
4. Clone the repository to your local machine
5. Create a new react vite app
6. Push the app to Github
7. Create a Dockerfile with the following steps (see template below):
  - Use the official Node image as a base image
  - Copy package.json and package-lock.json to the container
  - Install dependencies
  - Copy the rest of the application code to the container
  - Build the Vite app (to get the dist folder)
  - Install `pm2` and `serve` globally to run the app
  - Expose the port that your app is running on in order to access it from outside the container
  - Command to run your app using `pm2` and `serve` on port 5000 (for production as `--spa` (single page application))
8. Create a docker-compose.yml file
9. Create a Github Actions workflow
  - Use the template below
10. Setup a Docker Hub account if you dont have one
11. Create a new access token on docker hub
12. Add 2 secrets to your Github repository
  - DOCKERHUB_USERNAME
  - DOCKERHUB_TOKEN
13. Push the changes to Github
14. Check the Github Actions workflow
15. Check the Docker Hub repository
16. Login to the Digital Ocean droplet and pull the image from Docker Hub
  - `docker pull your-docker-username/your-app-name:latest` and
  - `docker run -p 3000:3000 your-docker-username/your-app-name:latest`
17. Check the app in the browser

#### debugging
- On droplet: `docker ps -a` - list all containers on the system
- On droplet: `docker logs <container_id>` - show logs for container with id `<container_id>`
- Building the image: `docker build -t <image name> .` from the root of the project where the Dockerfile is located
- Running container in a way that it will stay open: `docker run -p 3000:3000 europe tail -f /dev/null`
- Entering the container: `docker exec -it <container_id> /bin/sh`
- Exiting the container: `exit`

#### Docker file
The docker file will be used to build the image for the app. The image will be used to run the app in a container.

```dockerfile
# Use the official Node image as a base image
FROM node:18-alpine

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code to the container
COPY . .

# Build the Vite app
RUN npm run build

# Install 'pm2' and 'serve' globally (if not already installed)
RUN npm install -g serve
# RUN npm install -g pm2

# Expose the port that your app is running on
EXPOSE 3000

# CMD ["pm2-runtime", "serve", "dist", "3000", "--spa"]
CMD ["serve", "dist", "-l", "3000"]

```

#### Github workflow file
The Github workflow file will be used to build the image and push it to Docker Hub.

```yaml
name: React Build and Deploy to Docker Hub

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - 
        name: Checkout repository
        uses: actions/checkout@v2
      - 
        name: Login to Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}
      -
        name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2
      -
        name: Build and push
        uses: docker/build-push-action@v4
        with:
          context: .
          file: ./Dockerfile
          push: true
          tags: ${{ secrets.DOCKERHUB_USERNAME }}/europemap:latest
```
#### Docker compose file
The docker compose file will be used to run the app in a container on the droplet.

```yaml
version: "3.9"

services:
  app:
    image: your-docker-username/your-app-name:latest
    ports:
      - 3000:3000
    restart: always
```
- scp docker-compose.yml to the droplet: `scp docker-compose.yml root@<ip-address>:/root/<path-to-project>`


#### Class exercise
- Find a frontend project that you have made in the past
- Deploy the project to Docker Hub using Docker and Github Actions
- Pull the image from Docker Hub to your Digital Ocean droplet and run it (using docker-compose)
- Check that it is working in the browser
