# Docker and Docker Compose
[Read the docs](https://docker-curriculum.com/)

Docker is a tool that makes it easy to create, deploy, and run applications by using containers. 
Containers allow a developer to package up an application with all of the parts it needs, such as libraries and other dependencies, and ship it all out as one package. 
By doing so, thanks to the container, the developer can rest assured that the application will run on any other Linux machine regardless of any customized settings that machine might have that could differ from the machine used for writing and testing the code.
Docker containers are build from images. An image is a read-only template with instructions for creating a Docker container.
Often, an image is based on another image, with some additional customization. 
For example, you may build an image which is based on the ubuntu image, but installs some software like JDK and your application, as well as the configuration details needed to make your application run.
Images are stored in a Docker registry such as registry.hub.docker.com from where it is easy to share images with other developers.

## Demo
### Hello World
Run the following command in your terminal:
```bash
docker run hello-world
```
- Take a look at the output and try to understand what is happening.
- To see the images you have downloaded, run the following command in your terminal: `docker images`
- To see the containers you have downloaded, run the following command in your terminal: `docker ps -a`
- Run the following command in your terminal: `docker rm distracted_bhaskara` to remove the container again after you are done.
- Run the following command in your terminal: `docker rmi hello-world` to remove the image again after you are done.

### more parameters
Run the following command in your terminal:
```bash
docker run -d -p 8008:80 --name static-site prakhar1989/static-site
```
- `-d` for daemon mode (run in background and frees up terminal)
- `-p` for port mapping (host:container)
- `--name` for naming the container
- `prakhar1989/static-site` is the image name that gets downloaded from the registry (docker hub)
- Take a look at the browser adress: `http://localhost:8008` to see the result.

### docker compose
Docker compose is a tool for defining and running multi-container Docker applications. 
It also helps script the starting and stopping of these containers in a way that is repeatable across different environments.
- Create a file called `compose.yaml` in some empty folder.
- Copy the following content into the file:
```yaml
version: '3'
services:
  web:
    image: prakhar1989/static-site
    container_name: static-site-from-compose
    ports:
      - "8008:80"
```
- Run the following command in your terminal: `docker-compose up -d` to start the container.
- Take a look at the browser adress: `http://localhost:8008` to see the result.
- Run the following command in your terminal: `docker-compose down` to stop the container again.
- Remove images to clean up.

### docker compose with multiple containers
- Create a file called `compose.yaml` in some empty folder.
- Copy the following content into the file:
```yaml
version: '3'
services:
  web:
    image: prakhar1989/static-site
    container_name: static-site-from-compose
    ports:
      - "8008:80"
  redis:
    image: redis
    container_name: redis-from-compose
    ports:
      - "6379:6379"
```
- Run the following command in your terminal: `docker-compose up` to start the containers.

### docker compose with multiple containers and volumes
- Create a file called `compose.yaml` in some empty folder.
- Copy the following content into the file:
```yaml
version: '3'
services:
  web:
    image: prakhar1989/static-site
    container_name: static-site-from-compose
    ports:
      - "8008:80"
    volumes:
      - ./static-site:/usr/share/nginx/html
  redis:
    image: redis
    container_name: redis-from-compose
    ports:
      - "6379:6379"
```
- Create a file called `index.html` in the folder `static-site` and add some content.
- Run the following command in your terminal: `docker-compose up` to start the containers.
- Take a look at the browser adress: `http://localhost:8008` to see the result.

### docker compose with multiple containers and volumes and environment variables
- Create a file called `compose.yaml` in some empty folder.
- Copy the following content into the file:
```yaml
version: '3'
services:
  web:
    image: prakhar1989/static-site
    container_name: static-site-from-compose
    ports:
      - "8008:80"
    volumes:
      - ./static-site:/usr/share/nginx/html
    environment:
      - AUTHOR=YourName
  redis:
    image: redis
    container_name: redis-from-compose
    ports:
      - "6379:6379"
```
- Create a file called `index.html` in the folder `static-site` and add some content.
- Run the following command in your terminal: `docker-compose up` to start the containers.

### docker compose using a Dockerfile
- Create a file called `compose.yaml` in some empty folder.
- Copy the following content into the file:
```yaml
version: '3'
services:
  web:
    build: .
    container_name: my-static-site
    ports:
      - "8008:80"
    volumes:
      - ./static-site:/usr/share/nginx/html
    environment:
      - AUTHOR=YourName
  redis:
    image: redis
    container_name: redis-from-compose
    ports:
      - "6379:6379"
``` 
- Create a file called `Dockerfile` in the same folder and add the following content:
```dockerfile
FROM nginx:alpine
ENV AUTHOR=YourName
COPY static-site /usr/share/nginx/html
```
- Create a file called `index.html` in the folder `static-site` and add some content.
- Run the following command in your terminal: `docker-compose up` to start the containers.

