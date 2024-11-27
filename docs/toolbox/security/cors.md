---
title: CORS headers
description: Adding Cors headers to your API
layout: default
nav_order: 2
grand_parent: Toolbox
parent: Security
permalink: /tools/security/cors
---

# CORS headers

Cross-Origin Resource Sharing (CORS). These are great ressources:

- [CORS on Mozilla.org](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
- [CORS Explained In Under 4 minutes](https://www.youtube.com/watch?v=BibYiuLjpFM)

## Preparing your Javalin API for CORS

The Cross-Origin Resource Sharing standard works by adding new HTTP headers that let servers describe which origins are permitted to read that information from a web browser. To make our lives easier on 3rd semester, we allow generiously access to our API's. Keep in mind, that CORS only is of consideration for browser based clients. Any other server can request our apis, any time. So CORS headers are only a means to make life more secure for people using a webaplication that utilizes our endpoints made in Javalin.

## Setting up CORS headers

In your Javalin project, add these two methods to your `Application.config`:

```java
private static void corsHeaders(Context ctx) {
        ctx.header("Access-Control-Allow-Origin", "*");
        ctx.header("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE, OPTIONS");
        ctx.header("Access-Control-Allow-Headers", "Content-Type, Authorization");
        ctx.header("Access-Control-Allow-Credentials", "true");
    }

    private static void corsHeadersOptions(Context ctx) {
        ctx.header("Access-Control-Allow-Origin", "*");
        ctx.header("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE, OPTIONS");
        ctx.header("Access-Control-Allow-Headers", "Content-Type, Authorization");
        ctx.header("Access-Control-Allow-Credentials", "true");
        ctx.status(204);
    }
```

Then execute the methods in your `startServer` method:

```java
app.before(ApplicationConfig::corsHeaders);
app.options("/*", ApplicationConfig::corsHeadersOptions);
```

That's it. Now your API should be CORS hassle free.

Make sure you understand how it works.
