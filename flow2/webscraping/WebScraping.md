# Web scraping with Java
Web scraping serves various purposes, and its applications are wide-ranging. Some common purposes and use cases for web scraping include:
- Data Collection for Research: Researchers often use web scraping to gather data for studies and analysis. This can include collecting data on market trends, social media sentiment, scientific publications, and more.
- Competitive Intelligence: Businesses use web scraping to monitor competitors' prices, product offerings, and customer reviews. This information can inform pricing strategies and product development.
- Lead Generation: Sales and marketing professionals scrape websites and social media profiles to collect contact information for potential leads and customers.
- Content Aggregation: News websites, blogs, and content aggregators use web scraping to collect and display articles, news, and other content from various sources.
- and many more ...

## The Challenges of Web Scraping
Web scraping is a powerful tool for collecting data from the web, but it comes with its own set of challenges. Some of the common challenges of web scraping include:
- **Dynamic Content:** Many websites load content dynamically using JavaScript. This can make it difficult to scrape the content using traditional methods. You may need to use a headless browser or additional tools to scrape dynamic content.
- **Website Changes:** Websites are constantly changing, and even minor changes to the website structure can break your scraping code. You'll need to regularly maintain your code to accommodate website changes.
- **Data Cleaning and Transformation:** The data you scrape from websites may not be in the format you need. You may need to clean and preprocess the data to remove unnecessary elements, format it, and convert data types.
- **Error Handling:** Your web scraping code may encounter errors, such as network failures, invalid HTML, or unexpected changes to the website structure. You'll need to develop strategies to handle these errors and ensure your code is robust.

## HTML and CSS for selecting elements
When web scraping, you traverse the Document Object Model (DOM) of a web page to locate and extract specific data or elements. The DOM is a structured representation of a webpage's content, organized as a tree-like structure of HTML elements. Here's a step-by-step description of the process of traversing the DOM during web scraping:

1. **Sending an HTTP Request:**
   - The process begins by sending an HTTP request to the URL of the webpage you want to scrape. This request retrieves the HTML content of the page from the web server.

2. **Parsing the HTML:**
   - Once the HTML content is retrieved, it needs to be parsed. Commonly used libraries for HTML parsing in various programming languages include Jsoup (Java), Beautiful Soup (Python), and Nokogiri (Ruby).
   - The parsed HTML is then represented as a tree-like structure, with each HTML element represented as a node in the tree.

