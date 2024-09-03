---
title: JPA MapsId
description: MapsId annotation in JPA explained
layout: default
nav_order: 8
parent: ORM
grand_parent: Toolbox
permalink: /toolbox/java/jpa/maps-id/
---

# JPA - @MapsId explained

The `@MapsId` annotation in JPA is used to map an entity's relationship to another entity based on an embedded ID or a shared primary key. It is particularly useful when you have an entity that uses a composite primary key, and part of that composite key comes from another entity.

### How `@MapsId` Works

In the context of the example I provided earlier (with `Student`, `Course`, and `StudentCourse` entities), the `@MapsId` annotation is used to tie the foreign keys in the `StudentCourse` entity to the corresponding fields in the `StudentCourseId` composite key.

### Detailed Breakdown

#### 1. **StudentCourseId Class (Embedded Primary Key):**

```java
@Embeddable
public class StudentCourseId implements Serializable {

    private Long studentId;
    private Long courseId;

    // Default constructor, equals, and hashCode methods
}
```

- **`StudentCourseId`** is an `@Embeddable` class that defines the composite key for the `StudentCourse` entity. It contains the two fields `studentId` and `courseId`, which represent the foreign keys to the `Student` and `Course` entities, respectively.

#### 2. **StudentCourse Entity (Associative Entity):**

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

- **`@EmbeddedId`**: Indicates that the `StudentCourse` entity uses an embedded primary key of type `StudentCourseId`.
  
- **`@MapsId("studentId")`**:
  - This annotation tells JPA to map the `student` field to the `studentId` field in the `StudentCourseId` composite key.
  - The `MapsId` annotation effectively means that the `studentId` in the `StudentCourseId` composite key will be populated with the `id` from the associated `Student` entity.
  
- **`@ManyToOne`**: The `student` and `course` fields are many-to-one relationships, linking `StudentCourse` to `Student` and `Course` respectively.
  
- **`@JoinColumn(name = "student_id")`**: Specifies that the `student_id` column in the `student_course` table is the foreign key to the `Student` table.

### What Happens When `@MapsId` Is Used

1. **Shared Primary Key**:
   - The `StudentCourse` entity has a composite primary key (`StudentCourseId`), which includes `studentId` and `courseId`.
   - When you set the `student` and `course` relationships in `StudentCourse`, JPA automatically populates the corresponding fields in `StudentCourseId`.

2. **Eliminates Redundancy**:
   - Without `@MapsId`, you would need to manually manage the `StudentCourseId` fields in the `StudentCourse` entity, which would lead to redundant code and potential errors.
   - `@MapsId` simplifies this by linking the `studentId` and `courseId` fields in `StudentCourseId` directly to the primary keys of `Student` and `Course`.

3. **Integrity and Consistency**:
   - `@MapsId` ensures that the foreign keys and the composite key are always in sync. This means that the `studentId` in `StudentCourseId` is guaranteed to match the `id` of the `Student` entity associated with the `StudentCourse` entity.

### Example Usage

Let's say you want to create an `Enrollment` (which is an instance of `StudentCourse`) where `Alice` (Student ID 1) is enrolled in `Mathematics` (Course ID 101).

```java
Student alice = entityManager.find(Student.class, 1L);
Course math = entityManager.find(Course.class, 101L);

StudentCourse enrollment = new StudentCourse();
enrollment.setStudent(alice); // This automatically sets studentId in StudentCourseId
enrollment.setCourse(math);   // This automatically sets courseId in StudentCourseId

entityManager.persist(enrollment);
```

In this code:

- `enrollment.setStudent(alice)` not only sets the `student` field in `StudentCourse`, but also ensures that `studentId` in `StudentCourseId` is set to `1`.
- `enrollment.setCourse(math)` does the same for `courseId`, setting it to `101`.

### Summary

- `@MapsId` is a powerful annotation that simplifies the management of composite keys by automatically synchronizing the foreign key fields with the corresponding fields in an embedded ID class.
- It ensures that the relationship between entities is consistent and that the composite key is correctly populated based on the associated entities' primary keys.
- This approach is particularly useful in many-to-many relationships with composite keys in the join table.
