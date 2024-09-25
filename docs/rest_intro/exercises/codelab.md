---
title: CodeLab
description: Rest Intro Codelab
layout: default
nav_order: 3
grand_parent: Rest API intro
parent: Exercises
permalink: /rest-intro/exercises/codelab/
---

# Poem API exchange

![Haiku classic](./images/haiku.jpg){: .mx-auto .d-block .my-5 .md .d-md-none }
![Haiku classic](./images/haiku.jpg){: .d-none .d-md-inline-block .ml-3 .mb-5 .float-right}

This CodeLab exercise is designed to help you practice RESTful API concepts. We will also
practice [pair programming](../../toolbox/sys/projectmanagement/pairprogramming.md) and exchanging API endpoints with
another team.

So today we will work in pairs of 2 and then exchange our APIs with another team of programmers. This means that you
should not create pull-requests to the same repository as you usually do. Instead, each team will have their own
repository and then exchange the API endpoints with another team later.

## 1. The assignment

You are going to build a brilliant API for exchanging poems. The API should be able to handle CRUD operations for poems.
Just to get our feet wet with REST APIs and Javalin.

## 2. Gather a team of 2 and find another team of 2 to exchange APIs with (later)

## 3. Sign up on Moodle

[Create a team of 3-5 people in Moodle](https://cphbusiness.mrooms.net/mod/choicegroup/view.php?id=732839).
This is mainly for the teachers to be able to check attendance, and for you to get study points.

## 4. Decide on which poem style you want to share through your api?

Pick your favourite style: Haiku, Limerick, Senryu, Tanka, Sonnet, Villanelle, Acrostic, Elegy, Ode, Ghazal, Sestina,
Pantoum, Terza Rima, Triolet, Rondel, Rondeau, Villanelle, Ballad, Epic, Free verse, Lyric, Narrative, Prose, Rhymed
verse, Blank verse, Concrete, Found, Light, Visual, etc.

## 5. Get the data ready

Collect 5-10 smashing poems in your favourite style and save them in a text file for later

## 6. Set up the development environment / start code and Git (one per team)

## 7. Connect a database and create an Entity + DTO for the poems

1. Each member should create a database in your docker environment with postgres called `poems`.
2. Set up the HibernateConfig file to connect to the database.
3. Create a Poem entity. You decide which fields you want to have in the Poem entity.
4. Create a PoemDTO class. The PoemDTO class should have a constructor that takes a Poem entity as a parameter and
   creates a PoemDTO object from it.

## 8. Let's get started

Each team will create a RESTful API for poems. The poems should be stored in a database. Ideally, the API should be able
to handle all CRUD operations for poems. But we begin simple with the `/poems` endpoint. The API should be able to
handle the following routes representing a poem resource:

| Method | Endpoint   | Comment                                 |
|--------|------------|-----------------------------------------|
| GET    | /poem      | Returns all poems from the database     |
| GET    | /poem/{id} | Returns a specific poem based on the id |
| POST   | /poem      | Creates a new poem                      |
| PUT    | /poem/{id} | Updates an existing poem                |
| DELETE | /poem/{id} | Deletes an existing poem                |

When the first endpoint `poems` (get all poems) is ready, you will try to create a `.http` file to test the endpoint.
The http file should be able to test the endpoint and return the result in a json format.

**Exchanging poems with your friends**

Now, let's log into the **cphbus** hotspot and and find your local IP address. Hand this IP address to your friends (
another team) so they can test your API. We need to be on the same network and subnet to be able to test the API. That's
why we need to log into the same hotspot. So if the other team has IP address `10.132.12.13`, Jetty Port 7071, and they
have the endpoint `/poems`, you should be able to test their API by typing `http://10.132.12.13:7071/poems` in your
browser - or from a `.http` file.

## 9. Build a joint API

The idea is now to share poems with your friends and collect their poems and add them with yours in a new endpoint
called `/poems/friends`. This endpoint should return all poems from your friends' API and your API together. This will
take some fetching, DTO conversion and merging of the two APIs in a joint DTO.

## 10. Implement all the CRUD operations

Make sure that all CRUD operations are working as expected. You should be able to create, read, update and delete poems
from your own API.
