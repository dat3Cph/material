---
title: JSON DTO Exercise
description: Java Deep Dive II Exercise DTO and JSON
layout: default
nav_order: 1
has_children: false
grand_parent: Java Deep Dive II
parent: Exercises
permalink: /deepdive-2/exercises/api-to-dto/
---

# Reading data from a Rest API into DTOs

1. **API Data Retrieval and DTOs:**
Fetch information from a movie database API. Here's what you can do:

- Use a movie database API (e.g., The Movie Database API - TMDb: <https://developer.themoviedb.org/reference/intro/getting-started>) to retrieve detailed information about movies based on their titles.
- Sign up for the movie database API and obtain an API token for making requests. (They ask for a lot of info, but only the email has to be real.)
- Request the movie details using the IMDB id of each movie. See more [here](https://developer.themoviedb.org/reference/find-by-id).
- Get the Movie `overview` from the API response and add it to a properly designed DTO.
- Get the release date from the API response and add it to the DTO (as a `LocalDate`) and leave the release year as a `String`.

3. **Adding functionality**

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
