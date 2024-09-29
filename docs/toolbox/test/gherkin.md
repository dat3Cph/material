---
title: Gherkin Syntax
description: How to use Gherkin syntax for writing test cases
layout: default
parent: Test
grand_parent: Toolbox
nav_order: 3
permalink: /toolbox/test/gherkin-syntax
---

# Gherkin Syntax

**Gherkin** is a language used for writing structured, human-readable tests in **Behavior-Driven Development (BDD)**. It is designed to bridge the gap between technical and non-technical stakeholders by defining test scenarios using natural language and a clear structure. Gherkin syntax is commonly used with tools like **Cucumber** to define test cases in a format that both developers and business analysts can understand.

### Key Concepts in Gherkin Syntax

- **Feature:** Describes a feature of the application being tested. It contains a group of related test scenarios.
- **Scenario:** Represents a single test case, providing a specific example of how the system should behave.
- **Given:** Defines the initial context or preconditions for the scenario (i.e., the starting state).
- **When:** Describes the action or event that triggers the behavior being tested.
- **Then:** Specifies the expected outcome or result after the action has been performed.
- **And/But:** Used to add more conditions to the `Given`, `When`, or `Then` steps.

### Gherkin Syntax Example

```gherkin
Feature: User login
  Scenario: Successful login with valid credentials
    Given the user is on the login page
    When the user enters valid credentials
    Then the user should be redirected to the homepage
```

### How Gherkin is Used in Rest Assured

Rest Assured can be used in combination with **Cucumber** to implement BDD-style tests. Gherkin defines the behavior in natural language, and the actual test implementation is done in Java, using Rest Assured for interacting with the REST APIs.

Here’s how you can integrate Gherkin with Rest Assured:

1. **Define the Feature and Scenario (in `.feature` file):**

   ```gherkin
   Feature: API Testing with Rest Assured
     Scenario: Verify successful GET request to retrieve user details
       Given I have the base URL for the API
       When I send a GET request to "/users/1"
       Then I should receive a 200 OK response
       And the user name should be "John Doe"
   ```

2. **Implement the Step Definitions (in Java code):**
   These steps link the Gherkin scenario to Java code, using Rest Assured to make API calls and validate responses.

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

3. **Run the Test:**
   Once the steps are defined, you can run the tests using a tool like Cucumber or JUnit. The framework will interpret the Gherkin scenarios and execute the corresponding Java code with Rest Assured to make the HTTP requests and check the responses.

### Why Use Gherkin with Rest Assured

- **Readable and Understandable Tests:** The Gherkin syntax makes test cases easier to understand for both technical and non-technical team members, improving collaboration.
- **BDD Workflow:** It supports the BDD workflow, where the behavior of the system is defined before implementation, ensuring better alignment between development and business goals.
- **Automated API Testing:** When combined with Rest Assured, Gherkin enables automated API testing in a structured, maintainable way that is easy to integrate with CI/CD pipelines.

In summary, **Gherkin syntax** allows for structured, human-readable test definitions, and when used with Rest Assured in a **Cucumber BDD** environment, it facilitates the testing of REST APIs in a clear, maintainable way.
