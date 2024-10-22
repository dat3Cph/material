---
title: Postgres Setup
description: Deployment Exercises Postgres Setup
layout: default
nav_order: 3
grand_parent: Toolbox
parent: Deployment Pipeline
permalink: /toolbox/deployment-pipeline/postgres-setup/
---

![Postgres Logo](./images/postgres_logo.webp){: .mx-auto .d-block .my-5 .md .d-md-none  style="width: 25%;"}
![Postgres Logo](./images/postgres_logo.webp){: .d-none .d-md-inline-block .ml-3 .mb-5 .float-right style="width: 25%;"}

# Potsgres Setup

We use [Postgres](https://www.postgresql.org/) as our relational database. In this exercise, you will learn how to set up Postgres on your Digital Ocean Droplet. Later we will connect it to the hotelAPI Javalin application.

## Introduction - flashback to 2nd semester

On 2nd semester we installed Postgres on our Digital Ocean Droplet. We used a `docker-compose.yml` file to set up the Postgres database. The file looked roughly like this:

```yaml
# db: Postgresql data base server som kører på port 5432

version: '3'

services:

  db:
    image: postgres:16.2
    container_name: db
    restart: unless-stopped
    networks:
      - backend
    environment:
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
    volumes:
      - ./data:/var/lib/postgresql/data/
      - ./db/init.sql:/docker-entrypoint-initdb.d/init.sql
    ports:
      - "5432:5432"

networks:
  backend:
      name: backend
```

If you went through that setup on 2nd semester, as most did, you will have this compose file already on your Droplet. The docker-compose file is located in the `~jetty/2semDockerSetupRemote` folder. If you don't have it, then follow the [2nd semester tutorial](https://github.com/dat2Cph/2semDockerSetupRemote) and get on track.

## Step 1: Update the Docker Compose File

We don't want to loose our data, so we will keep the `db` service running on the `backend` network. This is the network that the `hotelAPI` service will connect to later. For security reasons, we will add environment variables for the Postgres user and password and store them in a an external `.env` file:

1. Navigate to the `~jetty/2semDockerSetupRemote` folder on your Droplet.
2. Open the `docker-compose.yml` file in an editor (nano).
3. Update the file with the following content:

   ```yaml
   version: '3'

   services:

     db:
       image: postgres:16.2
       container_name: db
       restart: unless-stopped
       networks:
         - backend
       environment:
         POSTGRES_USER: ${POSTGRES_USER}
         POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
       volumes:
         - ./data:/var/lib/postgresql/data/
         - ./db/init.sql:/docker-entrypoint-initdb.d/init.sql
       ports:
         - "5432:5432"
       healthcheck:
         test: ["CMD-SHELL", "pg_isready -U postgres"]
         interval: 30s
         timeout: 10s
         retries: 5
         start_period: 10s

   networks:
     backend:
       name: backend
   ```

4. It's close to the 2nd semester version, but we have removed the `mem_limit` and `mem_reservation` settings. We have also added `${POSTGRES_USER}` and `${POSTGRES_PASSWORD}` as environment variables. These will be set in the `.env` file later. We have also added a healthcheck to the service, that we will use later.

5. Save the file and exit the editor.

## Step 2: Create the `.env` file

1. Create a `.env` file in the `~jetty/2semDockerSetupRemote` folder:
  
    ```bash
    nano .env
    ```

2. Add the following content to the file:

    ```properties
    POSTGRES_USER=postgres
    POSTGRES_PASSWORD=<dit_sikre_password>
    ```

    Replace `<dit_sikre_password>` with a secure password.

3. Save the file and exit the editor.

## Step 3: Start the Postgres Service

1. Start the Postgres service with Docker Compose:

    ```bash
    docker-compose up -d
    ```

2. Check that the service is running:

    ```bash
    docker ps
    ```

    You should see the `db` service running.

3. Check the logs from the service:

    ```bash
    docker logs db
    ```

## Next step

Now that the Postgres service is running, we can connect the `hotelAPI` service to it. Follow the [Hotel API](./hotelAPI_setup.md) exercise to set up the hotelAPI Javalin web application on your Digital Ocean Droplet.
