---
title: Codelab - Full Pipeline
description: Deployment Exercises for the Full Pipeline
layout: default
nav_order: 2
parent: Exercises
grand_parent: Deployment
permalink: /deployment/exercises/codelab/
---

# Codelab: Full Pipeline

In this exercise, you will set up a full CI/CD pipeline for a Java project using GitHub Actions, Docker Hub, and Watchtower. You will learn how to automate the building, testing, and deployment of your application in a containerized environment and later run it on a Digital Ocean server.

## Part 1: Get an overview

First - read this overview carefully: [Full Pipeline](../../toolbox/deployment_pipeline/full_pipeline.md)

## Part 2: Setup a project to deploy

To get started you need a project to deploy. To make it easy for you, we have prepared a repo with a basic implementation of the Hotel API. You can find it [here](https://github.com/jonbertelsen/hotel_api_deployable). There is already a Dockerfile in the repo, so you can use that to build the Docker image, the pom.xml file is also ready to build the project with Maven for deployment, and there is a workflow.yml file for GitHub Actions.

1. Clone the repo to your local machine.
2. Open the project in IntelliJ.
3. Create a `config.properties` file in the `src/main/resources` folder with the following content:

```properties
    SECRET_KEY=4c9f92b04b1e85fa56e7b7b0a34f2de4f5b08cd9bb4dfe8ac4d73b4f7f6ef37b
    ISSUER=Jon Bertelsen
    TOKEN_EXPIRE_TIME=1800000
    DB_NAME=hotel
```

4. Make sure you have a `hotel` database in your Postgres database.
5. Run the project locally to make sure it works.
6. Populate the project with some data by running the populator in the `src/main/dat/config/Populate` class.
7. Delete the .git folder in the project to make it your own.
8. Push the project to your GitHub account. The GitHub Actions workflow will automatically build the project and try to push the Docker image to Docker Hub. However, you need to set up the secrets in the GitHub repository settings for this to work.

## Part 3: Setup secrets in Github

Head to Docker Hub, create an account, and create a personal access token.
Navigate to **Settings** → **Secrets and variables** → **Actions** in your GitHub repository and add these two Repository secrets.

- `DOCKERHUB_USERNAME`: Your Docker Hub username.
- `DOCKERHUB_TOKEN`: Your Docker Hub access token.

## Part 4: Run the actions again

Either push a new commit or run the workflow manually in GitHub Actions.

## Part 5: Setup Caddy and the hotelAPI container

In this step we will configure a `docker-compose.yml` file to run the hotelAPI and Caddy server on your Digital Ocean Droplet.

- Follow the [Hotel API setup](../../toolbox/deployment_pipeline/hotelAPI_setup.md) exercise to set up the hotelAPI on your Digital Ocean Droplet.
- Then follow the [Caddy Setup](../../toolbox/deployment_pipeline/caddy_setup.md) exercise to set up Caddy and a reverse proxy for the hotel api on your Digital Ocean Droplet.

## Part 6: Setup Watchtower

Now that the hotelAPI is running on your Digital Ocean Droplet, we want to set up Watchtower to automatically deploy new versions of the hotelAPI when a new Docker Image is pushed to Docker Hub. Follow the [Watchtower Setup](../../toolbox/deployment_pipeline/watchtower.md) exercise to add Watchtower to the `docker-compose.yml` file and complete the last step of the automated CI/CD pipeline.

## Part 7: Celebrate

When you have completed all the steps, you have a full CI/CD pipeline running on your Digital Ocean Droplet. You can now push new code to your GitHub repository, and it will automatically be built, tested, and deployed to your Droplet. Congratulations! 🎉
