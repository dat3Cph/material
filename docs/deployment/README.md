---
title: Deployment
description: Continuous Deployment and Continuous Integration
layout: default
nav_order: 8
has_children: true
permalink: /deployment/
---

# Deployment

Topics covered in this week are:

Deploying Javalin applications on Docker in the Cloud using:

- Docker
- Continuous Integration & Deployment
- GitHub Actions
- Docker Hub
- Watchtower
- Ubuntu VM on Digital Ocean
- Caddy Server
- Domains, SSL Certificates, and HTTPS

[Learning objectives for the week](./learningobjectives.md)

## Monday

Online review on the Friday assignment:

- What did you solve?
- Show your code an run it in IntelliJ
- Think about what you could have done differently
- What did you learn?

For the rest of the day: Prepare for the week. Watch the videos and read the articles.

## Tuesday (class) - Docker, Docker Hub, and GitHub Actions

### Prepare for the class

Watch this video:

- [CI / CD in 5 minutes](https://www.youtube.com/watch?v=42UP1fxi2SY)
- [Docker file (from 49:09 - 58:30)](https://youtu.be/pg19Z8LL06w?si=Q0ZWp6fojjCvHw5k&t=2950)

Skim through these articles:

- [Continuous integration vs delivery vs deployment](https://www.atlassian.com/continuous-delivery/principles/continuous-integration-vs-delivery-vs-deployment)

- [Dockerfile reference](https://docs.docker.com/reference/dockerfile/)

- [Docker Compose reference](https://docs.docker.com/compose/intro/features-uses/)

- [Github Actions (first page)](https://docs.github.com/en/actions/about-github-actions/understanding-github-actions)

### In-class exercises

- [Github Actions and Docker Hub Tutorial](../toolbox/deployment_pipeline/actions_dockerhub.md)

## Wednesday (CodeLab) - Docker, Digital Ocean, Watch Tower, and Caddy Server

Today we will finish deploying a web api on a Digital Ocean Droplet. We will use Docker, Watch Tower, and Caddy Server to deploy the web api.

The goal is to have a running web api on a Digital Ocean Droplet with a domain name and SSL certificate. The web api should be accessible through the domain name and should be updated automatically when a new version is pushed to the Docker Hub.

### Prepare for the CodeLab

1. It would be good if you have a **domain name ready**. It takes a little while to get a domain activated and have the dns handling transfered to Digital Ocean. If you don't have a domain name yet, [please follow this tutorial](https://cphbusiness.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=f8e7ebbb-8d17-480b-9ac2-b15600a699f2).

2. Also, sign up on Digital Ocean if you haven't done that already. [Here is a tutorial](../toolbox/deployment_infrastructure/digitalocean_signup.md).

3. Make sure you have a **Droplet** running on Digital Ocean. [Here is a tutorial](../toolbox/deployment_infrastructure/droplet.md).

### In-class exercises

This week's CodeLab is a full pipeline exercise. You will set up a full CI/CD pipeline for a Java project using GitHub Actions, Docker Hub, and Watchtower. You will learn how to automate the building, testing, and deployment of your application in a containerized environment and later run it on a Digital Ocean server.

- [Codelab of the week](./exercises/codelab.md)

## Thursday (class) - Putting the pieces together - Integration testing with Security

No preparations needed for this day. But bring your laptop ;-)

## Friday (exercise day)

No Friday assignment this week. Use the day to finish the exercises from the week. And show up for the JumpStart Event in the auditorium from
09:00 to 12:00 and bring a friend.

![Jumpstart](./images/jumpstart.png)

<hr>

Check [TimeEdit](https://skema.cphbusiness.dk/) for time schedule, teacher, and location - and keep an eye on your inbox for urgent updates.
