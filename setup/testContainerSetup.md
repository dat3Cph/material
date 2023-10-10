# Testcontainer setup

Get an [overview of test scenarios](../flow3/2_security/understanding_the_test_setup.md) here.

This repository holds an example code base of setting up test-containers for tests: [https://github.com/dat3Cph/3sem-javalin-rest-api](https://github.com/dat3Cph/3sem-javalin-rest-api). Explanations and 'how-to' will follow below:

You will need to go through these three steps to prepare for using test-containers:

1. Prepare your `pom.xml` with properties and extra test-container dependencies.
2. Add a util method called getProperty(String propName) in the ApplicationConfig class. This method will make it
possible to read properties from the pom.xml file. This is handy to feed in values to the Hibernate setup. Like `db.name`, `db.username`, and `db.password`.
3. Modify / overwrite the HibernateConfig file. The new version will provide a boolean ´isTest´ attribute, that can signal whether
the connectionpool should be hooked onto the real database (normal situation) - or be using the test-containers and a test database.
4. Setup your test class for the test EntityManagerFactory
5. Stuff some test data in the database (populate)
6. Use Rest Assured to perform you first REST test
7. Complete the remaining tests

Code-snippets are provided below:

## 1. Prepare your `pom.xml`

First, overwrite pom.xml with the version below. Make sure to set the ` <db.name>startcode</db.name>` to a database name
that you actually have on your Postgres database server:

```Java
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>dk.lyngby</groupId>
    <artifactId>hotel_rest_3sem</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
        <hibernate-version>6.2.4.Final</hibernate-version>
        <restassured.version>5.3.0</restassured.version>
        <testcontainers.version>1.18.0</testcontainers.version>
        <junit.version>5.9.1</junit.version>

        <!-- Project properties  -->
        <!--  token    -->
        <secret.key>841D8A6C80CBA4FCAD32D5367C18C53B</secret.key>
        <issuer>cphbusiness.dk</issuer>
        <token.expiration.time>3600000</token.expiration.time>
        <!--  DB    -->
        <db.name>startcode</db.name>
        <db.username>postgres</db.username>
        <db.password>postgres</db.password>
        <db.connection.string>jdbc:postgresql://localhost:5432/</db.connection.string>
        <!--  Javalin    -->
        <javalin.port>7070</javalin.port>
    </properties>
    <dependencies>

        <!--   R.E.S.T     -->

        <dependency>
            <groupId>io.javalin</groupId>
            <artifactId>javalin-bundle</artifactId>
            <version>5.6.1</version>
        </dependency>
        <dependency>
            <groupId>com.fasterxml.jackson.core</groupId>
            <artifactId>jackson-databind</artifactId>
            <version>2.15.0</version>
        </dependency>
        
        <!--  Utilities      -->
        <dependency>
            <groupId>com.google.code.gson</groupId>
            <artifactId>gson</artifactId>
            <version>2.10.1</version>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.28</version>
            <scope>provided</scope>
        </dependency>

        <!--   Security     -->

        <dependency>
            <!--  https://nimbusds.com/products/nimbus-jose-jwt   -->
            <groupId>com.nimbusds</groupId>
            <artifactId>nimbus-jose-jwt</artifactId>
            <version>9.0.1</version>
        </dependency>
        <dependency>
            <groupId>org.mindrot</groupId>
            <artifactId>jbcrypt</artifactId>
            <version>0.4</version>
        </dependency>

        <!--  DB    -->

        <dependency>
            <groupId>org.postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <version>42.6.0</version>
        </dependency>
        <dependency>
            <groupId>org.hibernate.orm</groupId>
            <artifactId>hibernate-core</artifactId>
            <version>${hibernate-version}</version>
        </dependency>
        <dependency>
            <!--   Hibernate Connection Pool      -->
            <groupId>com.zaxxer</groupId>
            <artifactId>HikariCP</artifactId>
            <version>5.0.1</version>
        </dependency>
        <dependency>
            <!--   Hibernate Connection Pool      -->
            <groupId>org.hibernate.orm</groupId>
            <artifactId>hibernate-hikaricp</artifactId>
            <version>${hibernate-version}</version>
        </dependency>

        <!--  Logging   -->

        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>1.4.7</version>
        </dependency>
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-core</artifactId>
            <version>1.4.7</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>2.0.7</version>
        </dependency>

        <!--  TESTING      -->

        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>${junit.version}</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-engine</artifactId>
            <version>${junit.version}</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-params</artifactId>
            <version>${junit.version}</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.hamcrest</groupId>
            <artifactId>hamcrest</artifactId>
            <version>2.2</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.testcontainers</groupId>
            <artifactId>testcontainers</artifactId>
            <version>${testcontainers.version}</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.testcontainers</groupId>
            <artifactId>postgresql</artifactId>
            <version>${testcontainers.version}</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.testcontainers</groupId>
            <artifactId>jdbc</artifactId>
            <version>${testcontainers.version}</version>
        </dependency>
        <dependency>
            <groupId>org.testcontainers</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>${testcontainers.version}</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>io.rest-assured</groupId>
            <artifactId>rest-assured</artifactId>
            <version>${restassured.version}</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>io.rest-assured</groupId>
            <artifactId>json-schema-validator</artifactId>
            <version>${restassured.version}</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <finalName>app</finalName> <!-- This is the name of the jar file -->
        <plugins>

            <!--  Pom.xml properties plugin  -->

            <plugin>
                <!--  https://www.baeldung.com/java-accessing-maven-properties  -->
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>properties-maven-plugin</artifactId>
                <version>1.0.0</version>
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
        </plugins>
    </build>
</project>
```

## 2. Add a util method called getProperty(String propName)

This one is easy peasy:

Add these methods to the bottom of the ApplicationConfig.class:

```Java
public static String getProperty(String propName) throws IOException
    {
        try (InputStream is = HibernateConfig.class.getClassLoader().getResourceAsStream("properties-from-pom.properties"))
        {
            Properties prop = new Properties();
            prop.load(is);
            return prop.getProperty(propName);
        } catch (IOException ex) {
            ex.printStackTrace();
            throw new IOException("Could not read property from pom file. Build Maven!");
        }
    }

public static void startServer(Javalin app, int port) {
        Routes routes = new Routes();
        app.updateConfig(ApplicationConfig::configuration);
        app.routes(routes.getRoutes(app));
        //HibernateConfig.setTest(false);
        app.start(port);
    }

    public static void stopServer(Javalin app) {
        app.stop();
    }
```


## 3. Prepare HibernateConfig.java

Use and modify this version of the HibernateConfig.java file. This will add a boolean `isTest` attribute, which
can be used for indication that `getEntityManagerFactory()` should return a factory that holds connections to
a test container with a Postgres Database.

```Java
package dk.lyngby.config;

import dk.lyngby.config.ApplicationConfig;
import dk.lyngby.model.Hotel;
import dk.lyngby.model.Room;
import jakarta.persistence.EntityManagerFactory;
import lombok.NoArgsConstructor;
import org.hibernate.SessionFactory;
import org.hibernate.boot.registry.StandardServiceRegistryBuilder;
import org.hibernate.cfg.Configuration;
import org.hibernate.service.ServiceRegistry;
import java.util.Properties;

@NoArgsConstructor(access = lombok.AccessLevel.PRIVATE)
public class HibernateConfig {
    private static EntityManagerFactory entityManagerFactory;
    private static Boolean isTest = false;

    private static EntityManagerFactory buildEntityFactoryConfigDev() {
        try {
            Configuration configuration = new Configuration();

            Properties props = new Properties();

            boolean isDeployed = (System.getenv("DEPLOYED") != null);

            if(isDeployed) {
                String DB_USERNAME = System.getenv("DB_USERNAME");
                String DB_PASSWORD = System.getenv("DB_PASSWORD");
                String CONNECTION_STR = System.getenv("CONNECTION_STR") + ApplicationConfig.getProperty("db.name");
                props.setProperty("hibernate.connection.url", CONNECTION_STR);
                props.setProperty("hibernate.connection.username", DB_USERNAME);
                props.setProperty("hibernate.connection.password", DB_PASSWORD);
            } else {
                props.put("hibernate.connection.url", ApplicationConfig.getProperty("db.connection.string") + ApplicationConfig.getProperty("db.name"));
                props.put("hibernate.connection.username", ApplicationConfig.getProperty("db.username"));
                props.put("hibernate.connection.password", ApplicationConfig.getProperty("db.password"));
                props.put("hibernate.show_sql", "true"); // show sql in console
                props.put("hibernate.format_sql", "true"); // format sql in console
                props.put("hibernate.use_sql_comments", "true"); // show sql comments in console
            }
            props.put("hibernate.dialect", "org.hibernate.dialect.PostgreSQLDialect"); // dialect for postgresql
            props.put("hibernate.connection.driver_class", "org.postgresql.Driver"); // driver class for postgresql
            props.put("hibernate.archive.autodetection", "class"); // hibernate scans for annotated classes
            props.put("hibernate.current_session_context_class", "thread"); // hibernate current session context
            props.put("hibernate.hbm2ddl.auto", "update"); // hibernate creates tables based on entities

            // Hibernate Default Pool Configuration
            // https://www.mastertheboss.com/hibernate-jpa/hibernate-configuration/configure-a-connection-pool-with-hibernate/
            props.put("hibernate.connection.provider_class", "org.hibernate.hikaricp.internal.HikariCPConnectionProvider");// Maximum waiting time for a connection from the pool
            props.put("hibernate.hikari.connectionTimeout", "10000"); // Minimum number of ideal connections in the pool
            props.put("hibernate.hikari.minimumIdle", "5"); // Maximum number of actual connection in the pool
            props.put("hibernate.hikari.maximumPoolSize", "20"); // Maximum time that a connection is allowed to sit ideal in the pool
            props.put("hibernate.hikari.idleTimeout", "200000"); // Maximum size of statements that has been prepared

            return getEntityManagerFactory(configuration, props);
        } catch (Throwable ex) {
            System.err.println("Initial SessionFactory creation failed." + ex);
            throw new ExceptionInInitializerError(ex);
        }
    }

    private static EntityManagerFactory buildEntityFactoryConfigTest() {
        try {
            Configuration configuration = new Configuration();

            Properties props = new Properties();
            props.put("hibernate.dialect", "org.hibernate.dialect.PostgreSQLDialect");
            props.put("hibernate.connection.driver_class", "org.testcontainers.jdbc.ContainerDatabaseDriver");
            props.put("hibernate.connection.url", "jdbc:tc:postgresql:15.3-alpine3.18:///test_db");
            props.put("hibernate.connection.username", "postgres");
            props.put("hibernate.connection.password", "postgres");
            props.put("hibernate.archive.autodetection", "class");
            props.put("hibernate.show_sql", "true");
            props.put("hibernate.hbm2ddl.auto", "create-drop");

            return getEntityManagerFactory(configuration, props);
        } catch (Throwable ex) {
            System.err.println("Initial SessionFactory creation failed." + ex);
            throw new ExceptionInInitializerError(ex);
        }
    }

    private static EntityManagerFactory getEntityManagerFactory(Configuration configuration, Properties props) {
        configuration.setProperties(props);

        getAnnotationConfiguration(configuration);

        ServiceRegistry serviceRegistry = new StandardServiceRegistryBuilder().applySettings(configuration.getProperties()).build();
        System.out.println("Hibernate Java Config serviceRegistry created");

        SessionFactory sf = configuration.buildSessionFactory(serviceRegistry);
        return sf.unwrap(EntityManagerFactory.class);
    }


    private static void getAnnotationConfiguration(Configuration configuration) {
        configuration.addAnnotatedClass(Hotel.class);
        configuration.addAnnotatedClass(Room.class);
    }

    private static EntityManagerFactory getEntityManagerFactoryConfigDev() {
        if (entityManagerFactory == null) entityManagerFactory = buildEntityFactoryConfigDev();
        return entityManagerFactory;
    }

    private static EntityManagerFactory getEntityManagerFactoryConfigTest() {
        if (entityManagerFactory == null) entityManagerFactory = buildEntityFactoryConfigTest();
        return entityManagerFactory;
    }

    public static EntityManagerFactory getEntityManagerFactory() {
        if (isTest) return getEntityManagerFactoryConfigTest();
        return getEntityManagerFactoryConfigDev();
    }

    public static void setTest(Boolean test) {
        isTest = test;
    }

    public static Boolean getTest() {
        return isTest;
    }
}
```

## 4. Setup your test class for the test EntityManagerFactory

First, lets create a place for the REST - tests to be:

Find the `HotelController.class` file, generate the Test by right-clicking in the class + choose Generate -> Test ... :

![](./images/testsetup_intellij.png)

Now we have a skeleton for the test class, and it's time to setup the test-container:

The tricks happens by setting the `isTest` boolean in the HibernateConfig class: `HibernateConfig.setTest(true);`. This
is done in the `@BeforeAll` method. Then the instantiation of the DAOs will point to the testcontainer.

Make sure your test class begins like this:

```Java

private static Javalin app;
    private static final String BASE_URL = "http://localhost:7777/api/v1";
    private static HotelController hotelController;
    private static EntityManagerFactory emfTest;

    private static Hotel h1, h2;

@BeforeAll
static void beforeAll()
{
    HibernateConfig.setTest(true);
    emfTest = HibernateConfig.getEntityManagerFactory();
    hotelController = new HotelController();
    app = Javalin.create();
    ApplicationConfig.startServer(app, 7777);
}
```

Now it's time to see if the test-container and test setup works. So run the HotelControllerTest på right-clicking it and click: `Run HotelControllerTest`.

There are four main sources of errors:

1. Rename the `getEntityManagerFactoryConfig()` in the `HibernateConfig.class` to `getEntityManagerFactory()` The old version
had a `Config` too many - so we ditched it.

2. Check whether your Docker engine is running. It should.

3. You might need to reimport all dependenies in Maven, and then run the Maven -> Lifecycle goal -> Install

4. In case you are the lucky owner of a Mac M1/M2 laptop, you also need to inform Docker to use a specific ARM64 version of
postgres. In the terminal execute these 2 commands:

```console
  docker tag arm64v8/postgres:latest postgresql:15.3-alpine3.18
  sudo ln -s $HOME/.docker/run/docker.sock /var/run/docker.sock
```

Now we are ready to perform integration test. Which could be to test the DAO. But we want to test the REST endpoints first:

## 5. Stuff some test data in the database (populate)

```Java
    @BeforeEach
    void setUp()
    {
        Set<Room> calRooms = getCalRooms();
        Set<Room> batesRooms = getBatesRooms();

        try (var em = emfTest.createEntityManager())
        {
            em.getTransaction().begin();
            // Delete all rows
            em.createQuery("DELETE FROM Room r").executeUpdate();
            em.createQuery("DELETE FROM Hotel h").executeUpdate();
            // Reset sequence
            em.createNativeQuery("ALTER SEQUENCE room_room_id_seq RESTART WITH 1").executeUpdate();
            em.createNativeQuery("ALTER SEQUENCE hotel_hotel_id_seq RESTART WITH 1").executeUpdate();
            // Insert test data
            h1 = new Hotel("Hotel California", "California", Hotel.HotelType.LUXURY);
            h2 = new Hotel("Bates Motel", "Lyngby", Hotel.HotelType.STANDARD);
            h1.setRooms(calRooms);
            h2.setRooms(batesRooms);
            em.persist(h1);
            em.persist(h2);
            em.getTransaction().commit();
        }
    }

    @AfterAll
    static void tearDown()
    {
        HibernateConfig.setTest(false);
        ApplicationConfig.stopServer(app);
    }
```

At the bottom of the HotelControllerTest file. Insert these populators:

```Java
 @NotNull
    private static Set<Room> getCalRooms()
    {
        Room r100 = new Room(100, new BigDecimal(2520), Room.RoomType.SINGLE);
        Room r101 = new Room(101, new BigDecimal(2520), Room.RoomType.SINGLE);
        Room r102 = new Room(102, new BigDecimal(2520), Room.RoomType.SINGLE);
        Room r103 = new Room(103, new BigDecimal(2520), Room.RoomType.SINGLE);
        Room r104 = new Room(104, new BigDecimal(3200), Room.RoomType.DOUBLE);
        Room r105 = new Room(105, new BigDecimal(4500), Room.RoomType.SUITE);

        Room[] roomArray = {r100, r101, r102, r103, r104, r105};
        return Set.of(roomArray);
    }

    @NotNull
    private static Set<Room> getBatesRooms()
    {
        Room r111 = new Room(111, new BigDecimal(2520), Room.RoomType.SINGLE);
        Room r112 = new Room(112, new BigDecimal(2520), Room.RoomType.SINGLE);
        Room r113 = new Room(113, new BigDecimal(2520), Room.RoomType.SINGLE);
        Room r114 = new Room(114, new BigDecimal(2520), Room.RoomType.DOUBLE);
        Room r115 = new Room(115, new BigDecimal(3200), Room.RoomType.DOUBLE);
        Room r116 = new Room(116, new BigDecimal(4500), Room.RoomType.SUITE);

        Room[] roomArray = {r111, r112, r113, r114, r115, r116};
        return Set.of(roomArray);
    }
```

## 6. Use Rest Assured to perform you first REST test

Meditate on this and try it out:

```Java
@Test
    void readAll()
    {
        // Given -> When -> Then
        List<HotelDto> hotelDtoList =
                given()
                        .contentType("application/json")
                        .when()
                        .get(BASE_URL + "/hotels")
                        .then()
                        .assertThat()
                        .statusCode(HttpStatus.OK_200)  // could also just be 200
                        .extract().body().jsonPath().getList("", HotelDto.class);

        HotelDto h1DTO = new HotelDto(h1);
        HotelDto h2DTO = new HotelDto(h2);

        assertEquals(hotelDtoList.size(), 2);
        assertThat(hotelDtoList, containsInAnyOrder(h1DTO, h2DTO));
    }
```

## 7. Complete the remaining tests for the HotelController

This one we will give away for free - since it's a little complex:

```Java
@Test
    void create()
    {
        Hotel h3 = new Hotel("Cab-inn", "Østergade 2", Hotel.HotelType.BUDGET);
        Room r1 = new Room(117, new BigDecimal(4500), Room.RoomType.SINGLE);
        Room r2 = new Room(118, new BigDecimal(2300), Room.RoomType.DOUBLE);
        h3.addRoom(r1);
        h3.addRoom(r2);
        HotelDto newHotel = new HotelDto(h3);

        List<RoomDto> roomDtos =
        given()
                .contentType(ContentType.JSON)
                .body(newHotel)
                .when()
                .post(BASE_URL + "/hotels")
                .then()
                .statusCode(201)
                .body("id", equalTo(3))
                .body("hotelName", equalTo("Cab-inn"))
                .body("hotelAddress", equalTo("Østergade 2"))
                .body("hotelType", equalTo("BUDGET"))
                .body("rooms", hasSize(2))
                .extract().body().jsonPath().getList("rooms", RoomDto.class);

        assertThat(roomDtos, containsInAnyOrder(new RoomDto(r1), new RoomDto(r2)));
    }
```

## 8. Make similar tests for the RoomController endpoints

## 9. Do the integrationstest for the DAOs