---
title: 8. Docker and Caddy
description: Deployment with your own domain name
layout: default
parent: Deployment
grand_parent: Toolbox
permalink: /toolbox/deployment/docker-caddy/
nav_order: 9
---

OBS! This tutorial is a work in progress. It's not finished yet - but will be ready for Wednesday this week.

# 8. Deployment on Droplet with Docker and Caddy

You have chosen the `dark red pill`. Good choice. Now you will end up with a website running on you own domain name. There is no way back. You are now a full stack developer. Congratulations!

![Red or Blue](./images/red.webp)

Okay, time to dive in:

This is how you can deploy a [Javalin](https://javalin.io/) webproject on a virtual machine (VM) running [Ubuntu](https://ubuntu.com/) and [Docker](https://www.docker.com/).

You can follow this [video tutorial](https://cphbusiness.cloud.panopto.eu/Panopto/Pages/Sessions/List.aspx?folderID=322ab819-f0ca-4fc4-8e76-b15600a65ecd) that explains the steps below:

## Prerequstites

- A configured Virtual Machine setup up after this [tutorial](https://github.com/dat2Cph/content/tree/main/linux_and_deployment) step 1-7. The VM is running on [Digital Ocean](https://www.digitalocean.com/)
- A Postgresql database running on port 5432
- A Javalin webproject ready to run on port 7070
- A built version of the Javalin project created as a "fat jar"
- A domain name or subdomain with DNS set to the IP of your VM
- A firewall that allows access for port 80 and 443 (http and https)
- A ssh connection to the VM

## Goal

We wish to host the Javalin web API and make it accessible through a subdomain. We also want to host a static page on the main domain name. The idea is that the static webpage can be used as a
portfolio content page, that links to your Javalin webapplications each running on their own subdomain. The setup will be able to handle a number of Javalin webapplications and static webpages, but as a beginning we set up only one. Each webapplication will run in an isolated Docker container.

We also wish to get access to the web applications through https. For this we use [Caddy Server](https://caddyserver.com/) as a reverse proxy server and static file server. Caddy Server is also running in its own Docker Container.

As a last thing, we also want to use a [Postgresql database](https://www.postgresql.org/) from our Javalin Webapplication.

## Recipe

TBD
