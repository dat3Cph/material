# Webscraping First Practise

## 1. Introduction

In this exercise you will be introduced to the concept of web-scraping. You will be introduced to the tools and libraries we 
have chosen to focus on, and you will get a chance to try them out.

## 2. Preparation

1. Create a new project in IntelliJ called `webscraping-first-practice`.
2. Add the following dependencies to your `pom.xml` file:

```xml
        <dependency>
            <groupId>org.jsoup</groupId>
            <artifactId>jsoup</artifactId>
            <version>1.16.1</version>
        </dependency>
```

3. Add a html file called `index.html` to your project. The content of the file should be:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Web Scraping Practice</title>
</head>
<body>
    <header>
        <h2>Web Scraping Practice</h2>
    </header>
    
    <h1>Welcome to Web Scraping Practice</h1>
    
    <div id="content">
        <p>This is a paragraph inside a div.</p>
        
        <ul>
            <li>Item 1</li>
            <li>Item 2</li>
            <li>Item 3</li>
        </ul>
        
        <a href="https://www.example.com">Visit Example.com</a>
    </div>
    
    <p>Random text for web scraping practice.</p>
    
    <a href="https://www.example.org">Visit Example.org</a>
    
    <p>More random text to scrape.</p>
    
    <table>
        <tr>
            <th>Name</th>
            <th>Age</th>
        </tr>
        <tr>
            <td>John</td>
            <td>30</td>
        </tr>
        <tr>
            <td>Alice</td>
            <td>25</td>
        </tr>
    </table>
    
    <footer>
        <p>&copy; 2023 Web Scraping Practice</p>
        <a href="https://www.facebook.com">Visit Facebook</a>
        <a href="https://www.instagram.com">Visit Instagram</a>
    </footer>
</body>
</html>
```

4. Add a class called `WebScrapingFirstPractice` to your project. This will be the class you will use to test out the tools and libraries.
5. Add the following code to the `main` method:

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.File;
import java.io.IOException;
import java.util.logging.Logger;

public class WebScrapingFirstPractice {

    private static final Logger logger = Logger.getLogger(WebScrapingFirstPractice.class.getName());

    public static void main(String[] args) {
        File input = new File("input.html");

        try {
            Document doc = Jsoup.parse(input, "UTF-8", "http://example.com/");

            // TODO: Extract and print the title of the HTML page.

            // TODO: Write code to find and print all the text within `<p>` tags on the page.

            // TODO: Extract and print all the URLs (href attributes) of the `<a>` tags on the page.

            // TODO: Exercise 3: Extract All Links

            // TODO: extract and print the data from the table as a structured format (e.g., as a list of name-age pairs).

            // TODO: Search for and print any paragraphs that contain the phrase "Random text" in their text content.

            // TODO: Modify your code to find and print only the URLs that contain "example" in their href attribute.

            // TODO: Extract and print the content of the `<header>` tag.

            // TODO: Find and print the text content of the `<div>` with the id "content" and all its nested elements.

            // TODO: Extract and print the text content of the `<footer>` tag.

        } catch (IOException e) {
            logger.warning(e.getMessage());
        }

    }
}
```

6. Finish the TODO tasks in the `main` method:


