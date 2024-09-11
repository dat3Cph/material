---
title: Threaded Jokes
description: Java Deep Dive II Exercise Threads and Joke APIs
layout: default
nav_order: 8
has_children: false
grand_parent: Java Deep Dive II
parent: Exercises
permalink: /deepdive-2/exercises/jokes
---
# Joke API Exercise

This exercise can be done little by little. Start by getting one joke from one API and then add more APIs. You will have to create DTOs for each API and then a mega DTO that contains all the data.

1. Create a program to get data from 7 differenct web services (APIs) at the same time.
2. Get the returned value from the web service and save it in DTOs.
3. Collect all the DTO data in a mega DTO and print it out in a nice format.
4. Examples of APIs to use:

        ```java
        String[] urls = new String[]{
            "https://icanhazdadjoke.com/api",
            "https://api.chucknorris.io/jokes/random",
            "https://api.kanye.rest",
            "https://api.whatdoestrumpthink.com/api/v1/quotes/random",
            "https://v2.jokeapi.dev/joke/Coding?type=single",
            "https://geek-jokes.sameerkumar.website/api?format=json",
            "https://official-joke-api.appspot.com/random_joke"
        };
        ```
5. First you fetch and convert each joke to a DTO one at a time. Create a timer to mesure the time it takes to fetch all jokes.

6. Then you fetch all jokes at the same time (by using threads) and measure the time it takes to fetch all jokes. Hopefully this speeds things up. You need to work with the `ExecutorService` and `Future` classes.
