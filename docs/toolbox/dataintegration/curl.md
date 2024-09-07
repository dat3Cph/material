---
title: CURL
description: What is `curl` and how to use it to interact with APIs
layout: default
parent: Data Integration
grand_parent: Toolbox
nav_order: 9
permalink: /toolbox/dataintegration/curl/
---

# What is `curl`?

`curl` is a command-line tool for transferring data to or from a server using various protocols, such as HTTP, HTTPS, FTP, and more. It's widely used to make HTTP requests directly from the terminal, such as GET, POST, PUT, DELETE, etc.

Key uses of `curl` include:

- Downloading or uploading data
- Interacting with APIs
- Debugging HTTP requests

### Basic `curl` Syntax

```bash
curl [options] [URL]
```

For example, to fetch data from a URL:

```bash
curl https://api.example.com/resource
```

### Example: Fetching a Joke from the Chuck Norris API

The **Chuck Norris API** (`https://api.chucknorris.io`) provides random Chuck Norris jokes. Here’s how you can use `curl` to fetch a random joke from this API.

#### Command to Fetch a Random Joke

```bash
curl https://api.chucknorris.io/jokes/random
```

### Explanation

- **URL**: `https://api.chucknorris.io/jokes/random` is the endpoint that returns a random joke in JSON format.
- **Output**: This command will display a random Chuck Norris joke in JSON format in your terminal.

#### Example Output

```json
{
  "categories": [],
  "created_at": "2020-01-05 13:42:19.576875",
  "icon_url": "https://assets.chucknorris.host/img/avatar/chucknorris.png",
  "id": "gW8tPYxFQ7KsQOxDGVyhrg",
  "updated_at": "2020-01-05 13:42:19.576875",
  "url": "https://api.chucknorris.io/jokes/gW8tPYxFQ7KsQOxDGVyhrg",
  "value": "Chuck Norris can divide by zero."
}
```

### Fetching a Joke by Category

The Chuck Norris API also allows you to fetch jokes by category. First, you can list the available categories:

```bash
curl https://api.chucknorris.io/jokes/categories
```

Then, to fetch a joke from a specific category, such as "animal":

```bash
curl "https://api.chucknorris.io/jokes/random?category=animal"
```

The `?category=animal` query parameter specifies the joke category you want.

### Summary

- **`curl`** is a versatile command-line tool for interacting with HTTP APIs and more.
- **Chuck Norris API** is a free API that returns random jokes. Using `curl`, you can easily fetch jokes directly from your terminal.
