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
    - [icanhazdadjoke](https://icanhazdadjoke.com/api) (this needs a header `Accept: application/json`)
    - [chucknorris](https://api.chucknorris.io/jokes/random)
    - [kanye.rest](https://api.kanye.rest)
    - [whatdoestrumpthink](https://api.whatdoestrumpthink.com/api/v1/quotes/random)
    - [jokeapi](https://v2.jokeapi.dev/joke/Coding?type=single)
    - [geek-jokes](https://geek-jokes.sameerkumar.website/api?format=json)
    - [official-joke-api](https://official-joke-api.appspot.com/random_joke)<br/>

    You might want to use the following code to get the ball rolling:

        ```java
        String[] urls = new String[]{
            "https://icanhazdadjoke.com/",
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

### Json example from Icanhazdadjoke

```json
{
    "id": "Xny5MZvHQCd",
    "joke": "Can I watch the TV? Dad: Yes, but don’t turn it on.",
    "status": 200
}
```

### Json example from Chuck Norris

```json
{
    "categories": [],
    "created_at": "2020-01-05 13:42:19.576875",
    "icon_url": "https://assets.chucknorris.host/img/avatar/chuck-norris.png",
    "id": "1",
    "updated_at": "2020-01-05 13:42:19.576875",
    "url": "https://api.chucknorris.io/jokes/1",
    "value": "Chuck Norris can divide by zero."
}
```

### Json example from Kanye Rest

```json
{
    "quote": "I feel like I'm too busy writing history to read it."
}
```

### Json example from What Does Trump Think

```json
{
    "message": "The beauty of me is that I'm very rich.",
    "nlp_attributes": {
        "quote_structure": [
            [
                "Determiner",
                "Noun",
                "Preposition",
                "Pronoun",
                "Copula",
                "Determiner",
                "Noun",
                "Adverb",
                "Adjective"
            ]
        ]
    }
}
```

### Json example from Joke API

```json
{
    "category": "Programming",
    "type": "single",
    "joke": "Why do programmers prefer dark mode? Because light attracts bugs.",
    "flags": {
        "nsfw": false,
        "religious": false,
        "political": false,
        "racist": false,
        "sexist": false
    },
    "id": 1,
    "error": false
}
```

### Json example from Geek Jokes

```json
{
    "joke": "What does a subatomic duck say? Quark."
}
```

### Json example from Official Joke API

```json
{
    "type": "general",
    "setup": "What was a more important invention than the first telephone?",
    "punchline": "The second one.",
    "id": 262
}
```
