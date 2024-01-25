# Exercises for Week 5: Web Scraping with Java
## Monday: Web Scraping
This exercise focuses on web scraping static content using Jsoup and regular expressions. In this exercise, you'll scrape and extract data from a webpage containing static content, such as news articles, and use regular expressions to refine and clean the extracted data.

## Exercise 1 
Web Scraping and Data Extraction with Jsoup and Regular Expressions

**Objective:** Build a Java program that scrapes data from here: `https://en.wikipedia.org/wiki/Women_in_computing`. We will be using Jsoup, and then `regular expressions` to clean and extract specific information from the scraped content.

**Requirements:**

1. **Initial Setup:**
   - Create a new Java project in IntelliJ IDEA.
   - Set up the Java project with the Jsoup dependency.

2. **Web Scraping:**
   - Use Jsoup to fetch and parse the HTML content of the webpage.

3. **Data Extraction:**
   - Answer the following questions by extracting data from the html source code:
     - How many references are there in the article?
     - How many references are there in the article that contain the word "computer"?
     - How many h3 headers are there on the page?
     - Can you select the the text comming after the h3? Create a map with key: h3 text, value: text after h3.

4. **Regular Expressions:**
   - Within the section: "1800s", how many names are there (regex to find names like Firstname Lastname, starting with a capital letter)?
   - Use groups in your regular expressions to capture only the last name of each name.

5. **Data Cleaning:**
   - Implement data cleaning functions to process the extracted data (e.g., remove HTML tags, trim whitespace).
   - Ensure that the extracted data is in a clean and usable format.

## Exercise 2
Wednesday: Concurrency and Json data
In this exercise, you'll scrape data from `amazon.com`: a paginated website, clean the data, and handle errors that may arise during the process.

**Exercise: Scraping, Cleaning, Error Handling, and Pagination**

**Objective:** Build a web scraping program that extracts product information from the amazon website. The website has multiple pages of product listings, and the goal is to scrape data from each page, clean it, and handle any errors that occur during the process.

**Requirements:**

1. **Initial Setup:**
   - Set up a Java project with Jsoup dependency.
   - Load the initial page of the amazon website.

2. **Scraping and Pagination:**
   - Write code to scrape product information (e.g., name, price, description) from the current page using Jsoup.
   - Implement logic to navigate to the next page using pagination informantion in the url, until there are no more pages to scrape.

3. **Data Cleaning:**
   - Implement data cleaning functions to remove unwanted characters, format prices, and sanitize descriptions.
   - Ensure that the scraped data is in a clean and usable format.

4. **Error Handling:**
   - Implement error handling for common issues that may occur during scraping, such as network errors or element not found errors.
   - Log errors and continue scraping from where the error occurred, if possible.

5. **Data Storage:**
   - Store the scraped data in the database using the proper data model.

6. **Testing:**
   - Write unit tests to verify the functionality of your data cleaning and error handling functions.
   - Test the program with various scenarios, including scenarios where errors are intentionally introduced.