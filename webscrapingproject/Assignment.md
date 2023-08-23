# Flow 2 Week Assignment: Weather Data Enrichment and Storage
This exercise focuses on web scraping, JPA, DTOs, reading from a REST API, and testing, spread over 5 working days:

## Requirements
This project is meant to be a group exercise and the scope is 5 working days. The requirements are as follows:

1. Choose a website that provides some interesting data that you can scrape daily.
2. Scrape the data from the website and using both JSoup and Selenium.
3. Enrich the data by fetching additional information from a REST API.
4. Store the data in a database using JPA.
5. Write unit tests for scraping, enrichment, and API reading logic using JUnit.

If you are unsure about finding a website to scrape, you can use the following example:
## Weather Data project

**Day 1: Web Scraping and DTOs**

- Choose a weather website to scrape daily weather forecasts.
- Use Jsoup to scrape the weather data for a specific location and date.
- Create a DTO class (e.g., `WeatherDTO`) to represent the weather data.
- Extract relevant weather data such as temperature, humidity, and conditions and map it to the DTO.

**Day 2: Enrichment, API Reading, and Unit Testing**

- Implement logic to enrich the scraped weather data using a weather API (e.g., OpenWeatherMap API).
- Create a Java class (e.g., `WeatherApiReader`) to interact with the API and fetch additional weather information.
- Write unit tests for scraping, enrichment, and API reading logic using JUnit and Mockito.

**Day 3: JPA Setup and Entity**

- Set up a local database (e.g., H2 or MySQL) for storing weather data.
- Create an entity class (e.g., `WeatherEntity`) to represent the data in the database.
- Use JPA annotations to map the entity to the database schema.
- Implement a JPA DAO interface for the weather entity, with methods like: `getAll`, `getYesterday`, `update(LocalDate date)` etc.
- Write unit tests for the JPA DAO. 
- Write code to convert the enriched DTO data into the JPA entity.
- Save the enriched weather data to the database using JPA repository methods.

**Day 4: Finalize and Document**

- Complete integration testing, ensuring all components work cohesively.
- Fine-tune your code, refactor, and optimize where necessary.
- Write documentation, including explanations of components and interactions.
- Consider edge cases, error handling, and potential improvements.
- Prepare a presentation to demonstrate your work for the review on friday

By following this 4-day exercise plan, you'll be able to develop a weather data enrichment and storage program that incorporates web scraping, JPA, DTOs, reading from a REST API, and testing practices. This condensed exercise will provide your group with a focused hands-on experience in each of these areas.