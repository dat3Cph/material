---
title: Frontend deployment
description: Exercises for Frontend Week IV
layout: default
nav_order: 3
grand_parent: React IV
parent: Exercises
permalink: /frontend/react-3/exercises/deployment/
---

# Exercise: Deploying frontend with Github Actions and Caddy

## Backend recap

During the backend development, we have learned how to deploy a backend application using Github Actions, Docker, Postgres, Caddy, and Watchtower. In this exercise, we will deploy a frontend application using the same tools. In fact we will use the same Caddy server to serve both the frontend and the backend.

## How to deploy a React frontend application

Our React Frontend applications are running on the client. This means that we can deploy them on any server that can serve static files. We will use Caddy to serve our frontend application. So we don't need to create a docker image for the frontend application. We can simply copy the build files to the server and let Caddy serve from the /site directory.

![Pipeline](../../../toolbox/deployment_pipeline/images/frontend_flow.svg)

## Preparation

1. Find a React frontend application that you want to deploy. Pick a simple one that doesn't require a backend API.
2. Make sure that the application is pushed to a Github repository.

## Exercise

3. [Follow this guide](../../../toolbox/deployment_pipeline/frontend.md) to deploy the frontend application using Github Actions and Caddy.

4. Find another of your React frontend applications that uses a backend api and deploy it using the same method.

## Questions to consider

1. What are the benefits of deploying the frontend and backend applications separately?

2. What does it mean that the frontend application is running on the client?

3. What are the benefits of using a static file server like Caddy for serving the frontend application? And what is a static file server?

4. Why is it necessary to use ssh to copy the files to the server?

5. How do we make sure that the subdomain is pointed to the correct application?
