---
title: JPA Many-To-Many extra
description: Many to Many relationship in JPA with extra attributes
layout: default
nav_order: 8
parent: ORM
grand_parent: Toolbox
permalink: /toolbox/java/jpa/many-to-many-extra/
---

# JPA - Many-To-Many associations with extra attributes in join table explained

In JPA, when you have a many-to-many relationship where the link (join) table has extra attributes, this is typically handled by creating an additional entity to represent the join table. This is often referred to as an *associative entity* or *junction entity*.

### Example Scenario

Let's say we have `Student` and `Course` entities, and we want to track the date when a student enrolled in a course. The `Enrollment` table (the link table) will have additional attributes such as `enrollmentDate`.

### Steps to Implement

1. **Create an Associative Entity**:
   - Create a new entity class to represent the join table, which will include the additional attributes along with the foreign keys.

2. **Map the Relationships**:
   - Define two `@ManyToOne` relationships in the associative entity to represent the links back to the original entities.
   - In the original entities (`Student` and `Course`), define a `@OneToMany` relationship pointing to the associative entity.

### Entity Classes

#### **Student Entity**

```java
@Entity
public class Student {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @OneToMany(mappedBy = "student", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<Enrollment> enrollments = new ArrayList<>();

    // Getters and setters
}
```

#### **Course Entity**

```java
@Entity
public class Course {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String title;

    @OneToMany(mappedBy = "course", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<Enrollment> enrollments = new ArrayList<>();

    // Getters and setters
}
```

#### **Enrollment Entity (Associative Entity)**

```java
@Entity
public class Enrollment {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToOne
    @JoinColumn(name = "student_id")
    private Student student;

    @ManyToOne
    @JoinColumn(name = "course_id")
    private Course course;

    private LocalDate enrollmentDate;

    // Getters and setters
}
```

### Explanation

1. **Enrollment Entity**:
   - **Fields**:
     - `student`: A many-to-one relationship with the `Student` entity.
     - `course`: A many-to-one relationship with the `Course` entity.
     - `enrollmentDate`: An additional attribute to store the date of enrollment.
   - The `Enrollment` entity serves as the link between `Student` and `Course`, holding the extra data (`enrollmentDate`) that can't be captured by the standard many-to-many relationship.

2. **Student and Course Entities**:
   - Both `Student` and `Course` entities have a one-to-many relationship with the `Enrollment` entity, representing the fact that each student can have multiple enrollments and each course can be associated with multiple enrollments.

### Database Structure

#### **Student Table**

| Column Name | Data Type    | Constraints                  |
|-------------|--------------|------------------------------|
| id          | BIGINT       | PRIMARY KEY, AUTO_INCREMENT  |
| name        | VARCHAR      | NOT NULL                     |

#### **Course Table**

| Column Name | Data Type    | Constraints                  |
|-------------|--------------|------------------------------|
| id          | BIGINT       | PRIMARY KEY, AUTO_INCREMENT  |
| title       | VARCHAR      | NOT NULL                     |

#### **Enrollment Table (Link Table with Extra Attributes)**

| Column Name     | Data Type    | Constraints                          |
|-----------------|--------------|--------------------------------------|
| id              | BIGINT       | PRIMARY KEY, AUTO_INCREMENT          |
| student_id      | BIGINT       | FOREIGN KEY REFERENCES Student(id)   |
| course_id       | BIGINT       | FOREIGN KEY REFERENCES Course(id)    |
| enrollmentDate  | DATE         | NOT NULL                             |

- **`id`**: Primary key for the `Enrollment` table.
- **`student_id`**: A foreign key referencing the `id` column in the `Student` table.
- **`course_id`**: A foreign key referencing the `id` column in the `Course` table.
- **`enrollmentDate`**: An additional column to store the date when a student enrolled in a course.

### Example of Table Content

Assume we have the following data:

- **Students**:
  - { id: 1, name: "Alice" }
  - { id: 2, name: "Bob" }
- **Courses**:
  - { id: 101, title: "Mathematics" }
  - { id: 102, title: "Physics" }
- **Enrollments**:
  - { id: 1, student_id: 1, course_id: 101, enrollmentDate: '2023-09-01' }
  - { id: 2, student_id: 1, course_id: 102, enrollmentDate: '2023-09-02' }
  - { id: 3, student_id: 2, course_id: 101, enrollmentDate: '2023-09-03' }

#### **Enrollment Table**

| id  | student_id | course_id | enrollmentDate |
|-----|------------|-----------|----------------|
| 1   | 1          | 101       | 2023-09-01     |
| 2   | 1          | 102       | 2023-09-02     |
| 3   | 2          | 101       | 2023-09-03     |

### How They Work Together

- The `Enrollment` table not only links `Student` and `Course` but also stores additional information (`enrollmentDate`), making it more flexible than a simple join table.
- This approach allows you to model complex many-to-many relationships with additional attributes effectively.

### Use Cases

- This pattern is useful in scenarios where the relationship between two entities has its own attributes, such as:
  - Students enrolling in courses with a specific date.
  - Employees assigned to projects with a specific role and start date.
  - Users liking posts with a timestamp.

