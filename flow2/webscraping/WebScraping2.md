# Web Scraping continued ...

## Multiple requests with concurrency
[See the concurrency example](Concurrency.md)

## Pagination and navigation
Pagination is a web design and user interface (UI) pattern used to break up and display a large amount of content or data into smaller, more manageable chunks or pages. It is commonly used in websites and applications to improve user experience when dealing with lengthy lists, search results, or data sets. Pagination allows users to navigate through the content one page at a time.  
- Pagination typically includes navigation controls such as "Previous" and "Next" buttons or page numbers. These controls allow users to move forward and backward through the pages.
- Page indicators show users where they are within the overall content and how many pages are available. Common indicators include page numbers, a progress bar, or markers for the current page.
- Often the page is reflected in the URL, so that users can bookmark or share a specific page of content.

If the pagination is reflected in the url, it is easy to navigate to the next page by simply incrementing the page number in the url. Otherwise you need to find the pagination elements on the page and click the next button with a javascript executor (outside the scope of this course).

### Code example:

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.IOException;

public class PaginatedWebScraper {
    public static void main(String[] args) {
        String baseUrl = "https://example.com/articles?page=";
        int totalPages = 5; // Specify the total number of pages to scrape

        try {
            for (int page = 1; page <= totalPages; page++) {
                String pageUrl = baseUrl + page;

                Document doc = Jsoup.connect(pageUrl).get();

                // Select the elements containing the articles on the page
                Elements articleElements = doc.select(".article"); // Assuming articles have a class named "article"

                // Process and extract information from the article elements
                List<Article> articles = new ArrayList<>();
                for (Element articleElement : articleElements) {
                    String title = articleElement.select(".title").text();
                    String content = articleElement.select(".content").text();
                    articles.add(new Article(title, content));
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}

```

## REST API
As a supplement to webscraping we can use REST APIs to get data from the web. REST stands for Representational State Transfer and is a software architectural style that defines a set of constraints to be used for creating web services. Web services that conform to the REST architectural style, called RESTful Web services, provide interoperability between computer systems on the Internet. RESTful Web services allow the requesting systems to access and manipulate textual representations of Web resources by using a uniform and predefined set of stateless operations. Rest APIs are a more reliable source of data than webscraping, because the data is structured and the API is designed to be used by other applications, and therefore the data is more likely to be consistent and reliable. 

If a REST API is available containing some data that can supplement your webscraping, you should always use the API instead of webscraping, to the extend that the API contains the data you need.

### Example:
The following example shows how to use the [OpenWeatherMap API](https://openweathermap.org/current) to get the current weather for a city. The API is free to use, but you need to sign up to get an API key. The API key is used to authenticate your requests to the API. 

```java

```