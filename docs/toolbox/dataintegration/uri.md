---
title: URI
description: What is a URI?
layout: default
parent: Data Integration
grand_parent: Toolbox
nav_order: 1
permalink: /toolbox/dataintegration/uri/
---


# What is an URI?

**URI** stands for **Uniform Resource Identifier**. It is a string of characters used to identify a resource on the Internet. A URI provides a simple and extensible means to identify resources either by location, name, or both.

There are two main types of URIs:

1. **URL (Uniform Resource Locator)**: Specifies the location of a resource on the Internet, including the protocol needed to access it (e.g., `http://`, `https://`, `ftp://`).
   - Example: `https://www.example.com/index.html`

2. **URN (Uniform Resource Name)**: Specifies a resource by name within a given namespace, but does not necessarily tell you how to access it.
   - Example: `urn:isbn:9780134685991`

### Components of a URI

A URI can have several components:

- **Scheme**: Identifies the protocol (e.g., `http`, `https`, `ftp`).
- **Authority**: Includes the domain name or IP address of the server (e.g., `www.example.com`).
- **Path**: Specifies the specific resource (e.g., `/index.html`).
- **Query**: Optional parameters passed to the server (e.g., `?name=John`).
- **Fragment**: Optional anchor within the resource (e.g., `#section1`).

**Example of a full URI**:  

`https://www.example.com/path/to/resource?query=example#fragment`

In this example:

- **Scheme**: `https`
- **Authority**: `www.example.com`
- **Path**: `/path/to/resource`
- **Query**: `?query=example`
- **Fragment**: `#fragment`

In summary, a URI is a general concept that includes both URLs (which provide a location for a resource) and URNs (which provide a name for a resource).
