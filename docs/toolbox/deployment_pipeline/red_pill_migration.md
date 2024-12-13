---
title: Red Pill Migration
description: Migrating docker-compose to postgres file
layout: default
nav_order: 9
grand_parent: Toolbox
parent: Deployment Pipeline
permalink: /toolbox/deployment-pipeline/red-pill-migration/
---

![Caddy Logo](./images/redblue.webp){: .mx-auto .d-block .my-5 .md .d-md-none  style="width: 25%;"}
![Caddy Logo](./images/redblue.webp){: .d-none .d-md-inline-block .ml-3 .mb-5 .float-right style="width: 25%;"}

# Migrating the Red Pill

In this exercise, you will learn how to migrate the Caddy and Javalin configurations from the `caddy_deployment` folder to the `2semDockerSetupRemote` folder. This will allow you to keep all the Docker configurations in one compose file and simplify the deployment process.

## Prerequisites at this point

1. You should have a Docker Compose file in the `2semDockerSetupRemote` folder on your Droplet with the Postgres database and the hotelAPI services.

2. You have a `caddy_deployment` folder that configures the Caddy server to serve the Javalin application over HTTPS. And you will probably also have one or more Javalin applications running in Docker containers from 2nd semester.

## The Plan

To make things easier to manage, we will begin by shutting down the Caddy and Javalin services by running:

```bash
cd ~jetty/caddy_deployment
docker compose down
```

We will then move the Caddy and Javalin configurations from the `caddy_deployment` folder to the `2semDockerSetupRemote` folder. This will allow us to keep all the Docker configurations in one compose file and simplify the deployment process.

There are three steps to this process:

1. Copy the content of the Caddyfile in the `caddy_deployment` folder to the corresponding Caddyfile in the `2semDockerSetupRemote` folder.
2. Copy the `site` folder from the `caddy_deployment` folder to the `2semDockerSetupRemote` folder. The `site` folder contains the static files for the Caddy server. This folder will be used to deploy frontend applications later in the semester.
3. Copy the Javalin applications folders from the `caddy_deployment` folder to the `2semDockerSetupRemote` folder. Like "Fog carport", "Cupcake", "Fourthingsplus" etc.
4. Finally, copy the Javalin services from the `docker-compose.yml` file in the `caddy_deployment` folder to the corresponding docker-compose.yml file in the `2semDockerSetupRemote` folder.

## The Commands

### Step 1: Copy the Caddyfile

1. Navigate to the `caddy_deployment` folder on your Droplet.
2. Print out the content of the Caddyfile:

    ```bash
    cat Caddyfile
    ```

3. Copy the content of the Caddyfile to the clipboard.
4. Navigate to the `2semDockerSetupRemote` folder.
5. Open the Caddyfile in an editor (nano):

    ```bash
    nano Caddyfile
    ```

6. Paste the content of the Caddyfile into the editor.
7. Save the file and exit the editor.

### Step 2: Copy the `site` folder

1. Navigate to the `caddy_deployment` folder on your Droplet.
2. Copy the `site` folder to the `2semDockerSetupRemote` folder:

    ```bash
    cp -r site ../2semDockerSetupRemote
    ```

### Step 3: Copy the Javalin applications folders

1. Navigate to the `caddy_deployment` folder on your Droplet.
2. Copy the Javalin applications folders to the `2semDockerSetupRemote` folder:

    ```bash
    cp -r fog ../2semDockerSetupRemote
    cp -r cupcake ../2semDockerSetupRemote
    cp -r fourthingsplus ../2semDockerSetupRemote
    ```

3. Repeat this step for all the Javalin applications you have running in Docker containers.

### Step 4: Copy the Javalin services

1. Navigate to the `caddy_deployment` folder on your Droplet.
2. Open the `docker-compose.yml` file in an editor (nano):

    ```bash
    nano docker-compose.yml
    ```

3. Copy the Javalin services from the `docker-compose.yml` file to the clipboard.
4. Navigate to the `2semDockerSetupRemote` folder.
5. Open the `docker-compose.yml` file in an editor (nano):

    ```bash
    nano docker-compose.yml
    ```

6. Paste the content of the Javalin services into the editor.
7. Save the file and exit the editor.

## The Result

You should now have all the Caddy and Javalin configurations in the `2semDockerSetupRemote` folder. You can now start the services with Docker Compose:

```bash
cd ~jetty/2semDockerSetupRemote
docker compose up -d
```

You should now be able to access the Javalin applications through the Caddy server over HTTPS.

You will also be able to deploy frontend applications in the `site` folder later in the semester.
