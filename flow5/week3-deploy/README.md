# Deployment Front and Back
## Learning Objectives monday: frontend deployment
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
FROM node:14-alpine

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

