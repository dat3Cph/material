---
title: GLS Part 1
description: gls exercise part 1
layout: default
nav_order: 1
parent: Exercises
grand_parent: JPA Part 1
permalink: /jpa-part-1/exercises/gls-part1/
---

## Exercise: GLS Package Tracking System - Part 1

![](../../images/glsbear.png)

### Scenario

GLS (Global Logistics Services) wants to develop a package tracking system to manage the delivery of packages. As part of the initial phase, they need to create a basic system using Java, JPA, and JPQL to manage package information.

### Requirements

1. Create an entity named "Package" using Lombok to manage package information. The "Package" entity should have the following attributes:
    - ID (auto-generated primary key)
    - Tracking number (String)
    - Sender name (String)
    - Receiver name (String)
    - Delivery status (Enum: PENDING, IN_TRANSIT, DELIVERED)

2. Implement a DAO (Data Access Object) class named "PackageDAO" to perform CRUD operations on the "Package" entity using JPA.

3. Define pre-update and pre-persist life cycle methods in the "Package" entity to update the last updated timestamp automatically.

4. Implement methods in the "PackageDAO" to perform the following operations:
    - Persist a new package
    - Retrieve a package by its tracking number
    - Update the delivery status of a package
    - Remove a package from the system

5. Write JUnit tests for the DAO methods to ensure they work correctly.

6. Use Maven for project management.

### Hints

- Use Jakarta Persistence (JPA) annotations to map the entity attributes to database columns.
- Implement JPQL queries for retrieving packages based on certain criteria, such as tracking number or delivery status.

4. JUnit Test Example:

```java
@TestInstance(TestInstance.Lifecycle.PER_CLASS)
public class PackageDAOTest {
    
   private static PackageDao packageDao;
   private static EntityManagerFactory emfTest;


   @BeforeAll
   static void setUpAll() {
      emfTest = HibernateConfig.getEntityManagerFactory();
      hotelDao = HotelDao.getInstance(emfTest);
   }
   
    @AfterAll
    public static void tearDown() {
        entityManager.close();
    }

    @Test
    public void testPersistPackage() {
        Package pkg = new Package();
        pkg.setTrackingNumber("ABC123");
        pkg.setSenderName("Sender");
        pkg.setReceiverName("Receiver");
        pkg.setDeliveryStatus(DeliveryStatus.PENDING);

        packageDAO.persistPackage(pkg);

        // Retrieve the package from the database and assert its existence
        Package retrievedPackage = entityManager.find(Package.class, pkg.getId());
        Assertions.assertNotNull(retrievedPackage);
        Assertions.assertEquals("ABC123", retrievedPackage.getTrackingNumber());
    }

    // Implement other test methods for CRUD operations
}
```

### Expected Outcome

This exercise should provide a solid foundation for understanding JPA (ORM) and JPQL in the context of building a package tracking system. In part 2, you can introduce more complex relationships between entities to further enhance the system.
