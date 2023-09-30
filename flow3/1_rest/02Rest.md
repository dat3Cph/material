## Restfull web services
### Architectural Constraints
[Source](https://restfulapi.net/rest-architectural-constraints/#code-on-demand)  

<img src="../images/ReST.png" width="1000" alt="">


- **Uniform interface**
    - communication between clients and servers in a RESTful system should be consistent and well-defined.
    - **HTTP** is the most used uniform interface and the one we will use in this course.
  - **Identification of resources**
    - Resources are identified in requests using URIs.
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
