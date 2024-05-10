# Deployment Part1 Backend

- Deployment of the backend part of the project
- The backend is a Javalin API
- The API is deployed to a Digital Ocean droplet
- The API is deployed using Docker and Docker Hub
- The API is deployed using GitHub Actions
- The API is deployed using Docker Compose
- The API is connected to a PostgreSQL database


1. The first thing you need is a working backend API with Javalin. Preferable with security in place, that means a
   login and a signup endpoint. If not, for this part, it would be enough to have a simple endpoint that returns a string.
2. Create an account on Docker Hub. It's free, and you can sign up with your GitHub account. https://hub.docker.com/
3. Create an API token on Docker Hub. You can do this by going to your Docker Hub account settings and then click on
   "Security" in the left menu. Then click on "New Access Token" and give it a name. Remember to save the token somewhere
   safe. You will need it later. Just give it all the permissions for now.
4. Add Dockerfile to your project

```dockerfile
FROM eclipse-temurin:17-alpine
# This is the jar file that you want to run
COPY target/app.jar /app.jar
# This is the port that your javalin application will listen on
EXPOSE 7070
# This is the command that will be run when the container starts
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

The Dockerfile is a file that tells Docker how to build your image. The first line tells Docker which image to use as a
base. In this case, we are using the official OpenJDK image. The second line copies the jar file that you want to run
into the image. The third line exposes the port that your Javalin application will listen on. The fourth line is the
command that will be run when the container starts. In this case, it is running the jar file with Java.

5. In your pom.xml file, add the following build tag:

**Remember to replace the comments between the mainClass tags, with the path to your main class. The path should be relative to the src/main/java!!**
**Main class is the class that has the main method**

```xml
    <build>
    <finalName>app</finalName> <!-- This is the name of the jar file -->

    <plugins>

        <!--  Pom.xml properties plugin  -->

        <plugin>
            <!--  https://www.baeldung.com/java-accessing-maven-properties  -->
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>properties-maven-plugin</artifactId>
            <version>1.2.1</version>
            <executions>
                <execution>
                    <phase>generate-resources</phase>
                    <goals>
                        <goal>write-project-properties</goal>
                    </goals>
                    <configuration>
                        <outputFile>${project.build.outputDirectory}/properties-from-pom.properties</outputFile>
                    </configuration>
                </execution>
            </executions>
        </plugin>

        <!--   Surefire plugin (Testing)  -->

        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>3.0.0</version>
        </plugin>

        <!--   Shade plugin (JAR)  -->

        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>3.5.1</version>
            <configuration>
                <transformers>
                    <transformer
                            implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>
                            <!-- ========================================================= -->
                            <!-- The plugin needs to know which class has the main method  -->
                            <!-- therefore we need to specify the path to the main class   -->
                            <!-- ========================================================= -->
                        </mainClass>
                    </transformer>
                </transformers>
                <filters>
                    <filter> <!-- This filter is needed to avoid a bug in the shade plugin -->
                        <artifact>*:*</artifact>
                    </filter>
                </filters>
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

6. Run Maven lifecycle `install`. This will download all dependencies, compile the code, run the tests, and create a jar file in the target folder.
7. Add Docker Hub secrets to GitHub repository. On your GitHub repository, go to "Settings" -> "Secrets" -> "New repository secret". Add the following secrets:
    - DOCKERHUB_USERNAME (your Docker Hub username)
    - DOCKERHUB_TOKEN (the token you created in step 3)
8. In the root of your project, create a folder called `.github` and inside that folder, create a folder called `workflows`. Inside the workflows folder, create a file called `build.yml`. The path should look like this:

`.github
workflows
build.yml`

9. Add the following code to the build.yml file:

Replace `<your-api-name>` with the name of your API. This will be the name of the Docker image.

```yaml
name: API JAVALIN WORKFLOW
on:
  push:
    branches: [ main ]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      -
        # https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-java-with-maven
        name: Checkout
        uses: actions/checkout@v3
      -
        name: Set up JDK 17
        uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'
      -
        name: Build with Maven
        run: mvn --batch-mode --update-snapshots package
      -
        # https://docs.docker.com/build/ci/github-actions/tr
        name: Login to Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}
      -
        name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2
      -
        name: Build and push
        uses: docker/build-push-action@v4
        with:
          context: .
          file: ./Dockerfile
          push: true
          tags: ${{ secrets.DOCKERHUB_USERNAME }}/<your-api-name>:latest
```
10. We also need to change our Hibernate file to use environment variables for the database connection. This is because
    we don't want to hardcode the database connection in the code. We want to be able to change it easily when we deploy the
    application. In the HibernateUtil.java file, add the buildEntityFactoryConfig below to your setup.