This design is crucial for handling real-world scenarios where relationships carry additional data beyond just the association itself.

## Same example with a different approach (more complicated but more flexible)

Certainly! When you have a true many-to-many relationship with an embedded primary key in the join table, you can use an embedded ID class to represent the composite primary key. This approach is useful when the join table has no extra attributes beyond the foreign keys but still needs to represent a composite key.

### Example Scenario

Let's continue with the `Student` and `Course` example. In this case, we'll represent the many-to-many relationship using a join table with an embedded primary key, which consists of the foreign keys from both entities.

### Steps to Implement

1. **Create an Embedded ID Class**:
   - This class will represent the composite key of the join table. It will contain the two foreign keys (`student_id` and `course_id`).

2. **Create an Associative Entity**:
   - This entity will represent the join table and use the embedded ID class as its primary key.

3. **Map the Relationships**:
   - In both `Student` and `Course` entities, define a `@ManyToMany` relationship that maps to the associative entity.

### Entity Classes

#### **Student Entity**

```java
@Entity
public class Student {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @ManyToMany
    @JoinTable(
        name = "student_course",
        joinColumns = @JoinColumn(name = "student_id"),
        inverseJoinColumns = @JoinColumn(name = "course_id")
    )
    private List<Course> courses = new ArrayList<>();

    // Getters and setters
}
```

#### **Course Entity**

```java
@Entity
public class Course {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String title;

    @ManyToMany(mappedBy = "courses")
    private List<Student> students = new ArrayList<>();

    // Getters and setters
}
```

#### **StudentCourseId Class (Embedded Primary Key)**

```java
@Embeddable
public class StudentCourseId implements Serializable {

    private Long studentId;
    private Long courseId;

    // Default constructor, equals, and hashCode methods
}
```

#### **StudentCourse Entity (Associative Entity)**

```java
@Entity
@Table(name = "student_course")
public class StudentCourse {

    @EmbeddedId
    private StudentCourseId id;

    @ManyToOne
    @MapsId("studentId")
    @JoinColumn(name = "student_id")
    private Student student;

    @ManyToOne
    @MapsId("courseId")
    @JoinColumn(name = "course_id")
    private Course course;

    // Default constructor, getters, and setters
}
```

### Explanation

1. **StudentCourseId Class**:
   - This is an `@Embeddable` class representing the composite key in the join table. It contains two fields: `studentId` and `courseId`, which correspond to the foreign keys in the join table.

2. **StudentCourse Entity**:
   - **`@EmbeddedId`**: Specifies that this entity uses an embedded primary key.
   - **`@MapsId`**: Maps the foreign keys to the fields in the embedded ID class. This ensures that the `studentId` and `courseId` fields in `StudentCourseId` are automatically populated based on the related `Student` and `Course` entities.
   - This entity is essentially a representation of the join table, and it directly ties `Student` and `Course` together with a composite key.

3. **Student and Course Entities**:
   - These entities define a many-to-many relationship and reference the `StudentCourse` entity through the `@JoinTable` annotation.

### Database Structure

#### **Student Table**

| Column Name | Data Type    | Constraints                  |
|-------------|--------------|------------------------------|
| id          | BIGINT       | PRIMARY KEY, AUTO_INCREMENT  |
| name        | VARCHAR      | NOT NULL                     |

#### **Course Table**

| Column Name | Data Type    | Constraints                  |
|-------------|--------------|------------------------------|
| id          | BIGINT       | PRIMARY KEY, AUTO_INCREMENT  |
| title       | VARCHAR      | NOT NULL                     |

#### **StudentCourse Table (Join Table with Embedded Primary Key)**

| Column Name | Data Type    | Constraints                  |
|-------------|--------------|------------------------------|
| student_id  | BIGINT       | FOREIGN KEY, PRIMARY KEY     |
| course_id   | BIGINT       | FOREIGN KEY, PRIMARY KEY     |

- **`student_id`**: A foreign key referencing the `id` column in the `Student` table. It is also part of the composite primary key.
- **`course_id`**: A foreign key referencing the `id` column in the `Course` table. It is also part of the composite primary key.

### Example of Table Content

Assume we have the following data:

- **Students**:
  - { id: 1, name: "Alice" }
  - { id: 2, name: "Bob" }
- **Courses**:
  - { id: 101, title: "Mathematics" }
  - { id: 102, title: "Physics" }

#### **StudentCourse Table**

| student_id | course_id |
|------------|-----------|
| 1          | 101       |
| 1          | 102       |
| 2          | 101       |

### How They Work Together

- The `StudentCourse` table links students and courses together using a composite key that consists of the `student_id` and `course_id`.
- This setup allows each `Student` to be associated with multiple `Course` records and each `Course` to be associated with multiple `Student` records, while the composite primary key ensures that each student-course pair is unique.

### Use Cases

- This pattern is used in many scenarios where the relationship itself doesn't need extra attributes, but the integrity of the composite key must be maintained, such as:
  - Authors and books (where an author can write multiple books and a book can have multiple authors).
  - Employees and projects (where an employee can be part of multiple projects and a project can have multiple employees).

This approach ensures that the many-to-many relationship is properly represented in the database, with a composite key enforcing uniqueness of the association.