3. **Selecting Elements:**
   - To extract specific data, you need to navigate this tree. You start by selecting the elements that contain the data you're interested in.
   - This is often done using CSS selectors, XPath expressions, or other methods provided by the parsing library. [See difference here](https://www.testim.io/blog/xpath-vs-css-selector-difference-choose/)
   - For example, you might select all the `<a>` tags (links) on the page, or find elements with specific class attributes.

4. **Traversing the DOM Tree:**
   - Once you've selected an element, you can traverse the DOM tree in various ways to access its children, siblings, or parent elements.
   - Common traversal methods include finding child elements, moving up to parent elements, and iterating through siblings.
   - For example, you might find all the `<li>` elements within an ordered list `<ol>` or navigate to the parent `<div>` of a specific paragraph `<p>`.
   - In most browsers you can right-click on an element and choose: inspect element. This will open the developer tools and highlight the element in the DOM tree. Now you can copy either the CSS selector or the XPath expression.

5. **Accessing Element Attributes and Text:**
   - After locating the desired elements, you can access their attributes (e.g., `href`, `src`, `class`) and extract text content.
   - For instance, you can retrieve the URL of a link (`<a>`) by accessing its `href` attribute or get the text inside a paragraph (`<p>`) by accessing its `textContent`.

6. **Data Extraction:**
   - Once you have accessed the attributes and text content of the elements, you can extract and store the data in variables or data structures for further processing or analysis.
   - Data extraction might involve cleaning and formatting the data to make it usable for your specific application.

7. **Iterating and Repeating:**
   - Depending on your scraping requirements, you may need to repeat the process by iterating over multiple elements or pages.
   - For example, you might scrape data from a list of search results or paginated content, iterating through each page's HTML.

8. **Error Handling and Validation:**
   - Throughout the process, it's essential to implement error handling to deal with issues such as missing elements or unexpected changes to the webpage structure.
   - Validation is also crucial to ensure that the extracted data meets your quality and accuracy standards.

By systematically traversing the DOM and selecting the relevant elements, we can efficiently extract the data you need from web pages during the web scraping process.

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

### Selecting elements
Here are some code examples of how we can use CSS selectors to select elements from the HTML document:

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

public class JsoupCSSSelectorsExample {
    public static void main(String[] args) {
        String html = "<html><body>" +
                      "<div class='container'>" +
                      "   <h1 id='title'>Hello, World!</h1>" +
                      "   <ul>" +
                      "       <li>Item 1</li>" +
                      "       <li>Item 2</li>" +
                      "   </ul>" +
                      "  <a href='#'>Link</a>" +
                      "  <p class='info'>This is some information.</p>" +
                      "</div></body></html>";

        Document document = Jsoup.parse(html);

        // Tag Selector
        Elements divElements = document.select("div");
        System.out.println("Div Elements: " + divElements);

        // Class Selector
        Elements infoParagraphs = document.select(".info");
        System.out.println("Info Paragraphs: " + infoParagraphs);

        // ID Selector
        Element titleElement = document.select("#title").first();
        System.out.println("Title Element: " + titleElement.text());

        // Descendant Selector
        Elements listItems = document.select("div ul li");
        System.out.println("List Items: " + listItems);

        // Child Selector
        Elements listItemsDirectChildren = document.select("div > ul > li");
        System.out.println("List Items (Direct Children): " + listItemsDirectChildren);

        // Attribute Selector
        Element anchorWithHref = document.select("a[href]").first();
        System.out.println("Anchor with Href: " + anchorWithHref);

        // Pseudo-Class Selector (e.g., :first-child)
        Element firstListItem = document.select("li:first-child").first();
        System.out.println("First List Item: " + firstListItem.text());
    }
}
```

## Data extraction using Regular Expressions
Source: https://www.w3schools.com/java/java_regex.asp
" A regular expression is a sequence of characters that forms a search pattern. When you search for data in a text, you can use this search pattern to describe what you are searching for.
A regular expression can be a single character, or a more complicated pattern."

Regular expressions can be very powerful for parsing and extracting specific patterns from HTML pages. Here are some common regex examples along with explanations for working with HTML content:

1. **Extract All Links (HREF Attributes):**
   - Regex: `<a[^>]*href=["'](https?[^"']+)["']`
   - Explanation: This regex is designed to capture all anchor (`<a>`) tags and extract the URLs (HREF attributes) within them.
   - `<a[^>]*`: Matches the opening `<a>` tag, allowing for any attributes between `<a` and `>`.
   - `href=["'](https?[^"']+)["']`: Captures the HREF attribute value (the URL) inside double or single quotes. It matches both HTTP and HTTPS URLs.

2. **Extract All Email Addresses:**
   - Regex: `[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}`
   - Explanation: This regex is designed to match common email address patterns within HTML content.
   - `[a-zA-Z0-9._%+-]+`: Matches the username part of the email address.
   - `@`: Matches the "@" symbol.
   - `[a-zA-Z0-9.-]+`: Matches the domain name part of the email address.
   - `\.`: Matches the dot separating the domain name and top-level domain (TLD).
   - `[a-zA-Z]{2,}`: Matches the TLD, requiring at least two letters.

3. **Extract All Image URLs (SRC Attributes):**
   - Regex: `<img[^>]*src=["'](https?[^"']+)["']`
   - Explanation: Similar to the link example, this regex captures all image (`<img>`) tags and extracts the image URLs (SRC attributes).
   - `<img[^>]*`: Matches the opening `<img>` tag, allowing for any attributes between `<img` and `>`.
   - `src=["'](https?[^"']+)["']`: Captures the SRC attribute value (the image URL) inside double or single quotes. It matches both HTTP and HTTPS URLs.

4. **Extract All HTML Comments:**
   - Regex: `<!--(.*?)-->`
   - Explanation: This regex captures HTML comments, including their content.
   - `<!--`: Matches the start of an HTML comment.
   - `(.*?)`: Captures the content of the comment (including newlines and other characters).
   - `-->`: Matches the end of an HTML comment.

5. **Extract Text Inside HTML Tags (e.g., Headings):**
   - Regex: `<h[1-6][^>]*>(.*?)<\/h[1-6]>`
   - Explanation: This regex captures text within heading tags (e.g., `<h1>`, `<h2>`) along with the tag itself.
   - `<h[1-6][^>]*>`: Matches the opening tag of headings from `<h1>` to `<h6`, allowing for any attributes.
   - `(.*?)`: Captures the content of the heading.
   - `<\/h[1-6]>`: Matches the closing tag of headings.

6. **Extract URLs within JavaScript or CSS Code:**
   - Regex: `(?:href=|src=|url\()[ '"]?(https?[^'" )]+)`
   - Explanation: This regex captures URLs within JavaScript or CSS code by looking for common patterns like `href=`, `src=`, or `url()`.
   - `(?:...)`: Represents a non-capturing group.
   - `href=|src=|url\(`: Matches common URL-related patterns.
   - `[ '"]?`: Handles optional spaces or quotes.
   - `(https?[^'" )]+)`: Captures the URL itself.

7. **Extract All HTML Tags and Their Attributes:**
   - Regex: `<([a-zA-Z0-9\-]+)([^>]*)>`
   - Explanation: This regex captures all HTML tags and their attributes. You can further parse the attributes if needed.
   - `<([a-zA-Z0-9\-]+)`: Matches the opening tag, allowing for alphanumeric characters and hyphens in the tag name.
   - `([^>]*)`: Captures any attributes inside the tag.

8. **Extract All Phone Numbers (US Format):**
   - Regex: `\b\d{3}[-.]?\d{3}[-.]?\d{4}\b`
   - Explanation: This regex matches US phone numbers in various common formats (e.g., 555-555-5555, 555.555.5555).
   - `\b`: Word boundary to ensure whole number matches.
   - `\d{3}[-.]?\d{3}[-.]?\d{4}`: Matches the phone number patterns, allowing for optional hyphens or periods as separators.

9. **Extract Social Media Profile Links:**
   - Regex: `<a[^>]*href=["'](https?:\/\/(www\.)?twitter\.com\/[^"']+)["']`
   - Explanation:

It is important to notice, that while regular expressions can be helpful for basic parsing of HTML content, they are not a recommended approach for parsing complex HTML documents. For parsing and traversing HTML documents, it's usually better to use dedicated HTML parsing libraries like Jsoup, which offer more robust and structured solutions. But for getting specific data from HTML (large) elements that are not easily accessible using CSS selectors, regular expressions can be a useful tool.
