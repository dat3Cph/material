## Deployment Part 2

- Deployment of the frontend part
- Using GitHub actions, DockerHub and Nginx

Part 1: 

- add a Dockerfile to the root of the frontend project. Add the code below to the Dockerfile.

```Dockerfile
# First stage: build the react app
# FROM tiangolo/node-frontend:10 as build-stage
FROM node:18 as build-stage
WORKDIR /app
COPY package*.json /app/
RUN npm install
COPY . .
RUN npm run build

# Second stage: use the build output from the first stage with nginx
FROM nginx:1.25
COPY --from=build-stage /app/dist/ /usr/share/nginx/html

# Copy the default nginx.conf to get the try-files directive to work with react router
COPY ./nginx.conf /etc/nginx/conf.d/default.conf
```

- Create a file called nginx.conf in the root of the frontend project and add the following code to it.

```nginx
server {
    listen       80;
    listen  [::]:80;
    server_name  localhost;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
        try_files $uri $uri/ /index.html;
    }
}
```

- Add a .github/workflows folder to the root of the frontend project and create a file called deploy.yml in the .github/workflows folder. Add the following code to the deploy.yml file.

```yml
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
          tags: ${{ secrets.DOCKERHUB_USERNAME }}/<your_frontend_api_name>:latest
```

Part 2:

- Push the changes to the main branch of the frontend repository. This will trigger the GitHub action to build the 
Docker image and push it to DockerHub.
- On your DigitalOcean droplet, update your already docker-compose.yml file to include the frontend service. Add the 
following code to the docker-compose.yml file. Remember to replace the placeholders with your own values. Also stop all 
running containers before adding the frontend service.

```yml
frontend:
    image: <your_docker_hub_username>/<your_frontend_api_name>:latest
    container_name: frontend
    ports:
      - "<your_frontend_port>:<your_frontend_port>"
    restart: unless-stopped
```

Part 3:

Go to the browser and enter the IP address of your DigitalOcean droplet followed by the frontend port. You should see
the frontend of your project.