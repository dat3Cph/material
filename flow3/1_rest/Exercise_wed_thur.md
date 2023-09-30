# Exercise with javalin and CRUD

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
- Create a new database in postgresql called `hoteldb`
- Create a IDAO generic interface with the following methods:
  - getAll()
  - getById()
  - create()
  - update()
  - delete()
- Create an abstract DAO class that implements the IDAO interface
- Create a HotelDAO and a RoomDAO that extends the abstract DAO class
- Add a method to the HotelDAO that returns all rooms for a specific hotel

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

- Implement functionality to convert between DTOs and Entities


## Part 2 create API Ressources

- Create a HotelController and a RoomController that returns handlers with above functionality using the DTOs
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

## Part 3 Error handling

- Implement app.error() to handle:
  - 404 Not Found (used for both missing resources and missing routes)
- Implement app.exception() to handle:
  - IllegalStateException: When posting or updating a hotel or room with incorrect json representation.

## Part 4: (Optional) logging
- Implement logging for all requests and responses
- Include the following information in the log:
  - Timestamp
  - Request method
  - Request path
  - Request body
  - Response status code
  - Response body

## Part 5 (Optional) Documentation
- Configure javalin to use `RouteOverviewPlugin` to create an interactive documentation of your API.


