---
title: Poems API Security
description: Adding a security layer to the Poems API
layout: default
nav_order: 6
grand_parent: Rest API Test and Security
parent: Exercises
permalink: /rest-test-security/exercises/poems-security/
---

# Security layer for Poems API (To do in class on Thursday)

- [See this resource for help and snippets](../../toolbox/security/api_security.md)

## Create the security routes

1. Create the following routes:

    - POST /register        // Open for everyone
    - POST /login           // Open for everyone
    - GET /poems            // only for users with the role USER
    - GET /poems/{id}       // only for users with the role USER
    - POST /poems           // only for users with the role ADMIN
    - PUT /poems/{id}       // only for users with the role ADMIN
    - DELETE /poems/{id}    // only for users with the role ADMIN

2. In case you don't have a Poems API. In Lyngby, you can clone this one:

    ```bash
      git clone --branch architecture https://github.com/jonbertelsen/poems.git
    ```

    If you do, then pay attention to the routes, that might be a little different from ones above. However, the plan is to only allow ADMIN users to create, update, and delete poems, while all users can read poems.
