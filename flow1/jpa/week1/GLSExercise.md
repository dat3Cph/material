# GLS package delivery exercise

Using:

Imagine we want to keep track of a package delivery sent from a sender, "Mr. Senderson", to a receiver "Mrs. Receiverson". 

The package is identified by a unique id, the name of the sender, the address + name of the receiver. A created date/time, an updated date/time when changes happen to the entity, and whatever you can come up with. As long as you only use one entity called "Package".

Todo:
1. Create a Maven / JPA project
2. Create a new database in Postgres for the project.
3. Create the "Package" entity with JPA annotations.
4. Implement a DAO with basic CRUD and test the methods with unit testing as you go along.

Mandatory features:
- use date/time attributes
- pre/update life cycle methods
- DAO for architectural purposes
- CRUD (persist, jpql, merge, remove)
- Test (jUnit)
- Lombok (please use in entity)