---
title: HotelAPI Setup
description: Deployment Exercises HotelAPI Setup
layout: default
nav_order: 4
grand_parent: Toolbox
parent: Deployment Pipeline
permalink: /toolbox/deployment-pipeline/hotelapi-setup/
---

![Postgres Logo](./images/javalin_logo.png){: .mx-auto .d-block .my-5 .md .d-md-none  style="width: 25%;"}
![Postgres Logo](./images/javalin_logo.png){: .d-none .d-md-inline-block .ml-3 .mb-5 .float-right style="width: 25%;"}

# Hotel API and Javalin Setup

In this exercise, you will learn how to set up the HotelAPI Javalin application on your Digital Ocean Droplet. We will pull the image from Docker Hub and launch the Jetty webserver in a Docker Container. We will also make sure that it can connect to the Postgres database that we set up in the previous exercise.

## Introduction - flashback to 2nd semester

On 2nd semester we had two options for deploying our web applications. We could either use the "[blue](https://dat2cph.github.io/content/linux/deployment/blue-pill/)" or the "[red](https://dat2cph.github.io/content/linux/deployment/red-pill/)" pill. The blue pill was the easy way out. We secure copied the fat jar-file to the droplet and ran it with `java -jar`. So we only had Postgres running in a Docker Container. The rest were running on the host machine. The websites were exposed on IP addresses and a port number.

The red pill was the harder way. But also the more sophisticated. We created a Dockerfile and a docker-compose file and ran the application in a Docker container. We also set up a reverse proxy with Caddy to serve the application over HTTPS and a domain name. If you went the red pill way, you should have a `docker-compose.yml` file on your Droplet in the `~jetty/caddy_deployment` folder.

![RedBlue](./images/redblue.webp)

So to sum it up. If you went the blue pill way, you should have a Postgres database running in a Docker Container. If you went the red pill way, you should have a Postgres database and Caddy, and Javalin applications running in Docker Containers. So you would be one of these personas:

- **Blue:** Only Postgres. The docker-compose file is located in the `~jetty/2semDockerSetupRemote` folder.
- **Red:** Postgres, Caddy, and Javalin. Postgres is still configured in the docker-compose.yml file in the `~jetty/2semDockerSetupRemote` folder. Caddy and Javalin are configured in the docker-compose.yml file in the `~jetty/caddy_deployment` folder.

So who are you. Blue or Red?

- **Blue:** Then you will keep all Docker configurations in the docker-compose.yml in the `~jetty/2semDockerSetupRemote` folder. Later we can rename the folder to `~jetty/deployment` to keep things organized - and distance ourselves from the past.

- **Red:** Then you will keep the Postgres configuration in the docker-compose.yml in the `~jetty/2semDockerSetupRemote` folder. We don't want to mess with the Postgres data. To keep things easier to manage, we will migrate (move) the Caddy and Javalin configurations to the `~jetty/2semDockerSetupRemote` folder. We will also rename that folder to `~jetty/deployment` to keep things organized. This takes a small effort to merge the two docker-compose files into one. But it is worth it.

## Step 1 (everyone): Add the hotelAPI Service to the Docker Compose File

1. Navigate to the `~jetty/2semDockerSetupRemote` folder on your Droplet.
2. Open the `docker-compose.yml` file in an editor (nano).
3. Add this services to the file below the Postgres service. Remember to rename the image to you own name instead of `jonbertelsen/hotel_api:latest`:

```yml
  hotelAPI:
    image: jonbertelsen/hotel_api:latest
    container_name: hotelAPI
    ports:
      - "7070:7070"
    environment:
      - DEPLOYED=${DEPLOYED}
      - DB_NAME=${DB_NAME}
      - DB_USERNAME=${DB_USERNAME}
      - DB_PASSWORD=${DB_PASSWORD}
      - CONNECTION_STR=${CONNECTION_STR}
      - SECRET_KEY=${SECRET_KEY}
      - ISSUER=${ISSUER}
      - TOKEN_EXPIRE_TIME=${TOKEN_EXPIRE_TIME}
    networks:
      - backend
      - frontend
    volumes:
      - ./logs:/logs
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:7070/api/auth/healthcheck"]
      interval: 30s
      timeout: 5s
      retries: 5
      start_period: 10s

volumes:
  logs:

networks:
  backend:
    name: backend
  frontend:
    name: frontend
```

Notice the healthcheck. It will check if the application is running by calling the `/api/auth/healthcheck` endpoint every 30 seconds. If the application does not respond within 5 seconds, it will retry 5 times with a 10 second start period. This is a good way to make sure that the application is running and healthy. You will need to implement a healthcheck endpoint in your application. We have already done that for you in the HotelAPI. Look in the [`SecurityController`](https://github.com/jonbertelsen/hotel_api_deployable/blob/b7c397b56559ad51ec6f070aa6ecd4fb49892099/src/main/java/dat/security/controllers/SecurityController.java#L194-L197) class, and also, notice the endpoint added in the [`SecurityRoutes`](https://github.com/jonbertelsen/hotel_api_deployable/blob/b7c397b56559ad51ec6f070aa6ecd4fb49892099/src/main/java/dat/security/routes/SecurityRoutes.java#L22).

4. Add the following environment variables to the `.env` file:

   ```properties
   DEPLOYED=true
   DB_NAME=hotel
   DB_USERNAME=postgres
   DB_PASSWORD=<your secure password>
   CONNECTION_STR=jdbc:postgresql://db:5432/
   SECRET_KEY=4c9f92b04b1e85fa56e7b7b0a34f2de4f5b08cd9bb4dfe8ac4d73b4f7f6ef37b
   ISSUER=Bilbo Baggins
   TOKEN_EXPIRE_TIME=18000
   ```

5. Save the file and exit the editor.

## Step 2 Start the Postgres and hotelAPI Services

1. Do this:

    ```bash
    docker compose down
    docker compose up
    ```

    Notice that we left out  the `-d` flag. This is because we want to see the output from the services. If there are any errors, we want to see them. Press Ctrl + C to stop the services.

2. Check that the services are running:

    Log into your droplet with another terminal window and run:

    ```bash
    docker ps
    ```

    You should see the `db` and the `hotelAPI` service running. The `hotelAPI` service might take a little while to get started, since we need to pull the image from Docker Hub. Also, remember to check the logs from the services if you see any errors. One typical error is that the `hotel` database does not exist. You can create it with the following command:

    ```bash
    docker exec -it db psql -U postgres -c "CREATE DATABASE hotel;"
    ```

    Or do it with pgAdmin from your local machine.

## Next step

The next step is to setup [Caddy Server](./caddy_setup.md) to serve the HotelAPI over HTTPS.
