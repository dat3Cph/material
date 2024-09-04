---
title: JPA Annotations
description: crud examples 
layout: default
nav_order: 2
parent: ORM
grand_parent: Toolbox
permalink: /toolbox/java/jpa/annotations/
---

# JPA - Annotations explained in brief

Below is a list of some of the most common JPA (Java Persistence API) annotations along with brief explanations of each:

### 1. **@Entity**

- **Purpose**: Marks a class as a JPA entity, which means it will be mapped to a database table.
- **Example**: `@Entity public class Employee { ... }`

### 2. **@Table**

- **Purpose**: Specifies the name of the database table to which the entity is mapped. If not provided, the class name is used as the table name.

- **Example**: `@Table(name = "employees")`

### 3. **@Id**

- **Purpose**: Marks a field as the primary key of the entity.

- **Example**: `@Id private Long id;`

### 4. **@GeneratedValue**

- **Purpose**: Specifies that the primary key should be automatically generated. Often used with strategies like `AUTO`, `IDENTITY`, `SEQUENCE`, or `TABLE`.

- **Example**: `@GeneratedValue(strategy = GenerationType.IDENTITY)`

### 5. **@Column**

- **Purpose**: Specifies the details of the column to which a field is mapped, such as the column name, length, and nullability.

- **Example**: `@Column(name = "first_name", nullable = false, length = 50)`

### 6. **@OneToOne**

- **Purpose**: Defines a one-to-one relationship between two entities.

- **Example**: `@OneToOne @JoinColumn(name = "passport_id") private Passport passport;`

### 7. **@OneToMany**

- **Purpose**: Defines a one-to-many relationship between two entities. Typically, the one side references a collection of the many side.

- **Example**: `@OneToMany(mappedBy = "department") private List<Employee> employees;`

### 8. **@ManyToOne**

- **Purpose**: Defines a many-to-one relationship between two entities. Typically, the many side holds the foreign key to the one side.

- **Example**: `@ManyToOne @JoinColumn(name = "department_id") private Department department;`

### 9. **@ManyToMany**

- **Purpose**: Defines a many-to-many relationship between two entities, often managed via a join table.

- **Example**:

```java
@ManyToMany @JoinTable(name = "student_course", joinColumns = @JoinColumn(name = "student_id"), inverseJoinColumns = @JoinColumn(name = "course_id")) private List<Course> courses;
```

### 10. **@JoinColumn**

- **Purpose**: Specifies the foreign key column used in the relationship between two entities.

- **Example**: `@JoinColumn(name = "department_id")`

### 11. **@JoinTable**

- **Purpose**: Specifies the join table that is used in a many-to-many relationship. It defines both the foreign keys to the two entities.

- **Example**:

    ```java
    @JoinTable(name = "student_course", joinColumns = @JoinColumn(name = "student_id"), inverseJoinColumns = @JoinColumn(name = "course_id"))
    ```

### 12. **@Embedded**

- **Purpose**: Embeds an embeddable class into an entity. This is used for classes that do not have an identity of their own but are part of another entity.

- **Example**: `@Embedded private Address address;`

### 13. **@Embeddable**

- **Purpose**: Marks a class as embeddable, meaning it can be embedded in another entity using the `@Embedded` annotation.

- **Example**: `@Embeddable public class Address { ... }`

### 14. **@EmbeddedId**

- **Purpose**: Marks a field as an embedded primary key. This is used for composite keys where the key is composed of multiple fields.

- **Example**: `@EmbeddedId private StudentCourseId id;`

### 15. **@MapsId**

- **Purpose**: Used in conjunction with `@IdClass` or `@EmbeddedId` to map a relationship’s foreign key to a part of the entity's primary key.

- **Example**:

    ```java
    @ManyToOne @MapsId("studentId") @JoinColumn(name = "student_id") private Student student;
    ```

### 16. **@Enumerated**

- **Purpose**: Specifies that a field should be persisted as an enumeration. Can specify either `EnumType.ORDINAL` (default) or `EnumType.STRING`.

- **Example**: `@Enumerated(EnumType.STRING) private Status status;`

### 17. **@Temporal**

- **Purpose**: Specifies the temporal type of a date field (e.g., `DATE`, `TIME`, `TIMESTAMP`).

- **Example**: `@Temporal(TemporalType.DATE) private Date birthDate;`

### 18. **@Lob**

- **Purpose**: Marks a field as a large object (LOB) for storing large amounts of data, such as text or binary data.

- **Example**: `@Lob private String description;`

### 19. **@Transient**

- **Purpose**: Marks a field as not being persisted to the database. This field will be ignored by JPA.

- **Example**: `@Transient private int tempCalculation;`

### 20. **@Version**

- **Purpose**: Marks a field as the version field for optimistic locking, which is used to detect concurrent modifications.

- **Example**: `@Version private Long version;`

### 21. **@Inheritance**

- **Purpose**: Specifies the inheritance strategy for entities in a hierarchy. Common strategies include `SINGLE_TABLE`, `JOINED`, and `TABLE_PER_CLASS`.

- **Example**: `@Inheritance(strategy = InheritanceType.JOINED)`

### 22. **@DiscriminatorColumn**

- **Purpose**: Specifies the column used to differentiate between entities in a single table inheritance hierarchy.

- **Example**: `@DiscriminatorColumn(name = "type")`

### 23. **@NamedQuery**

- **Purpose**: Defines a static, named query that can be called by its name later in the code. Often used for complex or frequently used queries.

- **Example**:

    ```java
    @NamedQuery(name = "Employee.findByName", query = "SELECT e FROM Employee e WHERE e.name = :name")
    ```

### 24. **@Cacheable**

- **Purpose**: Marks an entity as cacheable, meaning it can be cached by the second-level cache.

- **Example**: `@Cacheable(true)`

### 25. **@SqlResultSetMapping**

- **Purpose**: Maps the result of a native SQL query to an entity or a set of entities.

- **Example**:

    ```java
    @SqlResultSetMapping(name = "EmployeeMapping", entities = @EntityResult(entityClass = Employee.class))
    ```

These annotations are fundamental to working with JPA and allow you to map Java objects to relational database tables, manage relationships between entities, and define query strategies and more.
