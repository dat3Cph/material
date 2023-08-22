## How to create a basic Maven project with JUnit 5, Hibernate, PostgresSQL and Lombok.

1. Open IntelliJ and create a new project.
2. Select Maven and Java 17.
3. In advanced settings, add groupId.
4. Click finish.

---

</br>
<img src="./images/intellij_setup_1.png" width="600" height="500">

</br>

5. Open the pom.xml file and add the following dependencies:

```XML
 <dependencies>
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

        <!--  LOMBOK    -->

        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.28</version>
            <scope>provided</scope>
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
</dependencies>

```

---

6. Add the following lines into the properties tag

```xml

    <hibernate-version>6.2.4.Final</hibernate-version>
    <junit.version>5.9.1</junit.version>

```

---

7. Create a new java class file called HibernateConfig.

</br>
<img src="./images/hibernateconfig_2.png">
</br>

1. Copy and paste the following [Link](https://gist.github.com/tysker/cdf831680b964aa8dedd5545079e43b2) into the HibernateConfig.class.

</br>

**If you get an import error, try to run Maven lifecycle "install"**

---

</br>
<img src="./images/maven_lifecycle_3.png">

</br>

---
