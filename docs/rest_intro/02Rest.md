## Restfull web services
### Architectural Constraints
[Source](https://restfulapi.net/rest-architectural-constraints/#code-on-demand)  

<img src="../images/ReST.png" width="1000" alt="">


- **Uniform interface**
    - communication between clients and servers in a RESTful system should be consistent and well-defined.
    - **HTTP** is the most used uniform interface and the one we will use in this course.
  - **Identification of resources**
    - Resources are identified in requests using URIs.
    - Http methods will be used to identify the operation to be performed on the resource.
    - **GET**: It is used to retrieve the current state of a resource. In RESTful terms, it corresponds to the "Read" operation.
    - **POST**: It is used to create a new resource on the server. It corresponds to the "Create" operation.
    - **PUT**: It is used to update the state of an existing resource or create a new resource if it doesn't exist. It corresponds to the "Update" operation.
    - **DELETE**: It is used to remove a resource from the server. It corresponds to the "Delete" operation.
  - **Manipulation of resources through representations**
    - Resources are represented in requests using a common media type (JSON, XML, etc.).
  - **Self-descriptive messages**
    - Requests and responses should include enough information to describe how to process the message.
    - HTTP headers are used to provide information about the request or response.
  - **Hypermedia as the engine of application state (HATEOAS)**
    - Clients should be able to navigate the API by following links in the responses.
    - This is the only constraint that is not implemented in HTTP.
    - This constraint is optional and not used in this course.
- **Client–server**
  - By separating the user interface concerns (client) from the data storage concerns (server), we improve the portability of the user interface across multiple platforms and improve scalability by simplifying the server components. The server can be written in python and the client in Java or vice versa. (In our case the server will be java and the client will be javascript)
- **Stateless**
  - Each request from client to server must contain all of the information necessary to understand the request, and cannot take advantage of any stored context on the server.
- **Cacheable**
  - Cache constraints require that the data within a response to a request be implicitly or explicitly labeled as cacheable or non-cacheable.
  - If a response is cacheable, then a client cache is given the right to reuse that response data for later, equivalent requests.
  - The advantage of adding cache constraints is that they have the potential to partially or completely eliminate some interactions, improving efficiency, scalability, and user-perceived performance by reducing the average latency of a series of interactions.
- **Layered system**
  - A client cannot ordinarily tell whether it is connected directly to the end server, or to an intermediary along the way.
  - Intermediary servers may improve system scalability by enabling load balancing and by providing shared caches.

### Good and Bad URL design
| Good | Bad |
| --- | --- |
| https://example.com/products/laptops <br/> This URL is clear and descriptive, indicating that it retrieves a list of laptops in the "products" category. | https://example.com/page.php?id=123 <br/> This URL uses non-descriptive query parameters and does not indicate the content of the page. |
| https://api.example.com/v1/users/123 <br/> This URL follows a structured pattern and specifies versioning (v1) for the API, retrieving user information for user ID 123. | https://example.com/article <br/> The URL lacks context and does not provide any information about the article. |
| https://blog.example.com/2023/09/best-rest-api-practices <br/> This URL includes a clear date structure and keywords, making it easy to understand the topic. | https://example.com/?p=4567 <br/> It uses a generic query parameter without any meaningful information about the resource. |
| https://example.com/search?q=restful+web+services <br/> This URL employs a query parameter (q) to perform a search for "restful web services." | https://api.example.com/service <br/> The URL is too vague and does not specify the service being accessed. |
| https://store.example.com/products/iphone-13 <br/> This URL includes the product name ("iphone-13") for direct access to a specific product page. | https://example.com/abcd123 <br/> This URL contains a seemingly random string of characters, making it unclear. |
| https://api.example.com/v2/orders/456/status <br/> Another versioned API URL, retrieving the status of order ID 456. | https://example.com/p?123 <br/> It combines non-descriptive characters and numbers without context. |
| https://example.com/about-us <br/> A simple and concise URL for an "About Us" page. | https://example.com/x/y/z/12345 <br/> The URL structure is overly complex and lacks clarity. |
| https://forum.example.com/category/programming/java <br/> This URL clearly indicates that it leads to a forum category related to programming in the Java language. | https://example.com/api/v1/endpoints/controller/123/action <br/> This URL is excessively long and complex, which can lead to confusion. |
| https://example.com/events/2023/conference-registration <br/> A structured URL for registering for a conference in the year 2023. | https://example.com/1/2/3/4/5/6 <br/> An excessively deep URL structure that is not user-friendly. |

### Summary
Good URLs are typically structured, descriptive, and user-friendly, making it clear to both users and search engines what the resource represents. Bad URLs, on the other hand, are often cryptic, lack context, and can lead to confusion for users and difficulty for search engines in understanding the content.

## Class Exercise 1:
- Open your exercise project from last session.
- Create a new class called `RestDemo.java` in the `src/main/java` folder.
- Create a main method with the javalin application containing 5 routes for an Animal ressource:
  - GET /animals // Returns all animals from an in-memory collection of animals (You decide the data structure)
  - GET /animal/{id} // Returns a specific animal based on the id
  - POST /animal // Creates a new animal
  - PUT /animal/{id} // Updates an existing animal
  - DELETE /animal/{id} // Deletes an existing animal
- Setup the server so that all animal endpoints are under the path `/api/animals`
- Let the Animals live in a map in memory with the id as key and the animal as value.

## Class Exercise 2:
- Create a new class called `RoutesDemo.java` in the `src/main/java` folder.
- Create an Animal Entity and implement an AnimalDAO with the following methods operating on the database:
  - getAllAnimals()
  - getAnimalById()
  - createAnimal()
  - updateAnimal()
  - deleteAnimal()
- Create an AnimalController that returns handlers with above functionality
- Rewrite code from last exercise to use the AnimalController instead of the in-memory map.
- Implement app.error() to handle:
  - 404 Not Found (used for both missing resources and missing routes)
  - 500 Internal Server Error
- Implement app.exception() to handle:
  - IllegalArgumentException: 400 Bad Request when trying to create or update an animal with an invalid id.
  - IllegalStateException: When posting or updating an animal with incorrect json representation.


