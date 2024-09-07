---
title: Rest API to DTOs
description: Java Deep Dive II Exercise DTO and JSON
layout: default
nav_order: 2
has_children: false
grand_parent: Java Deep Dive II
parent: Exercises
permalink: /deepdive-2/exercises/api-to-dto/
---

![TMDB logo](./images/blue_long.svg)

# Reading data from a Rest API into DTOs

In this exercise we want to read data from a Rest API and map it to DTOs. We will use the [The Movie Database API - TMDb](https://developer.themoviedb.org/reference/intro/getting-started) to fetch information about movies. We will then map the data to DTOs. And finally, we will add a JPA DAO and functionality to the DTOs.

## API Data Retrieval from the TMDB web-interface (the easy way)

First, let's get familiar with the TMDB API. We will use the web interface to get data from the API. This is the easiest way to get started.

1. Create an account a TMDB. Use [this link to sign up](https://www.themoviedb.org/signup). Now you acn login in and get an API key.

2. Get an API key from TMDB. Use [this link to get an API key](https://www.themoviedb.org/settings/api). When you fill out the form you can be inspired by this: <br/><br/> ![API key form](./images/tmdb_api_form.png)

3. Now you have an API key. You can use it to fetch data from the TMDB API. You can use the following URL in your favourite browser to get a list of movies:

    ```plaintext
    https://api.themoviedb.org/3/movie/popular?api_key=YOUR_API
    ```

    It should look like this (but with your API key - this one won't work):

    ```plaintext
    https://api.themoviedb.org/3/movie/popular?api_key=9d7597515aa9bc499ea280f761379de1
    ```

3. You will probably be familiar with IMDB for movies. <br/><br/> ![IMDB logo](./images/imdb_logo.svg)<br/><br/>
You can also find info on movies from IMDB through TMDB. Try this: Request the movie details using the **IMDB** `ID` of each movie. See more [here](https://developer.themoviedb.org/reference/find-by-id). Let's aquire data for the [Godfather movie at IMDB](https://www.imdb.com/title/tt0068646). You might check this screenshot to how you configure and run the request from within the themoviedb.org page:<br/><br/>
![The Godfather Movie Data](./images/godfather.png)

4. Now use the *TMDB API* to retrieve detailed information about movies based on their `titles` instead of `ID`. Begin by fetching the details for the movie `Godzilla` throught the web interface of TMDB and then contruct a url to insert in your browser including your api-key. This is just to get familiar with the API and how to use it. Look carefully at the json response and try to understand the structure of the data. Notice there are many fields in the response. We will only use a few of them. Also, since several movies are spinoffs of the original Godzilla movie, you might want to use the `release_year` field to filter the results or notice the `ID` of the movie you are looking for (try with 1954).

## Getting data from the API programmatically in Java (the slightly harder way)

Now the fun begins. We will use Java to fetch data from the TMDB API. We will use the `HttpClient` class to make the requests. We will also use the `ObjectMapper` class from the Jackson library to map the JSON response to DTOs.

5. Get the Movie `overview` from the API response and add it to a properly designed DTO.

6. Get the release date from the API response and add it to the DTO (as a `LocalDate`) and leave the release year as a `String`.

7. **Adding functionality**

- Add a new Class MovieController with the following methods:
  - `getByRating` that can take an MPAA rating or similar as a parameter and return all movies with that rating or lower or if you prefer, use the quality rating and find all movies with a specific rating e.g 8.5 and higher.
  - `getSortedByReleaseDate` that returns all movies sorted by release date descending.
- Make a generic interface for the class so it can be used for Books, Games, etc. as well.
- Write unit tests for the MovieController where you search for the following titles and persist them:
  - The Shawshank Redemption
  - The Godfather
  - The Dark Knight
  - The Godfather: Part II
  - The Lord of the Rings: The Return of the King
  - Pulp Fiction
  - 12 Angry Men
  - The Good, the Bad and the Ugly
  - Forrest Gump
  - Fight Club
  - Inception
- Then test the other methods in the MovieController.

<https://api.themoviedb.org/3/search/movie?api_key=API_KEY&query=Godzilla>