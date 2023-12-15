# Deploy React frontend with React router
- Steps:
  - Create a new project with `npm create vite@latest project-name --template react`
  - Install `react-router-dom` with `npm install react-router-dom`
  - Make your application how you like it with the router.
  - When it is time to deploy: In the root of you project create 3 files:
    - 1. `Dokcerfile` with the following content:
      ```dockerfile
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
    - 2. `nginx.conf` with the following content:
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
    - 3. `.github/workflows/ci.yml` with the following content: 
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
            tags: ${{ secrets.DOCKERHUB_USERNAME }}/frontendsecure:latest
      ```
    - Create a new repository on GitHub
    - Setup 2 repository secrest on the GitHub repository:
      - `DOCKERHUB_USERNAME` with your Docker Hub username
      - `DOCKERHUB_TOKEN` with your Docker Hub token
    - Push your code to the GitHub repository.
    - Check your github actions to see if the build was successful and go to hub.docker.com to see if your image was pushed.
    - SSH into your Digital Ocean droplet and `cd` into the folder where you want to store your project.
    - If you have done a previous deployment of backend or frontend - Execute `docker compose down` to stop any running containers.
    - Find your docker-compose file (or create a new one if [not done before](./traefik.md), e.g. when you did the backend deployment) and add the following service:
      ```yml
      <NAME TO GIVE YOUR SERVICE>:
        image: "<YOUR DOCKERHUB USERNAME>/<YOUR APPLICATION DOCKER IMAGE>:latest"
        container_name: "<WHATEVER YOU WANT TO CALL YOUR CONTAINER>"
        networks:
          - backend
        labels:
          - "traefik.enable=true"
          - "traefik.http.routers.<SERVICE NAME HERE>.rule=Host(`<SERVICE NAME HERE>.cphbusinessapps.dk`)"
          - "traefik.http.routers.<SERVICE NAME HERE>.entrypoints=websecure"
          - "traefik.http.routers.<SERVICE NAME HERE>.tls.certresolver=myresolver"
          - "com.centurylinklabs.watchtower.enable=true"
      ```
    - Execute `docker compose up -d` to start the container.
    - Now go to your applied url and see if your frontend is working.

