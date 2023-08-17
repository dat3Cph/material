# Day 1 - JPA Introduction

## 1. How to create a simple Maven project with JUnit 5, Hibernate, PostgresSQL and Lombok.

1. Open IntelliJ and create a new project.
2. Select Maven and Java 17.
3. In advanced settings, add groupId.
4. Click finish.

---

</br>
<img src="./images/intellij_setup_1.png" width="600" height="500">

</br>

5. Open the pom.xml file and add the following dependencies: [Link](https://gist.github.com/tysker/33f364970e366ba1d2daf96d034abea6)

- JUnit 5
- Hibernate
- PostgresSQL
- Lombok

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


1. Copy and paste the following gist into the file: [Link](https://gist.github.com/tysker/cdf831680b964aa8dedd5545079e43b2)

</br>

**If you get an import error, try to run Maven lifecycle "install"**

---

</br>
<img src="./images/maven_lifecycle_3.png">

</br>

---
