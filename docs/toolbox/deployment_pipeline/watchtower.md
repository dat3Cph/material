---
title: Watchtower Setup
description: Setting up Watchtower for Continuous Deployment
layout: default
nav_order: 7
grand_parent: Toolbox
parent: Deployment Pipeline
permalink: /toolbox/deployment-pipeline/watchtower-setup/
---

# Watchtower Setup

We use [Watchtower](https://containrrr.dev/watchtower/) to handle deployment of your Docker Image to your Digital Ocean Droplet. In this exercise, you will learn how to set up Watchtower to automatically deploy your Javalin application when a new Docker Image is pushed to Docker Hub.

![Watchtower Setup](./images/watchtower.png){: .mx-auto .d-block .my-5 .md .d-md-none style="width: 50%;" }
![Watchtower Setup](./images/watchtower.png){: .d-none .d-md-inline-block .ml-3 .mb-5 .float-right style="width: 50%;"}

## Introduction

Watchtower is a tool used in Docker environments to automate the process of updating and redeploying running containers when new versions of their images become available. It monitors Docker containers and checks for updates to their images in Docker registries (like Docker Hub). When a new image is detected, Watchtower pulls the updated image, stops the running container, and restarts it with the new image, maintaining the same configuration as the original container.

## Prerequisites

1. You will need to have a Docker Image on Docker Hub with your Javalin application. If not, then follow the [Github Actions and Docker Hub tutorial](./actions_dockerhub.md) tutorial first.

## Step 1: Getting oriented

1. **SSH into your Droplet**:
   - Open a terminal and SSH into your Digital Ocean Droplet.

2. **Install Watchtower with docker-compose**:
You should already have a `docker-compose.yml` file on your Droplet from 2nd semester. It is located in the `~jetty/2semDockerSetupRemote` folder.

3. Jump into the `2semDockerSetupRemote` folder:

```bash
cd ~jetty/2semDockerSetupRemote
```

## Step 2: Add Watchtower to the `docker-compose.yml` file

- Open the `docker-compose.yml` file with `nano`:

     ```bash
     nano docker-compose.yml
     ```

To configure Watchtower to run in a container using Docker Compose and to pull a specific image from Docker Hub every 5 minutes, you can set up a Docker Compose file with Watchtower configured for the desired container. Here’s a step-by-step guide:

### Step 1: Create Your Docker Compose File

In your Docker Compose file, you’ll define the Watchtower service with the necessary options. Below is an example configuration where Watchtower is set to monitor a container running your specific image (e.g., `your-dockerhub-username/hotelAPI`) and checks for updates every 5 minutes.

```yaml

services:

  watchtower:
    image: containrrr/watchtower:latest
    container_name: watchtower
    restart: unless-stopped
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      - WATCHTOWER_CLEANUP=true
      - WATCHTOWER_POLL_INTERVAL=300  # Check for updates every 300 seconds (5 minutes)
    networks:
      - frontend
    command: hotelAPI 
    depends_on:
      hotelAPI:
        condition: service_healthy
```

#### Explanation

- **watchtower**: This container runs Watchtower. The following options are specified:
  - **Volumes**: Watchtower requires access to the Docker socket (`/var/run/docker.sock`) to interact with Docker.
  - **Environment Variables**:
    - `WATCHTOWER_POLL_INTERVAL=300`: This sets Watchtower to check for updates every 300 seconds (5 minutes).
    - `WATCHTOWER_CLEANUP=true`: Watchtower removes old images after they are updated to free up space.
  - **Command**: Specifying `hotelAPI` tells Watchtower to monitor only the `hotelAPI` container. If you omit this, Watchtower will monitor all containers by default.

### Step 2: Run the Configuration

To start the Watchtower service with this configuration, run the following commands:

```bash
    docker-compose up -d
```

This will start both the `hotelAPI` container and the Watchtower service. Watchtower will check for updates to the `hotelAPI` image on Docker Hub every 5 minutes and automatically update the container if a new version is available.

- Check that the Watchtower container is running:

  ```bash
    docker ps
  ```

- You should see a container named `watchtower` running.

## Step 3: Test Watchtower

- Test Watchtower by pushing a new version of your Docker Image to Docker Hub.
- Watchtower should detect the new image and redeploy your Javalin application within 5 minutes.

## Step 4: Troubleshooting

- If Watchtower does not detect the new image, then check the logs of the Watchtower container:

     ```bash
     docker logs watchtower
     ```

- The logs will show you what is going wrong. In the testing phase, you might also want to set the `WATCHTOWER_POLL_INTERVAL` to a lower value to test if Watchtower is working as expected. For example, set it to 60 seconds.

## Step 5: Testing the endpoint

Depending on your firewall settings, you might need to open the port `7070` on your Droplet. You can do this in the Digital Ocean dashboard. Then you should be able to hit the endpoint of your Javalin application by navigating to `http://your-droplet-ip:7070` and add the necessary path to your API. However, the sub domain should also work on https, since Caddy is running. It should be available at `https://hotel.mydomain.com`.

## Next Step: 2nd semester migration - or done

Now that you have set up Watchtower to automatically deploy your Javalin application, you have completed you setup. In case you need to move your settings from the "Red Pill" setup from 2nd semester, then follow the [Red Pill Migration](./red-pill-migration.md) tutorial. Otherwise, you have made it to the end of the deployment pipeline. Congratulations!

## Bonus Step: Rename the deployment folder

This one is easy. Stop your containers and then rename the `2semDockerSetupRemote` folder to `deployment`:

```bash
cd ~jetty/2semDockerSetupRemote
docker-compose down
cd ~jetty
mv 2semDockerSetupRemote deployment
```

## Source files

You can check the source files for this exercise:

- [Docker Compose File](./docs/docker-compose.yml)
- [.env file](./docs/env.txt)
