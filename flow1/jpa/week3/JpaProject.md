# Course Assignment 1

## Introduction

_"The business idea is about to create a platform that not only provides information about people 
and their hobbies but also offers a matchmaking service. Users can input their hobbies and interests, and the 
platform can connect them with like-minded individuals or groups in their local area. This would add a social 
networking element to the service and encourage people to explore new hobbies together, fostering real-world connections."_

This business idea is one of many you can think of. There are, however, a few restrictions that you must adhere to.
For instance, users who register must be able to enter their hobbies, phone number and ultimately their full address in their profile.
Of course, the user stories mentioned below must also play into your considerations.

Your task is to find a business idea where users and hobbies play a central role. You can, of course, make the above 
business concept your own and perhaps expand on it.

Once you have come up with a business idea, your next step will be to develop a domain model. This will make it easier 
for you to keep an overall perspective over your business plan. Conceptional a domain model is a representation of the
problem domain (the subject area the software deals with). It defines the entities, their attributes, and how they relate to each other in the real-world context.



The last step is to create a diagram that mirrors your future database, also known as an EER diagram.

Your Domain Model and EER diagram will be the foundation for your database and the JPA entities you will create in the next step. Both
diagram should be added to your README.md file with the business idea and user stories.

Happy coding!


## Technologies

- JPA
- JPQL
- Maven
- JDK 17
- JUnit 5
- Docker
- PostgresSQL
- pgAdmin
- Lombok

## User Stories

- [U1] As a user I want to get all the information about a person
- [U2] As a user I want to get all phone numbers from a given person
- [U3] As a user I want to get all persons with a given hobby
- [U4] As a user I want to get the number of people with a given hobby
- [U5] As a user I want to get a list all hobbies + a count of how many are interested in each hobby
- [U6] As a user I want to get all persons living in a given city (i.e. 2800 Lyngby)
- [U7] As a user I want to get a list of all postcodes and city names in Denmark
- [U8] As a user I want to get all the information about a person (address, hobbies etc) given a phone number
- [U9] As a user I want to be able to do CRUD operations on all JPA entities unless it wouldn't make sense for a given entity.
- [U10] … Add more meaningful services of your own choice 

### Project Requirements

- [R1] The project must use the following technologies
    - JPA
    - JPQL
    - Maven
    - JDK 17
    - JUnit 5
    - Docker
    - PostgresSQL
    - pgAdmin
    - Lombok
- [R2] The project must contain a meaningful eer-diagram (use pgAdmin to create the diagram)
- [R3] The project must be documented (short) in a README.md file 
- [R4] The project must contain meaningful unit tests. (All methods must be tested (DAO, Entity ...))
- [R5] JPA annotations must be used for mapping domain classes
- [R6] JPQL must be used for all CRUD operations
- [R7] JPA annotations must include minimum once an @Enumerated, @PrePersist, @PreUpdate and @Temporal tag.
- [R8] The phone number as to follow the Danish rules for phone numbers (e.g. +45 12345678)
- [R9] The project must be handed in Moodle as a link to a git-repo containing the full source code incl. unit tests. [Link](#)

### Optional Requirements

- [O1] TODO


### Resources

- [ZipCode - Hobby](https://github.com/dat3startcode/dataForCA-2 )

Alternatively and more challenging can the data for City Info be requested from the following API:
- [Dataforsyning]https://api.dataforsyningen.dk/postnumre

