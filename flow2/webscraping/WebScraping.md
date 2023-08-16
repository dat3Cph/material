# Web scraping with Java
## HTML and CSS for selecting elements
- Navigate the DOM tree:
https://jsoup.org/cookbook/extracting-data/dom-navigation

## Jsoup
Maven dependency:
```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.16.1</version> <!-- Check for the latest version -->
</dependency>
```


## Fetching web content and parsing HTML
```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import java.io.IOException;

public class WebContentFetcher {
    public static void main(String[] args) {
        String url = "https://example.com"; 
        String htmlContent = "<html><body><div class='my-class'>Hello, <span>World!</span></div></body></html>";

        try {
            // Fetch the webpage content
            Document document = Jsoup.connect(url).get();
            // Parse the HTML content
            Document document2 = Jsoup.parse(htmlContent);

             // Select and print the text of the <span> element
            Element spanElement = document.select("span").first();
            if (spanElement != null) {
                System.out.println("Text inside <span>: " + spanElement.text());
            }

            // Print the fetched HTML content
            System.out.println(document);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

## CSS selectors
https://jsoup.org/cookbook/extracting-data/selector-syntax

## Data extraction

## Using Regular Expressions
