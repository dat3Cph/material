# Flow 2 Week Assignment: Weather Data Enrichment and Storage

Today, data can potentially be worth a lot of money. However, data are usually spread all over the internet. 
A common usecase is to collect, store, and enrich data from various sources. API's, webpages etc.  

In this exercise we will train how to do that using JPA, DTOs, web scraping, and REST API's.

## Requirements

This project is meant to be a group exercise and the scope is 4 working days. The requirements are as follows:

1. Choose a website that provides some interesting data that you can scrape daily.
2. Scrape the data from the website and using JSoup.
3. Enrich the data by fetching additional information from a REST API.
4. Store the data in a database using JPA.
5. Write unit tests for scraping, enrichment, and API reading logic using JUnit.
6. Use DTOs to represent the data.
7. Use as many of the concepts you have learned as possible as functional programming, streams, lambdas, generics etc.
7. Write documentation for the project.

If you are unsure about finding a website to scrape, you can use the following example:
## Weather Data project

**Day 1: Web Scraping and DTOs**

- Choose a weather website to scrape daily weather forecasts.
- Use Jsoup to scrape the weather data for a specific location and date.
- Create a DTO class (e.g., `WeatherDTO`) to represent the weather data.
- Extract relevant weather data such as temperature, humidity, and conditions and map it to the DTO.

**Day 2: Enrichment, API Reading, and Unit Testing**

- Implement logic to enrich the scraped weather data using a weather API (OpenWeatherMap API) and add additional data/info regarding geographical destinations. 
    - https://dawadocs.dataforsyningen.dk/dok/api/sted or
    - https://vejr.eu/pages/api-documentation
- Create a Java class (e.g., `WeatherApiReader`) to interact with the API and fetch additional weather information.
- Write unit tests for scraping, enrichment, and API reading logic using JUnit.

**Day 3: JPA Setup and Entity**

- Set up a local database (PostgreSql) for storing weather data.
- Create an entity class (e.g., `WeatherEntity`) to represent the data in the database.
- Use JPA annotations to map the entity to the database schema.
- Implement a JPA DAO interface for the weather entity, with methods like: `getAll`, `getYesterday`, `update(LocalDate date)` etc.
- Write test for the JPA DAO. 
- Write code to convert the enriched DTO data into the JPA entity.
- Save the enriched weather data to the database using JPA repository methods.

**Day 4: Finalize and Document**

**Refactoring**
- Complete testing, ensuring all components work cohesively.
- Fine-tune your code, refactor, and optimize where necessary.

**Documentation**
- Write documentation like a EER Diagram including links and names of the used api's and pages that are used for web scraping.
- Consider edge cases, error handling, and potential improvements.
- Prepare a presentation to demonstrate your work for the review on friday

