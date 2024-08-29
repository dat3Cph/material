---
title: GLS Part 2
description: gls exercise part 2
layout: default
nav_order: 1
parent: Exercises
grand_parent: JPA Part 2
permalink: part2/exercises/gls-part2/
---

## Exercise: GLS Package Tracking System - Part 2

![gls delivery](../../images/glsdelivery.jpg)

In this part of the exercise, we'll extend the GLS Package Tracking System to include more complex relationships between entities and introduce additional functionality.

### Requirements:

1. Extend the existing package tracking system to include a new entity named "Location" using Lombok to manage location information. The "Location" entity should have the following attributes:
   - ID (auto-generated primary key)
   - Latitude (Double)
   - Longitude (Double)
   - Address (String)

2. Create a new entity named "Shipment" to represent the movement of packages between locations. The "Shipment" entity should have the following attributes:
   - ID (auto-generated primary key)
   - Package (ManyToOne relationship with the Package entity)
   - Source location (ManyToOne relationship with the Location entity)
   - Destination location (ManyToOne relationship with the Location entity)
   - Shipment date/time (Date/Time attribute)

3. Implement relationships between entities:
   - A package can have multiple shipments.
   - Each shipment is associated with one package, one source location, and one destination location.

4. Modify the "Package" entity to include a OneToMany relationship with the "Shipment" entity.

5. Update the DAO and entity classes to handle the new relationships and attributes.

6. Write additional JUnit tests to verify the functionality of the new features.

7. Use Jakarta Persistence (JPA) annotations to map the relationships between entities.

8. Update PackageDAO and ShipmentDAO classes to handle CRUD operations for the new entities and relationships.

9. Write additional JUnit tests to cover the new functionality, including creating shipments, associating shipments with packages, and retrieving packages with their shipments.

## Expected Outcome

By completing Part 2 of the exercise, you'll gain a deeper understanding of how to manage complex relationships between entities using JPA and how to implement more advanced features in a Java-based application.