After that you will have three different Hibernate configurations. One for local development, one for testing, and one
for deployment. The deployment configuration will use environment variables for the database connection.

```java
private static EntityManagerFactory buildEntityFactoryConfigDeployed() {
    try {
        Configuration configuration = new Configuration();

        Properties props = new Properties();

        props.put("hibernate.connection.url", System.getenv("CONNECTION_STR") + System.getenv("DB_NAME"));
        props.put("hibernate.connection.username", System.getenv("DB_USERNAME"));
        props.put("hibernate.connection.password", System.getenv("DB_PASSWORD"));
        props.put("hibernate.dialect", "org.hibernate.dialect.PostgreSQLDialect"); // dialect for postgresql
        props.put("hibernate.connection.driver_class", "org.postgresql.Driver"); // driver class for postgresql
        props.put("hibernate.archive.autodetection", "class"); // hibernate scans for annotated classes
        props.put("hibernate.current_session_context_class", "thread"); // hibernate current session context
        props.put("hibernate.hbm2ddl.auto", "update"/*"create-drop"*/); // hibernate creates tables based on entities
        return getEntityManagerFactory(configuration, props);
    } catch (Throwable ex) {
        System.err.println("Initial SessionFactory creation failed." + ex);
        throw new ExceptionInInitializerError(ex);
    }
}
```

You also need to create a method that gets the EntityManagerFactory instance with the right configuration and properties,
independence if you are using the local, test or deployment configuration. It could look like this:

```JAVA
public static EntityManagerFactory getEntityManagerFactory(boolean isTest) {
    if (isTest) return getEntityManagerFactoryConfigTest();
    boolean isDeployed = (System.getenv("DEPLOYED") != null);
    if (isDeployed) return getEntityManagerFactoryConfigIsDeployed();
    return getEntityManagerFactoryConfigDevelopment();
}
```

11. Push til Git repository and check the actions tab on GitHub to see if the workflow runs successfully
    The workflow will run every time you push to the main branch. It will compile the code, create a jar file, build a Docker image, and push it to Docker Hub.
    Check on Docker Hub to see if the image is there.
12. Login to your droplet via your terminal. `ssh <your_user>@<your-droplet-ip>`
13. Stop and delete all running docker containers running on your server
14. Create a folder on your droplet called deployment. `mkdir /deployment`
15. Create a docker-compose.yml file in the deployment folder. `nano /deployment/docker-compose.yml`
16. Paste the following code in the docker-compose.yml file

**Replace all the placeholders with your own values!!**

```bash
version: '3.9'

services:
   restapi:
      image: <docker_hub-username>/<your-docker-image-name>:latest
      container_name: restapi
      restart: unless-stopped
      networks:
         - frontend
         - backend
      environment:
        CONNECTION_STR: jdbc:postgresql://db:5432/
        DB_USERNAME: <your_postgres_user>
        DB_PASSWORD: <your_postgres_password>
        DB_NAME: <your_postgres_db_name>
        DEPLOYED: TRUE
        SECRET_KEY: 841D8A6C80CBA4FCAD32D5367C18C53B
        TOKEN_EXPIRE_TIME: 1800000
        ISSUER: cphbusiness.dk
      ports:
         - "7070:7070"

   db:
      image: postgres:latest
      container_name: db
      restart: unless-stopped
      networks:
         - backend
      environment:
         POSTGRES_USER: <your_postgres_user>
         POSTGRES_PASSWORD: <your_postgres_password>
      volumes:
         - ./data:/var/lib/postgresql/data/
      ports:
         - "5432:5432"

networks:
   frontend:
      name: frontend
      driver: bridge
   backend:
      name: backend
      driver: bridge
```
17. Run docker-compose up in the deployment folder. This will start the containers and the API should be up and running.
18. Create database inside docker container or use pgadmin
```bash  
docker exec -it postgres_container psql -U postgres
CREATE DATABASE mydatabase;
```
