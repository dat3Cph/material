---
title: Pipeline
description: Deployment Exercises
layout: default
nav_order: 1
parent: Exercises
grand_parent: Deployment
permalink: /deployment/exercises/pipeline/
---

### Tutorial: Setting Up a CI/CD Pipeline with GitHub Actions and Docker

![pipeline](./images/cicd-pipeline.png)

#### Introduction
This tutorial will guide you through creating a CI/CD pipeline for a Java project using GitHub Actions, Docker Hub, and Docker. You will learn how to automate the building, testing, and deployment of your application in a containerized environment and run it on a Digital Ocean server.

### Prerequisites
Before starting, ensure that you have the following:
1. A GitHub repository for your Java project.
2. A Docker Hub account.
3. Git and Docker installed on your machine for local testing.
4. A server on Digital Ocean with Docker installed.

### CI/CD Pipeline Overview
Our pipeline will consist of the following steps:

1. **Building the Project**: GitHub Actions will pull the code from the repository and build it using Maven.
2. **Running Tests**: All tests will be executed to ensure code quality and functionality.
3. **Creating a Docker Image**: Once the build and tests pass, a Docker image will be created using a `Dockerfile`.
4. **Pushing the Image to Docker Hub**: The created image will be tagged and pushed to Docker Hub for deployment.
5. **Running the Image on Digital Ocean**: The image will be pulled and run on a Digital Ocean server using `docker-compose`.

### Step 1: Setting Up the Project for CI/CD

1. **GitHub Actions Workflow File**:
   Create a file named `workflow.yml` inside the `.github/workflows` folder in the root of your project.

   ```yaml
   # .github/workflows/workflow.yml
   name: CI/CD WORKFLOW
   on:
     push:
       branches: [ main ]

   jobs:
     build:
       runs-on: ubuntu-latest

       steps:
         - name: Checkout
           uses: actions/checkout@v3

         - name: Set up JDK 17
           uses: actions/setup-java@v3
           with:
             java-version: '17'
             distribution: 'temurin'

         - name: Build with Maven
           run: mvn --batch-mode --update-snapshots package

         - name: Login to Docker Hub
           uses: docker/login-action@v2
           with:
             username: ${{ secrets.DOCKERHUB_USERNAME }}
             password: ${{ secrets.DOCKERHUB_TOKEN }}

         - name: Set up Docker Buildx
           uses: docker/setup-buildx-action@v2

         - name: Build and push Docker image
           uses: docker/build-push-action@v4
           with:
             context: .
             file: ./Dockerfile
             push: true
             tags: ${{ secrets.DOCKERHUB_USERNAME }}/<your-api-name>:latest
   ```

2. **Dockerfile**:
   Create a `Dockerfile` in the root of your project to define how your application should be built and run inside a Docker container.

   ```dockerfile
   # Dockerfile
   FROM eclipse-temurin:17-alpine
   COPY target/app.jar /app.jar
   EXPOSE 7070
   ENTRYPOINT ["java", "-jar", "/app.jar"]
   ```

3. **Maven Configuration**:
   Make sure you have the `maven-shade-plugin` in your `pom.xml` to package your application into a single JAR file:

   ```xml
   <build>
       <finalName>app</finalName> <!-- This is the name of the jar file -->
       <plugins>
           <!-- Maven Shade Plugin -->
           <plugin>
               <groupId>org.apache.maven.plugins</groupId>
               <artifactId>maven-shade-plugin</artifactId>
               <version>3.5.1</version>
               <configuration>
                   <transformers>
                       <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                           <mainClass>dk.lyngby.Main</mainClass> <!-- Update this with your main class -->
                       </transformer>
                   </transformers>
               </configuration>
               <executions>
                   <execution>
                       <phase>package</phase>
                       <goals>
                           <goal>shade</goal>
                       </goals>
                   </execution>
               </executions>
           </plugin>
       </plugins>
   </build>
   ```

4. **Setting Up GitHub Secrets**:
   To authenticate with Docker Hub, add two secrets to your GitHub repository:
    - `DOCKERHUB_USERNAME`: Your Docker Hub username.
    - `DOCKERHUB_TOKEN`: Your Docker Hub access token.

   Navigate to **Settings** → **Secrets** → **Actions** in your GitHub repository and add these two secrets.

### Step 2: Configuring Hibernate for Environment-Specific Configurations

Update your `HibernateConfig` file to use environment variables to determine which configuration to load. This setup will help switch between test, development, and production configurations.

**HibernateConfig.java**

```java
public class HibernateConfig {

    public static EntityManagerFactory getEntityManagerFactory() {
        if(System.getenv("PRODUCTION") != null) {
            return setupHibernateConfigurationForProduction();
        }
        return IS_TEST ? getEntityManagerFactoryConfigTest() : getEntityManagerFactoryConfigDevelopment();
    }

    private static EntityManagerFactory setupHibernateConfigurationForProduction() {
        Properties props = new Properties();
        props.put("hibernate.connection.url", System.getenv("JDBC_DATABASE_URL"));
        props.put("hibernate.connection.username", System.getenv("JDBC_DATABASE_USERNAME"));
        props.put("hibernate.connection.password", System.getenv("JDBC_DATABASE_PASSWORD"));
        return new Configuration().addProperties(props).buildSessionFactory();
    }
    
    // Other configuration methods for development and test environments
}
```

Make sure to set the following environment variables on your Digital Ocean server:
- `PRODUCTION`
- `JDBC_DATABASE_URL`
- `JDBC_DATABASE_USERNAME`
- `JDBC_DATABASE_PASSWORD`

### Step 3: Setting Up `docker-compose.yml` for Deployment

Create a `docker-compose.yml` file in the root of your project. This file will be used to run your Docker image on the Digital Ocean server.

```yaml
# docker-compose.yml
version: '3.8'
services:
  app:
    image: <your-dockerhub-username>/<your-api-name>:latest
    environment:
      - PRODUCTION=true
      - JDBC_DATABASE_URL=${JDBC_DATABASE_URL}
      - JDBC_DATABASE_USERNAME=${JDBC_DATABASE_USERNAME}
      - JDBC_DATABASE_PASSWORD=${JDBC_DATABASE_PASSWORD}
    ports:
      - "7070:7070"
    restart: unless-stopped
```

### Step 4: Deploying to Digital Ocean

1. **SSH into Your Digital Ocean Server**:
   ```bash
   ssh root@your_server_ip
   ```

2. **Set Environment Variables**:
   On the server, set the environment variables using the following commands:

   ```bash
   export JDBC_DATABASE_URL='your-database-url'
   export JDBC_DATABASE_USERNAME='your-database-username'
   export JDBC_DATABASE_PASSWORD='your-database-password'
   ```

3. **Run `docker-compose`**:
   Navigate to the directory containing `docker-compose.yml` and run:

   ```bash
   docker-compose up -d
   ```

This command will pull the latest Docker image from Docker Hub and run it with the specified environment variables.

### Final Thoughts
This pipeline ensures that any change pushed to the `main` branch is automatically built, tested, and deployed to Docker Hub, and can be easily deployed to your Digital Ocean server using `docker-compose`. Encourage your students to experiment with additional workflows and explore the capabilities of GitHub Actions for more complex CI/CD processes.

**Happy Coding!**