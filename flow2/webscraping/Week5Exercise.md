# Web scraping a movie site
This exercise combines web scraping using Jsoup, and reading data from a REST API into DTOs (Data Transfer Objects). 
This exercise simulates scraping information about movies from a website and then enriching the data with additional information from a movie database API.

**Exercise: Movie Data Enrichment**

1. **Web Scraping:**
We want to scrape a website that lists movie titles of the top 250 most popular movies (https://www.imdb.com/chart/top/?ref_=nv_mv_250) and titles plus their ratings. 
   - Use Jsoup to fetch the initial page content.
   - Select the elements containing the movie titles, thumbnail images, ratings etc.
   - Extract each movie into a DTO containing the following fields:
     - IMDB_id (e.g., tt0111161)
     - Title
     - Thumbnail image URL
     - Rating
     - Number of ratings
     - Release year
     - MPAA rating (e.g., PG-13)
     - Duration 

2. **API Data Retrieval and DTOs:**
After obtaining the movie titles and ratings from the website, you'll enrich the data by fetching additional information from a movie database API. Here's what you can do:

- Use a movie database API (e.g., The Movie Database API - TMDb: https://developer.themoviedb.org/reference/intro/getting-started) to retrieve detailed information about movies based on their titles.
- Sign up for the movie database API and obtain an API token for making requests. (They ask for a lot of info, but only the email has to be real.)
- Request the movie details using the IMDB id of each movie. See more [here](https://developer.themoviedb.org/reference/find-by-id).
- Get the Movie `overview` from the API response and add it to the DTO.
- Get the release date from the API response and add it to the DTO (as a `LocalDate`) and leave the release year as a `String`.

3. **Persistence**
Now setup a new database and the necessary classes to persist the data including the necessary maven dependencies in the POM.xml file.
- Create a JPA entity class (e.g., `MovieEntity`) to represent the data in the database.
- Create a JPA DAO interface for the movie entity, with methods like: 
  - `getAll`, 
  - `getByImdbId`, 
  - `update`, 
  - `delete`, 
  - `persist` and
  - `getByRating` that can take an MPAA rating or similar as a parameter and return all movies with that rating or lower or if you prefer, use the quality rating and find all movies with a specific rating e.g 8.5 and higher.
- Make the interface generic so it can be used for Books, Games, etc. as well.
- Implement the DAO interface using JPA and Hibernate with MovieEntity as the entity class.
- Write unit tests for the JPA DAO where you search for the following titles and persist them:
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
- Then test the other methods in the DAO interface.