# Testcontainer setup

Get an [overview of test scenarios](../flow3/2_security/understanding_the_test_setup.md) here.

This repository holds an example code base of setting up test-containers for tests: [https://github.com/dat3Cph/3sem-javalin-rest-api](https://github.com/dat3Cph/3sem-javalin-rest-api). Explanations and 'how-to' will follow below:

You will need to go through these three steps to prepare for using test-containers:

1. Prepare your `pom.xml` with properties and extra test-container dependencies.
2. Add a util method called getProperty(String propName) in the ApplicationConfig class. This method will make it
possible to read properties from the pom.xml file. This is handy to feed in values to the Hibernate setup. Like `db.name`, `db.username`, and `db.password`.
3. Modify / overwrite the HibernateConfig file. The new version will provide a boolean ´isTest´ attribute, that can signal whether
the connectionpool should be hooked onto the real database (normal situation) - or be using the test-containers and a test database.

Code-snippets are provided below:

## 1. Prepare your `pom.xml`

First, add these dependencies:

```Java
<!--  TESTING      -->

        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-api</artifactId>
            <version>5.10.0</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-engine</artifactId>
            <version>5.10.0</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter-params</artifactId>
            <version>5.10.0</version>
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
            <version>1.18.0</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.testcontainers</groupId>
            <artifactId>postgresql</artifactId>
            <version>1.18.0</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.testcontainers</groupId>
            <artifactId>jdbc</artifactId>
            <version>1.18.0</version>
        </dependency>
        <dependency>
            <groupId>org.testcontainers</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>1.18.0</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>io.rest-assured</groupId>
            <artifactId>rest-assured</artifactId>
            <version>5.3.2</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>io.rest-assured</groupId>
            <artifactId>json-schema-validator</artifactId>
            <version>5.3.2</version>
            <scope>test</scope>
        </dependency>
```

## 2. Add a util method called getProperty(String propName)

Add this method to the ApplicationConfig class:

```Java
public static String getProperty(String propName) throws IOException {
        try (InputStream is = HibernateConfig.class.getClassLoader().getResourceAsStream("properties-from-pom.properties")) {
            Properties prop = new Properties();
            prop.load(is);
            return prop.getProperty(propName);
        } catch (IOException ex) {
            ex.printStackTrace();
            throw new IOException("Could not read property from pom file");
        }
    }
```

## 3. Prepare HibernateConfig.java

Use and modify this version of the HibernateConfig.java file. This will add a boolean `isTest` attribute, which
can be used for indication that `getEntityManagerFactory()` should return a factory that holds connections to
a test container with a Postgres Database.

```Java

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
        configuration.addAnnotatedClass(Person.class);
        configuration.addAnnotatedClass(User.class);
        configuration.addAnnotatedClass(Role.class);
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

## Setup your test class for the test EntityManagerFactory

The tricks happens by setting the `isTest` boolean in the HibernateConfig class: `HibernateConfig.setTest(true);`. This
is done in the `@BeforeAll` method. Then the instantiation of the DAOs will point to the testcontainer.

```Java
class PersonDAOTest {

    private static PersonDAO personDAO;
    private static EntityManagerFactory emfTest;

    private int[] IDS; //
     
    @BeforeEach
    void setUp() {
        IDS = TestData.createPersonTestData(emfTest);
    }

    @BeforeAll
    static void setUpAll() {
        HibernateConfig.setTest(true);
        emfTest = HibernateConfig.getEntityManagerFactory();
        personDAO = PersonDAO.getInstance(emfTest);
    }

    @AfterAll
    static void tearDownAll() {
        HibernateConfig.setTest(false);
    }

    // .......
```
