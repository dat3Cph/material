---
title: JPA CRUD Examples
description: crud examples 
layout: default
nav_order: 4
parent: ORM
grand_parent: Toolbox
permalink: /toolbox/java/jpa/crud/
---

# These are CRUD examples prompted from ChatGpt and modified to our setup with Hibernate

- [Create (persist)](#persist)
- [Read (select)](#selecting-books)
- [Update](#update)
- [Delete (remove)](#delete--remove)

## Update

**Prompt: Show a java method that implements an update in jpa and use a Book entity?**

Certainly! Below is a simple example of a JPA update operation using a `Book` entity. In this example, the `Book` entity class is annotated with JPA annotations to map it to a database table. The `updateBook` method performs an update operation.

### Book Entity

```java
import jakarta.persistence.*;

@Entity
public class Book {
    @Id
    private Long id;
    private String title;
    private String author;

    // Getters and setters
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getAuthor() {
        return author;
    }

    public void setAuthor(String author) {
        this.author = author;
    }
}
```

### Update Method using JPA

```java
import jakarta.persistence.*;

public class BookRepository {

    private EntityManagerFactory emf = HibernateConfig.getEntityManagerFactoryConfig();

    public void updateBook(Long id, String newTitle, String newAuthor) {
        EntityManager entityManager = entityManagerFactory.createEntityManager();

        // Begin transaction
        entityManager.getTransaction().begin();

        // Find the book by its ID
        Book book = entityManager.find(Book.class, id);

        // Update book details
        if (book != null) {
            book.setTitle(newTitle);
            book.setAuthor(newAuthor);
        }

        // Commit transaction
        entityManager.getTransaction().commit();

        // Close the EntityManager
        entityManager.close();
    }
}
```

In this example:

- The `Book` class represents the entity, and it maps to a table in the database.
- The `BookRepository` class has a method named `updateBook` which takes a `Long id`, a `String newTitle`, and a `String newAuthor` as parameters.
- An `EntityManager` is used to manage the JPA operations. The `find` method retrieves the `Book` entity object from the database.
- The `setTitle` and `setAuthor` methods update the `Book` entity object.
- Finally, the transaction is committed with `entityManager.getTransaction().commit()`.

Note: This is a simplified example to demonstrate the update operation in JPA. Error handling, logging, and other concerns are not covered. Always close the `EntityManager` and `EntityManagerFactory` in a real-world application, possibly using try-with-resources or try-finally blocks.

## Persist

**Prompt: show a similar method for persisting a book**

Certainly! Below is an additional method named `addBook` in the `BookRepository` class for persisting a `Book` entity to the database.

### Book Entity (for reference)

```java
import jakarta.persistence.*;

@Entity
public class Book {
    @Id
    private Long id;
    private String title;
    private String author;

    // Getters and setters (same as previous example)
    // ...
}
```

### Method for Persisting a Book

```java
import jakarta.persistence.*;

public class BookRepository {

    private EntityManagerFactory emf = HibernateConfig.getEntityManagerFactoryConfig();

    public void addBook(Long id, String title, String author) {

        EntityManager entityManager = entityManagerFactory.createEntityManager();

        // Create a new Book object
        Book newBook = new Book();
        newBook.setId(id);
        newBook.setTitle(title);
        newBook.setAuthor(author);

        // Begin transaction
        entityManager.getTransaction().begin();

        // Persist the Book object to the database
        entityManager.persist(newBook);

        // Commit transaction
        entityManager.getTransaction().commit();

        // Close the EntityManager
        entityManager.close();
    }

    // Other methods like updateBook (same as previous example)
    // ...
}
```

### Explanation

- The `addBook` method accepts an `id`, `title`, and `author` as parameters.
- It then creates a new `Book` entity object and sets its fields.
- The `EntityManager` starts a transaction with `entityManager.getTransaction().begin()`.
- The `persist` method is used to add the `Book` entity object to the database.
- Finally, the transaction is committed with `entityManager.getTransaction().commit()`.

This is a basic example to demonstrate how you might persist a `Book` entity using JPA. Note that error handling, logging, and other concerns have been omitted for the sake of simplicity. In a real-world application, you'd typically include those as well.

## Delete / Remove

**Prompt: create a similar example for remove**

Certainly! Below is an additional method named `addBook` in the `BookRepository` class for persisting a `Book` entity to the database.

### Book Entity (for reference)

```java
import jakarta.persistence.*;

@Entity
public class Book {
    @Id
    private Long id;
    private String title;
    private String author;

    // Getters and setters (same as previous example)
    // ...
}
```

### Method for Persisting a Book

```java
import jakarta.persistence.*;

public class BookRepository {

    EntityManager entityManager = entityManagerFactory.createEntityManager();

    public void addBook(Long id, String title, String author) {
        EntityManager entityManager = entityManagerFactory.createEntityManager();

        // Create a new Book object
        Book newBook = new Book();
        newBook.setId(id);
        newBook.setTitle(title);
        newBook.setAuthor(author);

        // Begin transaction
        entityManager.getTransaction().begin();

        // Persist the Book object to the database
        entityManager.persist(newBook);

        // Commit transaction
        entityManager.getTransaction().commit();

        // Close the EntityManager
        entityManager.close();
    }

    // Other methods like updateBook (same as previous example)
    // ...
}
```

### Explanation

- The `addBook` method accepts an `id`, `title`, and `author` as parameters.
- It then creates a new `Book` entity object and sets its fields.
- The `EntityManager` starts a transaction with `entityManager.getTransaction().begin()`.
- The `persist` method is used to add the `Book` entity object to the database.
- Finally, the transaction is committed with `entityManager.getTransaction().commit()`.

This is a basic example to demonstrate how you might persist a `Book` entity using JPA. Note that error handling, logging, and other concerns have been omitted for the sake of simplicity. In a real-world application, you'd typically include those as well.

## Selecting books

**show a similar method for selecting all books written by "Haruki Murakami"**

Certainly! You can use the JPA Query Language (JPQL) to select all books written by a specific author, such as "Haruki Murakami". Below is an additional method named `findAllBooksByAuthor` in the `BookRepository` class for this purpose.

### Book Entity (for reference)

```java
import jakarta.persistence.*;

@Entity
public class Book {
    @Id
    private Long id;
    private String title;
    private String author;

    // Getters and setters (same as previous examples)
    // ...
}
```

### Method for Finding All Books by "Haruki Murakami"

```java
import jakarta.persistence.*;
import java.util.List;

public class BookRepository {

    EntityManager entityManager = entityManagerFactory.createEntityManager();

    // Method to find all books by a specific author
    public List<Book> findAllBooksByAuthor(String authorName) {
        EntityManager entityManager = entityManagerFactory.createEntityManager();

        // Create a JPQL query to find all books by the specified author
        TypedQuery<Book> query = entityManager.createQuery("SELECT b FROM Book b WHERE b.author = :authorName", Book.class);
        query.setParameter("authorName", authorName);

        // Execute the query and get the result list
        List<Book> books = query.getResultList();

        // Close the EntityManager
        entityManager.close();

        return books;
    }

    // Other methods like addBook, updateBook, and removeBook (same as previous examples)
    // ...
}
```

### Explanation

- The `findAllBooksByAuthor` method accepts an `authorName` parameter.
- It uses the `EntityManager` to create a JPQL query with `entityManager.createQuery()`. The query selects all books from the `Book` entity where the `author` field matches the `authorName` parameter.
- The `TypedQuery` interface is used for type safety.
- The `query.getResultList()` method executes the query and returns a `List<Book>` containing all books written by the specified author.

You can now call this method to retrieve all books written by "Haruki Murakami" or any other author you specify. Note that this example is simplified and omits things like error handling and logging for the sake of clarity. In a real-world application, you'd likely include those as well.
