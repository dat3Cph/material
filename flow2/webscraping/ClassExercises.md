# Exercises for Week 5: Web Scraping with Java
## Monday: Web Scraping
This exercise focuses on web scraping static content using Jsoup and regular expressions. In this exercise, you'll scrape and extract data from a webpage containing static content, such as news articles, and use regular expressions to refine and clean the extracted data.

**Exercise: Web Scraping and Data Extraction with Jsoup and Regular Expressions**

**Objective:** Build a Java program that scrapes data from here: `https://en.wikipedia.org/wiki/Women_in_computing`. We will be using Jsoup, and then `regular expressions` to clean and extract specific information from the scraped content.

**Requirements:**

1. **Initial Setup:**
   - Set up a Java project with the Jsoup dependency.

2. **Web Scraping:**
   - Choose a webpage containing static content (e.g., a news article).
   - Use Jsoup to fetch and parse the HTML content of the webpage.

3. **Data Extraction:**
   - Identify specific pieces of information you want to extract from the webpage. This can include the article title, author, publication date, and article content. 

4. **Regular Expressions:**
   - Write regular expressions to match and extract the desired information from the HTML content.
   - Use groups in your regular expressions to capture different parts of the data (e.g., title, author, date). Hint: see example [Here](RegularExpressions.md#example)

5. **Data Cleaning:**
   - Implement data cleaning functions to process the extracted data (e.g., remove HTML tags, trim whitespace).
   - Ensure that the extracted data is in a clean and usable format.

6. **Display or Store Data:**
   - Choose whether to display the extracted data in the console or store it in a file or data structure for further use.

7. **Testing:**
   - Test your regular expressions and data cleaning functions with various articles to ensure they work correctly.

8. **Documentation:**
   - Document your code, including explanations of each component and how to run the program.
   - Include comments to describe the purpose of each regular expression and data cleaning step.

**Time Allocation:**

This exercise provides a hands-on experience in web scraping static content with Jsoup and using regular expressions to extract and clean data. It's a valuable skill for extracting structured information from websites that may not offer APIs or structured data formats.

## Wednesday: Dynamic Content and Testing
Exercise that combines Selenium and Jsoup for web scraping, focusing on data cleaning, error handling, and pagination.
In this exercise, you'll scrape data from `amazon.com`: a paginated website, clean the data, and handle errors that may arise during the process.

**Exercise: Scraping, Cleaning, Error Handling, and Pagination**

**Objective:** Build a web scraping program that extracts product information from the amazon website. The website has multiple pages of product listings, and the goal is to scrape data from each page, clean it, and handle any errors that occur during the process.

**Requirements:**

1. **Initial Setup:**
   - Set up a Java project with Selenium and Jsoup dependencies.
   - Configure Selenium to use a WebDriver (e.g., ChromeDriver).
   - Load the initial page of the e-commerce website.

2. **Scraping and Pagination:**
   - Write code to scrape product information (e.g., name, price, description) from the current page using Jsoup.
   - Implement logic to navigate to the next page using Selenium (pagination) until there are no more pages to scrape.

3. **Data Cleaning:**
   - Implement data cleaning functions to remove unwanted characters, format prices, and sanitize descriptions.
   - Ensure that the scraped data is in a clean and usable format.

4. **Error Handling:**
   - Implement error handling for common issues that may occur during scraping, such as network errors or element not found errors.
   - Log errors and continue scraping from where the error occurred, if possible.

5. **Data Storage:**
   - Choose a data storage option (e.g., in-memory list, CSV file, database) to store the cleaned product data.

6. **Testing:**
   - Write unit tests to verify the functionality of your data cleaning and error handling functions.
   - Test the program with various scenarios, including scenarios where errors are intentionally introduced.

7. **Documentation:**
   - Document your code, including explanations of each component and how to run the program.
   - Include comments to describe the purpose of each function and block of code.

This exercise provides a comprehensive hands-on experience with web scraping, data cleaning, error handling, pagination, and testing using Selenium and Jsoup. It's a practical way to improve your skills in handling real-world web scraping scenarios.