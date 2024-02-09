# JPA Lifecycle and Annotations

## Objective: 

**Apply JPA annotations to map Java classes to database tables and understand entity lifecycle.**

1. Create a new Java project using Maven.
2. Define a simple entity class called "Student" with attributes like `id`, `firstName`, `lastName`, `email` and `age`. Remember to include a no-arg constructor.
3. Use JPA annotations to map the entity class to a database table named `students`.
4. Add a constraint to the `email` attribute to ensure that the email address is unique.
5. Include appropriate annotations such as `@Entity`, `@Table`, `@Id`, `@GeneratedValue`, and `@Column` to define the primary key and attributes mapping.
5. Add a `Main.class` including a main method 
6. Create the following methods and add it to the Main class:
   - `public static void createStudent(Student student)` - This method should create a new student and persist it to the database.
   - `public static Student readStudent(int id)` - This method should read a student from the database using the student's id.
   - `public static Student updateStudent(Student updStd)` - This method should update an existing student in the database.
   - `public static void deleteStudent(int id)` - This method should delete a student from the database using the student's id.
   - `public static List<Student> readAllStudents()` - This method should retrieve all students from the database and return them as a list. Use a `TypedQuery` to retrieve all students. 
   - In all the methods above, remember to open and close the `EntityManager` and `EntityManagerFactory` objects.
   - You can use either the `try-with-resources` or the `finally` block to close the objects.
7. In all the methods above, write small comments that explains when an object is transient, detached, removed or managed. (See example below)

```JAVA
    public static void main(String[] args) {
    // entity is in transient state
    Student student = new Student("Michelle", "Schmidt", "schmidt@mail.com", 30);

    }
    
    public static void createStudent(Student student) {
        try(EntityManager em = emf.createEntityManager()) {
            em.getTransaction().begin();
            // entity is in managed state (after persist)
            em.persist(student);
            // entity is in detached state after the transaction is committed
            em.getTransaction().commit();
        }
    }
```

8. Create a method in the Student class that verifies that the email address is valid. The method should return a boolean value. 
9. Add a `@PrePersist` method to the Student class that verifies that the email address is valid. If the email address is not valid, throw an exception. 
10. Do the same as in step 9, but this time use a `@PreUpdate` method. 
11. Create a test class with a test method for each of the methods in the Main class. 
12. Run the test class and verify that all tests pass. 
13. Create 10 students and persist them to the database. 
    - 3 of the students should have the last name "Hansen" and 4 should have the last name "Jensen".
    - 1 of the students should be the oldest with an age of 90.
    - 1 of the students should be the youngest with an age of 10. 
14. Get the `average` age of all students in the database. 
15. Get the `average` age of all students in the database whose last name is "Hansen".
16. `count` the number of students in the database whose last name is "Jensen". 
17. Get the first name of the oldest student in the database. 
18. Get the youngest student in the database. 
19. Get the `sum` of all ages of all students in the database.