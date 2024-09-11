---
title: The Movie Database API
description: Java Deep Dive II Exercise DTO and JSON
layout: default
nav_order: 5
has_children: false
grand_parent: Java Deep Dive II
parent: Exercises
permalink: /deepdive-2/exercises/api-to-dto/
---
<br/>
![TMDB logo](./images/blue_long.svg)

# Reading data from a Rest API into DTOs

In this exercise we want to read data from a Rest API and map it to DTOs. We will use the [The Movie Database API - TMDb](https://developer.themoviedb.org/reference/intro/getting-started) to fetch information about movies. We will then map the data to DTOs. And finally, we will add some functionality to operate on the DTOs.

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

## Getting data from the API programmatically in Java <br/>

(the slightly harder - but cooler and more useful way)

In these exercises you will need to use your api-key to fetch data from the TMDB API. However, we don't want to type the api-key explicitly in the code. Instead, we will enter the api-key in IntelliJ IDEA as a environment variable. This is a more secure way to handle sensitive information. We did the same trick on 2nd semester:

![env](./images/api_1.png)
![env](./images/api_2.png)
![env](./images/api_3.png)

Then from Java you can access the environment variable like this:

```java
String apiKey = System.getenv("API_KEY");
```

That's it. Then we can avoid pushing the api-key to the repository.

Now the fun begins. We will use Java to fetch data from the `TMDB API`. We will use the [`HttpClient`](../../toolbox/dataintegration/httpclient.md) class to make the requests. We will also use the `ObjectMapper` class from the [Jackson library](../../toolbox/dataintegration/jackson.md) to [map](../../toolbox/dataintegration/dto_conversion.md) the [JSON](../../toolbox/dataintegration/json.md) response to [DTOs](../../toolbox/designpatterns/dto.md).

The plan is to fetch some moviedata from the TMDB API and map it to a MovieDTO. We will then add some functionality that can operate on the MovieDTOs.

1. Get the Movie `overview` from the API response (for a particular `ID`) and add it to a properly designed MovieDTO. The result is to be able to print out the `overview` from, let's say "Mifunes sidste sang" (id=139). If you work with pair programming, one person can write the DTOs and the other can write the code to fetch the data from the API. Also, when working together with another team of two, you can let the other team take the next exercise (2). However, you should all work together and share the same DTO's. This endpoint will get you going: [https://developer.themoviedb.org/reference/movie-details](https://developer.themoviedb.org/reference/movie-details)

2. This exercise is about expanding on the MovieDTO. We want get the release date from the API response and add it to the MovieDTO (as a `LocalDate`). This can be achieved by adding an extra `JavaTimeModule` to the Jackson `ObjectMapper`. Like this:

      ```java
      objectMapper.registerModule(new JavaTimeModule());
      ```

      We also need you to make a getter method, `getReleaseYear()`, that can return the release year as a `String`. So the result of this exercise is to be able to print out the release year of the movie "Mifunes sidste sang" (id=139) and others.

3. **Adding functionality**

    Add a new class `MovieService` with the following methods:

    - Refactor your from above, so you can fetch the movie data from the API by `id` and return a `MovieDTO` object. Call the method `getMovieById` and make sure it returns a `MovieDTO` object.

    - `getByRating` that can take a rating/voting or similar as a parameter and return all movies with that rating between a lower and upper rating. Find all movies with a specific rating betwee 8.5 and 9.0. You will need to return the movies in a List of MovieDTOs. You might need to consult chatGPT for the best way to do this. Also notice, that the resulting json might contain many pages of movies. You can use the `page` parameter to navigate through the pages. You can also use the `vote_average.gte` and `vote_average.lte` parameters to filter the results. This endpoint will get you there: [https://developer.themoviedb.org/reference/discover-movie](https://developer.themoviedb.org/reference/discover-movie)

    - `getSortedByReleaseDate` that takes a query string and returns all movies sorted by release date descending. You will need to return the movies in a List of MovieDTOs. And then use a Java stream to sort the movies by release date.

    - Write unit/integration tests for the `MovieService` where you search for the following titles tests the result agains the expected out result. Make a strategy for how to test the methods in the MovieService class:

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

    - Then test the other method in the `MovieService` class.

4. **Extra**

- Add a methods to the `MovieService` that you find useful.
