---
title: School Exercise
description: school exercise
layout: default
nav_order: 1
parent: Exercises
grand_parent: JPA Part 2
permalink: part2/exercises/school/
---

# School Exercise (JPQL)

### 1. Set up the data model as shown in the diagram below.

![School ERD](../../images/school_eer_model.png)

### 2. Using JPQL to find solutions to the following challenges:

#### Part 1:

1. Create a ´Populate` class with a main method. In the main method create a method that can populate the database with data.

#### Part 2:

2. Create a `dao` package and add a new interface called `StudentDAO` and add the following code to the interface:

```java
public interface IStudentDAO {
    // find all students in the system with the first name Anders
    List<Student> findAllStudentsByFirstName(String firstName);

    // find all students in the system with the last name And
    List<Student> findAllStudentsByLastName(String lastName);

    // find the total number of students, for a semester given the semester name as a parameter
    long findTotalNumberOfStudentsBySemester(String semesterName);

    // find the total number of students that has a particular teacher
    long findTotalNumberOfStudentsByTeacher(Teacher teacher);

    // find the teacher who teaches the most semesters
    Teacher findTeacherWithMostSemesters();

    // find the semester that has the fewest students
    Semester findSemesterWithFewestStudents();

    // find all students, encapsulated as StudentInfo
    StudentInfo getAllStudentInfo(int id);
}
```

3. At the same location add a new class called `StudentDAOImpl` and implement the interface to the class with all the methods.

4. In the root of the project add a new class called `Populate` and add the following code to the class:

```java
public class Populate {
    public static void main(String[] args) {
        EntityManagerFactory emf = HibernateConfig.getEntityManagerFactoryConfig();
        EntityManager em = emf.createEntityManager();

        try {
            em.getTransaction().begin();
            // populate the database with data
            em.getTransaction().commit();
        } finally {
            em.close();
        }
    }
}
```

5. Run the `main` method in the Populate class to populate the database with the students, teachers, and semesters.

6. All the methods in the `StudentDAOImpl` class should now be implemented using JPQL.

#### Part 3:

1. Create a StudentInfo class with the following properties:
   - `fullName`
   - `studentId`
   - `thisSemesterName`
   - `thisSemesterDescription`
2. Add a public constructor that takes all the necessary arguments to initialize the properties.
3. Now create a method (using JPQL) with the following signature to return a list of all Students, encapsulated as StudentInfo.
   - `public StudentInfo getAllStudentInfo(int id)`

PS. Add the getAllStudentInfo method to the StudentDAO interface and implement it in the StudentDAOImpl class.

### Part 4:

1. Create a test class with a test method for each of the methods in the `StudentDAOImpl` class.

2. Run the test class and verify that all tests pass.

**Good luck!**

