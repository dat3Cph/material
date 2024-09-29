---
title: Rest Assured
description: Rest Assured Overview
layout: default
parent: Test
grand_parent: Toolbox
nav_order: 2
permalink: /toolbox/test/rest-assured
---

# Rest Assured

**Rest Assured** is a popular Java library used for testing and validating RESTful APIs. It simplifies writing tests for REST services by providing an easy-to-use syntax, allowing developers to send HTTP requests and verify the responses without writing a lot of boilerplate code.

### Key Features of Rest Assured

- **Simplified HTTP request handling:** Rest Assured allows you to perform all common HTTP methods (GET, POST, PUT, DELETE, etc.) in a simple, readable syntax.
- **Built-in validation methods:** It provides built-in methods for validating response data like status codes, headers, body content, etc., using a BDD (Behavior-Driven Development)-style approach.
- **Integration with testing frameworks:** Rest Assured integrates easily with popular testing frameworks like JUnit and TestNG, making it seamless to write API tests alongside unit tests.

### Why Rest Assured is Necessary

1. **Ease of Use:** Testing REST APIs without Rest Assured can involve writing significant boilerplate code using libraries like `HttpURLConnection` or `HttpClient`. Rest Assured abstracts away much of this complexity.

2. **Readable and Maintainable Tests:** The DSL (Domain-Specific Language) used in Rest Assured makes the test cases more readable and easier to maintain. For example using the [Gherkin Syntax](./gherkin.md) with Rest Assured:

   ```java
    @Test
    void create()
    {
        Hotel h3 = new Hotel("Cab-inn", "Østergade 2", Hotel.HotelType.BUDGET);
        Room r1 = new Room(117, new BigDecimal(4500), Room.RoomType.SINGLE);
        Room r2 = new Room(118, new BigDecimal(2300), Room.RoomType.DOUBLE);
        h3.addRoom(r1);
        h3.addRoom(r2);
        HotelDto newHotel = new HotelDto(h3);

        List<RoomDto> roomDtos =
        given()
                .contentType(ContentType.JSON)
                .body(newHotel)
                .when()
                .post(BASE_URL + "/hotels")
                .then()
                .statusCode(201)
                .body("id", equalTo(3))
                .body("hotelName", equalTo("Cab-inn"))
                .body("hotelAddress", equalTo("Østergade 2"))
                .body("hotelType", equalTo("BUDGET"))
                .body("rooms", hasSize(2))
                .extract().body().jsonPath().getList("rooms", RoomDto.class);

        assertThat(roomDtos, containsInAnyOrder(new RoomDto(r1), new RoomDto(r2)));
    }
   ```

3. **Comprehensive API Testing:** Rest Assured supports a wide range of features like:
   - Authentication (Basic, OAuth)
   - JSON/XML response validation
   - Multi-part form data testing
   - Request/Response logging for debugging

4. **Integration and Automation:** It helps automate API tests in CI/CD pipelines, ensuring that any changes to the API are quickly caught, which is crucial for maintaining the health of modern microservices-based architectures.

In summary, **Rest Assured** is widely used because it makes testing RESTful APIs simple, readable, and maintainable, which is especially valuable in projects that involve continuous integration and automated testing.

## Overview of the difference between Rest Assured and regular DAO Integration Testing

![Overview](./images/javalin_test_map.png)
