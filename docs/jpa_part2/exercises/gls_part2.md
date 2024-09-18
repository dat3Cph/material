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

![gls delivery](./images/gls_shipments.png)

In this part of the exercise, we'll extend the GLS Package Tracking System to include more complex relationships between entities and introduce additional functionality.

When a package i sent from one location to another, it is considered a shipment. A shipment is a movement of a package between two locations. Each shipment is associated with a package, a source location, and a destination location. The package can have multiple shipments, but each shipment is associated with only one package, one source location, and one destination location. In the illustation above, a package is sent from Copenhagen to Aaarhus through four shipments between five locations.

### Requirements and Instructions for the entities and relationships

Read the requirements below and sketch a class diagram to visualize the entities, and the relationships between them. This will give you an overview of the entities and their relationships before you start implementing them. Later you might want to add methods.

1. Extend the existing package tracking system to include a new entity named "Location" to manage location information. The "Location" entity should have the following attributes:

   - ID (auto-generated primary key)
   - Latitude (Double)
   - Longitude (Double)
   - Address (String)

2. Create a new entity named "Shipment" to represent the movement of packages between locations. The "Shipment" entity should at least have the following attributes:

   - ID (auto-generated primary key)
   - Package (ManyToOne relationship with the Package entity)
   - Source location (ManyToOne relationship with the Location entity)
   - Destination location (ManyToOne relationship with the Location entity)
   - Shipment date/time (Date/Time attribute)

3. Implement relationships between entities:
   - A package can have multiple shipments.
   - Each shipment is associated with one package, one source location, and one destination location.

4. Update the DAO and entity classes to handle the new relationships and attributes. You might want to create new DAO classes for the "Location" and "Shipment" entities as well, and begin by implementing the CRUD operations for these entities little by little. A good approach is to start with the "Location" entity and then move on to the "Shipment" entity. And also to first implement the read operations (find by ID, find all, etc.) and then move on to the create. Update, and delete operations are usually the most complex to implement.

5. Write additional JUnit tests (integration tests) to verify the functionality of the new features.

## Expected Outcome

By completing Part 2 of the exercise, you'll gain a deeper understanding of how to manage complex relationships between entities using JPA and how to implement more advanced features in a Java-based application.
