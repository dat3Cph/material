---
title: Unicorn Snippets
description: unicorn snippet
layout: default
nav_order: 1
parent: Exercises
grand_parent: JPA Part 1
permalink: /jpa-part-1/exercises/unicorn_snippets/
---

# Snippets for Unicorn JPA exercise

## Unicorn.class

```java
import jakarta.persistence.*;

@Entity
public class Unicorn {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "unicorn_id", nullable = false)
    private int id;

    @Column(name = "name", length = 100)
    private String name;

    @Column(name = "age")
    private int age;

    @Column(name = "power_strength")
    private int powerStrength;

    public Unicorn()
    {
    }

    // Getters and setters
}
```

## Remember to add the entity in the HibernateConfig file

```java
private static void getAnnotationConfiguration(Configuration configuration) {
        configuration.addAnnotatedClass(Unicorn.class);
    }
```

## UnicornDAO.class

```java
import jakarta.persistence.*;

public class UnicornDAO
{

    private EntityManagerFactory emf = HibernateConfig.getEntityManagerFactoryConfig();

    public Unicorn save(Unicorn unicorn)
    {
        EntityManager em = emf.createEntityManager();
        em.getTransaction().begin();
        em.persist(unicorn);
        em.getTransaction().commit();
        em.close();
        return unicorn;
    }

    public Unicorn findById(int id)
    {
        EntityManager em = emf.createEntityManager();
        Unicorn foundUnicorn = em.find(Unicorn.class, id);
        em.close();
        return foundUnicorn;
    }

    public Unicorn update(Unicorn unicorn)
    {
        EntityManager em = emf.createEntityManager();
        em.getTransaction().begin();
        Unicorn updatedUnicorn = em.merge(unicorn);
        em.getTransaction().commit();
        em.close();
        return updatedUnicorn;
    }

    public void delete(int id)
    {
        EntityManager em = emf.createEntityManager();
        em.getTransaction().begin();
        Unicorn unicorn = findById(id);
        if (unicorn != null)
        {
            em.remove(unicorn);
        }
        em.getTransaction().commit();
        em.close();
    }

    public void close()
    {
        emf.close();
    }
} 
```

## Main.class

```java
public class Main
{
    public static void main(String[] args)
    {
        UnicornDAO unicornDAO = new UnicornDAO();

        // Create
        Unicorn newUnicorn = new Unicorn();
        newUnicorn.setName("Sparkle");
        newUnicorn.setAge(5);
        newUnicorn.setPowerStrength(90);
        Unicorn createdUnicorn = unicornDAO.save(newUnicorn);

        // Read
        Unicorn foundUnicorn = unicornDAO.findById(createdUnicorn.getId());
        System.out.println("Found Unicorn: " + foundUnicorn.getName());

        // Update
        foundUnicorn.setAge(6);
        Unicorn updatedUnicorn = unicornDAO.update(foundUnicorn);
        System.out.println("Updated Unicorn Age: " + updatedUnicorn.getAge());

        // Delete
        //unicornDAO.delete(createdUnicorn.getId());

        unicornDAO.close();
    }
}
```
