# Træfik Setup Remote

## Requirements

- [DigitalOcean](https://www.digitalocean.com/) account
- [Droplet with Docker preinstalled (Marketplace)](https://marketplace.digitalocean.com/apps/docker)
- [DockerHub](https://hub.docker.com/search?q=) Docker-Hub account
- [Domain](https://punktum.dk/) name 
- Your domain is pointing to DigitalOcean DNS servers
- Wildcard DNS record for your domain (*.your_domain) setup on DigitalOcean

## Features

- [Traefik](https://doc.traefik.io/traefik/) as a reverse proxy
- [Let's Encrypt](https://letsencrypt.org/) for SSL certificates
- [Traefik Dashboard](https://docs.traefik.io/operations/dashboard/) for monitoring
- [PostgreSQL](https://www.postgresql.org/) for database
- [Docker](https://www.docker.com/) for containerization
- [Docker Compose](https://docs.docker.com/compose/) for container orchestration
- [DigitalOcean](https://www.digitalocean.com/) for cloud hosting

## Setup

### 1. SSH into your DigitalOcean droplet and `cd` into the folder where you want to store your project.
- `mkdir <your_project_name>` to create a new folder
- Inside the folder run `nano docker-compose.yml` to create a new docker-compose file and paste in the following code:

```bash
version: "3.3"

services:

  traefik:
    image: "traefik:v2.10"
    container_name: "traefik"
    restart: unless-stopped
    command:
      - "--log.level=DEBUG"
      # - "--api.insecure=true"
      - "--api.dashboard=true"
      - "--providers.docker=true"
      - "--providers.docker.exposedbydefault=false"
      - "--entrypoints.websecure.address=:443"
      - "--entrypoints.web.address=:80"
      - "--entrypoints.web.http.redirections.entrypoint.to=websecure"
      - "--entrypoints.web.http.redirections.entrypoint.scheme=https"
      - "--entrypoints.web.http.redirections.entrypoint.permanent=true"
      - "--certificatesresolvers.myresolver.acme.tlschallenge=true"
      - "--certificatesresolvers.myresolver.acme.email=YOUR_EMAIL"
      - "--certificatesresolvers.myresolver.acme.storage=/letsencrypt/acme.json"
      # Enable dashboard
      - "--api.dashboard=true"
    # Dynamic Configuration
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.traefik_https.rule=Host(`traefik.YOUR_DOMAIN.dk`)"
      - "traefik.http.routers.traefik_https.entrypoints=websecure"
      - "traefik.http.routers.traefik_https.tls=true"
      - "traefik.http.routers.traefik_https.tls.certResolver=myresolver"
      - "traefik.http.routers.traefik_https.service=api@internal"
      - "traefik.http.routers.traefik_https.middlewares=auth"
      - "traefik.http.middlewares.auth.basicauth.users=YOUR_USER_SEE_HINT_BELOW"
      - "traefik.http.middlewares.auth.basicauth.realm=Restricted Area"
        
    ports:
      - "443:443"
      - "80:80"
    networks:
      - backend
    volumes:
      - "./letsencrypt:/letsencrypt"
      - "/var/run/docker.sock:/var/run/docker.sock:ro"

  whoami:
    image: "traefik/whoami"
    container_name: "simple-service"
    networks:
      - backend
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.whoami.rule=Host(`whoami.YOURDOMAIN.dk`)"
      - "traefik.http.routers.whoami.entrypoints=websecure"
      - "traefik.http.routers.whoami.tls.certresolver=myresolver"
      - "com.centurylinklabs.watchtower.enable=true"
  
  db:
    image: postgres:latest
    container_name: db
    restart: unless-stopped
    environment:
      POSTGRES_USER: YOUR_POSTGRES_USER
      POSTGRES_PASSWORD: YOUR_POSTGRES_PASSWORD
    volumes:
      - ./data:/var/lib/postgresql/data/
      - ./db/init.sql:/docker-entrypoint-initdb.d/init.sql
    ports:
      - "5432:5432"
    networks:
      - backend
    labels:
      # Watchtower configuration
      - "com.centurylinklabs.watchtower.enable=false"

  watchtower:
    image: containrrr/watchtower
    container_name: watchtower
    environment:
      REPO_USER: webtrade
      REPO_PASS: ${DOCKERHUB_TOKEN}
    labels:
      com.centurylinklabs.watchtower.enable: "false"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    networks:
      - backend
    command: --interval 600 --cleanup --debug # checks for updates every 600 seconds (10 min), cleans up old images, and outputs debug logs

networks:
  backend:
    driver: bridge
```
- HINT: To generate a traefik hashed dashboard login (droplet linux terminal ) run the following command: `echo $(htpasswd -nb <your_username> <your_password>) | sed -e s/\\$/\\$\\$/g`

### 2. Create a folder: `db` with a file called `init.sql` inside the folder
- Run the following commands in your droplet terminal: `mkdir db && cd db && nano init.sql`
- Paste the following code into the init.sql file:
```bash
-- create role
CREATE ROLE dev WITH LOGIN CREATEDB PASSWORD 'ax2';

-- create databases
CREATE DATABASE projectdb;
```
- The code will run when you start the docker-compose file and create a new user and database

### 3. Generate a token from DockerHub
- Go to [DockerHub](https://hub.docker.com/) and login
- Go to your profile settings and click on `Security`
- Click on `New Access Token`
- Give your token a name and click on `Create`
- Copy the token and save it somewhere safe

### 4. Create a .env file at the root of your Digital Ocean folder and add the following environment variables

```bash
DOCKERHUB_TOKEN=TOKEN_GENERATED_FROM_DOCKERHUB
CONNECTION_STR=jdbc:postgresql://db:5432/
DB_USERNAME=dev # Change to your own username
DB_PASSWORD=ax2 # Change to your own password
DEPLOYED=TRUE
SECRET_KEY=nGHkj89DFi345gGWdsd8911G22Woas31v # For JWT
TOKEN_EXPIRE_TIME=1800000 # 30 minutes
ISSUER=YOUR_DOMAIN
USER=admin:$$apr1$$Zrm/YMJT$$HelFjM1BjPO4Mr2uCQXP. # Change to your own username and password generated from the htpasswd command
```
- These vaules can be read from your docker-compose file using the following syntax: `${ENVIRONMENT_VARIABLE_NAME}`

###  Docker commands
- Start the docker containers with the following command: `docker-compose up -d `
- Check if all containers are running with `docker ps -a`
- Stop and remove the docker containers with the following command: `docker-compose down`

### Access Traefik Dashboard through browser
- Go to the following url in your browser: `traefik.<your_domain>`

## Debugging

- Check if all containers are running with `docker ps -a`
- Check if all env variables are set in .env file and are correct
- Check if docker compose has read all environment variables with `docker-compose config`
- Check the logs of the individual container with `docker logs <container_name>` or `docker logs --follow <container_name>`
- Did you remember to add your domain to the DigitalOcean DNS servers?
- Did you remember to add a wildcard DNS record for your domain?
- Did you remember to create the acme.json file and set the correct permissions?
- Run your docker compose file with `docker-compose up` (without the -d flag) and check the output logs for errors