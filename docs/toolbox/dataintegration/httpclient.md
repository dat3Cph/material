---
title: Fetching from an API?
description: Example of fetching data from an API with httpclient
layout: default
parent: Data Integration
grand_parent: Toolbox
nav_order: 8
permalink: /toolbox/dataintegration/httpclient
---
# Fetching JSON from an API using HttpClient

## 1. **`HttpClient` (Introduced in Java 11)**

`HttpClient` is a modern API for HTTP communication that was introduced in **Java 11**. It brings several improvements over the older `HttpURLConnection`:

#### **Key Advantages of `HttpClient`**

- **Asynchronous and Synchronous Support**:
  - `HttpClient` supports both **synchronous** (blocking) and **asynchronous** (non-blocking) requests. This is a major improvement over `HttpURLConnection`, allowing for better performance in applications where network latency or server response times can be variable.

  - With asynchronous requests, the application can continue processing other tasks while waiting for a response, making it more efficient for handling concurrent HTTP requests.

- **Cleaner, More Intuitive API**:
  - The `HttpClient` API is much easier to use, with less boilerplate code. It provides a builder pattern to configure the HTTP client and requests in a fluent and readable way.

- **Built-in Support for HTTP/2 and WebSockets**:
  - `HttpClient` has native support for **HTTP/2**, which improves performance by allowing multiplexed requests, header compression, and better resource management.
  - It also supports **WebSockets**, which allows real-time, bidirectional communication between the client and server.

- **Timeouts and Redirection**:
  - `HttpClient` provides easy-to-configure options for setting **timeouts** and handling **redirections** automatically, reducing the complexity involved in managing these aspects manually.

- **Built-in Cookie and Authentication Support**:
  - `HttpClient` supports managing cookies, proxies, and authentication mechanisms (such as **Basic Authentication**) out of the box.

- **Immutable and Thread-Safe**:
  - `HttpClient` instances are **immutable** and **thread-safe**, meaning they can be safely shared between threads, making them ideal for use in multi-threaded applications.

#### Example of `HttpClient`

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class HttpClientExample {
    public static void main(String[] args) {
        try {
            // Create an HttpClient instance
            HttpClient client = HttpClient.newHttpClient();

            // Create a request
            HttpRequest request = HttpRequest.newBuilder()
                    .uri(new URI("https://vejr.eu/api.php?location=Roskilde&degree=C"))
                    .GET()
                    .build();

            // Send the request and get the response
            HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

            // Check the status code and print the response
            if (response.statusCode() == 200) {
                System.out.println(response.body());
            } else {
                System.out.println("GET request failed. Status code: " + response.statusCode());
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

**Async Example**:

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.util.concurrent.CompletableFuture;

public class AsyncHttpClientExample {
    public static void main(String[] args) {
        HttpClient client = HttpClient.newHttpClient();

        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://vejr.eu/api.php?location=Roskilde&degree=C"))
                .build();

        CompletableFuture<HttpResponse<String>> response = client.sendAsync(request, HttpResponse.BodyHandlers.ofString());

        // Handle the async response
        response.thenAccept(res -> {
            if (res.statusCode() == 200) {
                System.out.println(res.body());
            } else {
                System.out.println("Request failed. Status code: " + res.statusCode());
            }
        }).join(); // Ensures the main thread waits for completion
    }
}
```

#### **Comparison: `HttpURLConnection` vs. `HttpClient`**

| Feature                            | `HttpURLConnection`              | `HttpClient` (Java 11+)                 |
|-------------------------------------|----------------------------------|----------------------------------------|
| **Asynchronous Support**            | No                               | Yes (non-blocking requests)            |
| **Synchronous Support**             | Yes                              | Yes                                    |
| **HTTP/2 Support**                  | No                               | Yes                                    |
| **WebSocket Support**               | No                               | Yes                                    |
| **Boilerplate Code**                | High                             | Low (fluent, cleaner API)              |
| **Cookie Management**               | Manual                           | Automatic (built-in support)           |
| **Authentication Support**          | Manual (or third-party libraries) | Built-in support for Basic Auth, etc.  |
| **Timeout and Redirect Handling**   | Manual                           | Easy, with built-in methods            |
| **Thread Safety**                   | Limited                          | HttpClient is thread-safe              |

### Conclusion

`HttpClient` offers a much cleaner, modern, and feature-rich API compared to the older `HttpURLConnection`. It simplifies HTTP communication in Java by reducing boilerplate code, supporting both synchronous and asynchronous operations, and offering native support for HTTP/2 and WebSockets. These improvements make it the preferred choice for building HTTP clients in Java 11 and beyond.
