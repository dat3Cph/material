---
title: Hotel API part 1
description: Hotel API part 1
layout: default
nav_order: 6
grand_parent: Rest API intro
parent: Exercises
has_children: false
permalink: /rest-intro/exercises/hotel-api-part-1/
---

# Exercise with Javalin and CRUD

![Hotel California](./images/hotel_california.jpeg){: .mx-auto .d-block .my-5 .md .d-md-none }
![Hotel California](./images/hotel_california.jpeg){: .d-none .d-md-inline-block .ml-3 .mb-5 .float-right}

## Part 1 setup project

- Setup a new maven project in IntelliJ
- Add the following dependencies to the pom.xml file:
- Add necessary dependencies to pom.xml:
  - Javalin
  - JUnit
  - Gson or Jackson
  - hibernate
  - postgresql
- Create a new javalin application with 2 ressources: `Hotel`  and `Room`
- Create a new database in postgresql called `hotel`
- Create a IDAO generic interface with the following methods: *)
  - getAll()
  - getById()
  - create()
  - update()
  - delete()
- Create an abstract DAO class that implements the IDAO interface *)
- Create a HotelDAO and a RoomDAO that extends the abstract DAO class
- Add a method to the HotelDAO that returns all rooms for a specific hotel

*) NB! If you have trouble with inheritance and generics, you can skip the generic interface and abstract class and just create the DAO classes with the methods you need. You should also see the hint at the end of this document for more details.

## Part 2 DTOs

- Create a HotelDTO and a RoomDTO with the following fields:
  HotelDTO:
  - id
  - name
  - address
  - rooms

  RoomDTO:
  - id
  - hotelId
  - number
  - price

- Implement functionality to convert between DTOs and Entities. Both ways.

## Part 3 create API Ressources

- Create a HotelController and a RoomController that handles the above functionality using the DTOs
- Create a new Routes.java file that contains all routes for the application and implement the following routes with json:
  - GET /hotel
    - response json: `[{id: 1, name: "Hotel 1", address: "Address 1"}, {id: 2, name: "Hotel 2", address: "Address 2"}]`
  - GET /hotel/{id}
    - response json: `{id: 1, name: "Hotel 1", address: "Address 1"}`
  - GET /hotel/{id}/rooms
    - response json: `[{id: 1, hotelId: 1, number: 1, price: 100}, {id: 2, hotelId: 1, number: 2, price: 200}]`
  - POST /hotel
    - request json: `{name: "Hotel 3", address: "Address 3"}`
    - response json: `{id: 3, name: "Hotel 3", address: "Address 3"}`
  - PUT /hotel/{id}
    - request json: `{name: "Hotel renamedHotel", address: "Address 1"}`
    - response json: `{id: 1, name: "Hotel renamedHotel", address: "Address 1"}`
  - DELETE /hotel/{id}
    - response json: `{id: 1, name: "Hotel 1", address: "Address 1"}`
  - GET /room
    - Response json: `[{id: 1, hotelId: 1, number: 1, price: 100}, {id: 2, hotelId: 1, number: 2, price: 200}]`
  - GET /room/{id}
    - Response json `{id: 1, hotelId: 1, number: 1, price: 100}`
  - POST /room
    - Request json `{hotelId: 1, number: 1, price: 100}`
    - Response json `{id: 1, hotelId: 1, number: 1, price: 100}`
  - PUT /room/{id}
    - Request json: `{hotelId: 1, number: 1234, price: 333}`
    - Response json `{id: 1, hotelId: 1, number: 1234, price: 333}`
  - DELETE /room/{id}
    - Response json: `{id: 1, hotelId: 1, number: 1, price: 100}`

In above api, if no request json is specified, then the request body should be empty.

NB! Use an http file to test the endpoints.

## Part 4 Error handling

- Implement app.error() to handle:
  - 404 Not Found (used for both missing resources and missing routes)
- Implement app.exception() to handle:
  - IllegalStateException: When posting or updating a hotel or room with incorrect json representation.

## Part 5: (Optional) logging

Use our small tutorial from yesterday and use LogBack to log requests, responses, and exceptions.

- Implement logging for all requests and responses
- Include the following information in the log:
  - Timestamp
  - Request method
  - Request path
  - Request body
  - Response status code
  - Response body

## Part 6 (Optional) Documentation

- Configure javalin to use `RouteOverviewPlugin` to create an interactive documentation of your API.

## Monday review

- Prepare a short presentation of your API for Monday's review session. You will have 5 minutes to present your API and show how it works. You can use an http file to demonstrate the API.

## Hint on generics and inheritance

When implementing your DAOs, consider creating a generic `IDAO` interface and an `AbstractDAO` class to handle common CRUD operations for any entity type. This approach helps reduce code duplication and makes your code more maintainable. Here’s a quick guide:

1. **Define the `IDAO` Interface**: This interface should specify basic CRUD methods (`getAll()`, `getById()`, `create()`, `update()`, `delete()`) using generics (`<T>`) to handle different types of entities.

2. **Create an `AbstractDAO` Class**: Implement the `IDAO` interface in an abstract class called `AbstractDAO`. This class will provide common implementations of CRUD methods, utilizing an `EntityManager` for database interactions. Use generics to make it flexible for any entity type.

3. **Extend `AbstractDAO` in Specific DAOs**: Create concrete DAO classes like `HotelDAO` and `RoomDAO` that extend `AbstractDAO`. These classes can inherit the common CRUD functionality and add any specific methods needed for their respective entities, such as fetching all rooms for a particular hotel in `HotelDAO`.

4. **Example Method Signatures**:
   - In `IDAO`: `List<T> getAll();`
   - In `AbstractDAO`: `public List<T> getAll() { // common implementation }`
   - In `HotelDAO`: `public List<Room> getRoomsForHotel(int hotelId) { // specific implementation }`

**If you find generics and inheritance challenging**, you can skip this approach and directly implement the required CRUD methods in your DAO classes (`HotelDAO` and `RoomDAO`). However, using the interface and abstract class will make your code cleaner and more reusable.
