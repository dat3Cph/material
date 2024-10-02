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
[See this resource for help](./api_security.md)

## Create the security routes

1. Create the following routes:

    - POST /register        // Open for everyone
    - POST /login           // Open for everyone
    - GET /poems            // only for users with the role USER
    - GET /poems/{id}       // only for users with the role USER
    - POST /poems           // only for users with the role ADMIN
    - PUT /poems/{id}       // only for users with the role ADMIN
    - DELETE /poems/{id}    // only for users with the role ADMIN
