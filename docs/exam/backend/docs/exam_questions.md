---
title: Exam questions backend
description: Selected Learning Goals for the Backend exam
layout: default
nav_order: 8
parent: Backend
grand_parent: Exam
permalink: /exam/backend/questions
---

# Exam questions backend exam 2024

These are handpicked among our learning goals for the backend exam. They are meant to give you an idea of what to expect in the exam, and give you something to practice on. They are theoretical questions, but think about them in the context of your own code, and projects you have done during the semester.

1. **What is a REST API, and why is it commonly used in web development?**

    - What does ReST stand for?
    - What are the main principles of RESTful architecture?
    - What are semantic URLs, and how do they improve the readability of RESTful APIs?

2. **Explain the purpose of using DTO (Data Transfer Object) classes in a java application:**

    - Where are DTO classes typically used in the context of RESTful APIs?
    - How can DTO classes help in decoupling the domain model from the API response?
    - Should DTO classes import domain model classes? Why or why not?

3. **What is the difference between HTTP GET, POST, PUT, and DELETE methods? Provide examples for each:**

    - How are these HTTP methods typically used in RESTful API design?
    - What are the main differences between PUT and POST methods in terms of idempotency and safety?
    - How can the PATCH method be used to update resources in a RESTful API?
    - What is the purpose of the OPTIONS method in HTTP?

4. **What is error handling in REST APIs, and why is it important?**

    - How can HTTP status codes be used to communicate errors in a RESTful API?
    - What are some common error codes and their meanings in the context of RESTful APIs?
    - How can custom error messages be returned in a RESTful API response?

5. **Describe how JSON is typically used in RESTful APIs for data exchange**

    - What are the advantages of using JSON over other data formats like XML?
    - How can JSON be serialized and deserialized in Java using libraries like Jackson?
    - What is the purpose of the Content-Type header in an HTTP request or response?

6. **What is logging in the context of application development, and how can it improve error management and debugging?**

    - How can logging be implemented in a Java application using libraries like Logback?
    - What are the different log levels, and when should they be used in an application?
    - How can log messages be formatted to include relevant information like timestamps and log levels?

7. **Explain the concept of dependency injection and its benefits in creating scalable applications.**

    - Where do you use dependency injection in your application?
    - What is the alternative to dependency injection?
    - How does dependency injection help in your code?

8. **How do streams and lambda expressions work in Java, and how can they help in processing collections?**

9. **Show an example of using streams and lambda expressions to filter, map, and reduce elements in a collection.**

    - What are the advantages of using streams and lambda expressions over traditional iteration methods?
    - Show examples of grouping elements in a collection using streams and lambda expressions.

10. **What are Java Generics, and why are they used? Provide an example of a generic class or interface.**

    - How can generics help in creating reusable and type-safe code?
    - Why do we want to use interface data types over concrete data types?
    - How can you restrict the types that can be used with a generic class or method?

11. **Explain the role of JPA (Java Persistence API) in Java applications and how it manages data persistence.**

12. **What are Hibernate and EntityManagerFactory, and how do they facilitate ORM (Object-Relational Mapping) in Java?**

    - What is the purpose of the HibernateConfig file in your application?
    - What is a DAO (Data Access Object), and how does it fit into the design of a backend service?

13. **What is the purpose of some common JPA annotations**

    - What is the purpose of using annotations like @Entity, @Table, and @Column in JPA entities?
    - What is the difference between FetchType.LAZY and FetchType.EAGER in JPA entity relationships?
    - What is the purpose of the @Id and @GeneratedValue annotations in JPA entity classes?

14. **Describe the One-to-Many relationship in a database and how it can be represented using JPA annotations.**

    - What is the difference between unidirectional and bidirectional relationships in JPA entities?
    - How can cascading operations be used to maintain consistency in a One-to-Many relationship?
    - What are some common pitfalls to avoid when working with cascading operations in JPA entities?

15. **Explain how external APIs can be integrated into an application and some considerations when calling these APIs.**

    - What are RESTful APIs, and how can they be consumed in a Java application?
    - How can you handle authentication when calling external APIs?
    - How can we best consume JSON data from an external API in a Java application?

16. **What is JWT (JSON Web Token), and how does it enhance security in RESTful applications?**

    - How can JWT be used for authentication and authorization in a RESTful API?
    - What are the main components of a JWT token, and how are they used for secure communication?
    - How can JWT tokens be validated and decoded in a Java application?

17. **How does role-based access control work, and how can it be applied to secure REST API endpoints?**

    - Show in your code how you can restrict access to certain endpoints based on user roles.
    - How are the user roles from the token used to determine access rights in your application?

18. **Describe the differences between integration testing and unit testing in the context of REST API endpoints.**

    - What is RestAssured, and how can it be used to test RESTful APIs in Java?
    - How can you test access control and error handling in your RESTful API using integration tests?
    - How does Hamcrest help in writing expressive assertions in your test cases?

19. **Give an overview of how we deploy our backend applications to the cloud**

    - What is CI/CD?
    - How are we using GitHub Actions to automate the deployment of your application?
    - What is Docker Hub?
    - How can we use Docker Compose to manage multi-container applications?
    - How do we re-deploy our application when we have made changes to our code?
