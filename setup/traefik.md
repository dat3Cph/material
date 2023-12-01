# Setting up traefik for edge/reverse proxy routing
Setting up traefik to listen to docker events and route traffic to containers based on labels.
- There are to files that should be created in the root of the project on you docker enabled droplet:
  - `docker-compose.yml`
  - `.env`
- In docker compose we can define the traefik container and the other containers we want to route traffic to.
- Traefik container

- `docker-compose.yml`:
```yaml
version: "3.3"

services:

  traefik:
    image: "traefik:v2.10"
    container_name: "traefik"
    command:
      #- "--log.level=DEBUG"
      - "--api.insecure=true"
      - "--providers.docker=true"
      - "--providers.docker.exposedbydefault=false"
      - "--entrypoints.websecure.address=:443"
      - "--entrypoints.web.address=:80"
      - "--entrypoints.web.http.redirections.entrypoint.to=websecure"
      - "--entrypoints.web.http.redirections.entrypoint.scheme=https"
      - "--certificatesresolvers.myresolver.acme.tlschallenge=true"
      #- "--certificatesresolvers.myresolver.acme.caserver=https://acme-staging-v02.api.letsencrypt.org/directory"
      - "--certificatesresolvers.myresolver.acme.email=thomas@webtrade.dk"
      - "--certificatesresolvers.myresolver.acme.storage=/letsencrypt/acme.json"
    ports:
      - "443:443"
      - "8080:8080"
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
      - "traefik.http.routers.whoami.rule=Host(`whoami.cphbusinessapps.dk`)"
      - "traefik.http.routers.whoami.entrypoints=websecure"
      - "traefik.http.routers.whoami.tls.certresolver=myresolver"

  europe:
    image: "webtrade/europemap:latest"
    container_name: "europeapp"
    networks:
      - backend
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.europe.rule=Host(`europe.cphbusinessapps.dk`)"
      - "traefik.http.routers.europe.entrypoints=websecure"
      - "traefik.http.routers.europe.tls.certresolver=myresolver"
      - "com.centurylinklabs.watchtower.enable=false"

  db:
    image: postgres:latest
    container_name: db
    restart: unless-stopped
    environment:
      POSTGRES_USER: dev
      POSTGRES_PASSWORD: ax2
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

  api:
    image: tyskerdocker/javalinapi:latest
    container_name: api
    environment:
      - CONNECTION_STR=${CONNECTION_STR}
      - DB_USERNAME=${DB_USERNAME}
      - DB_PASSWORD=${DB_PASSWORD}
      - DEPLOYED=TRUE
      - SECRET_KEY=${SECRET_KEY}
      - TOKEN_EXPIRE_TIME=${TOKEN_EXPIRE_TIME}
      - ISSUER=${ISSUER}
    ports:
      - "7070:7070"
    networks:
      - backend
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.api.rule=Host(`api.cphbusinessapps.dk`)"
      - "traefik.http.routers.api.entrypoints=websecure"
      - "traefik.http.routers.api.tls.certresolver=myresolver"
      - "com.centurylinklabs.watchtower.enable=true"

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
- `.env` file in root of project next to `docker-compose.yml`: 
```env
CONNECTION_STR=jdbc:postgresql://db:5432/
DB_USERNAME=dev
DB_PASSWORD=ax2
DEPLOYED=TRUE
SECRET_KEY=FGHkj89DFi345DKWdsd8911G22Woas31v
TOKEN_EXPIRE_TIME=1800000
ISSUER=cphbusinessapps.dk


```
