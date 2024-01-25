# Regular expressions
## Introduction
Regular expressions are a powerful tool for matching patterns in text. This page gives a basic introduction to regular expressions themselves sufficient for our JSoup exercises and shows how regular expressions work.

## Example
The following example illustrates the use of regular expressions in Java. The example finds all the image names on the wiki page and prints them out.

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class WikipediaImageNameExtractor {
    public static void main(String[] args) {
        try {
            // Define the URL of the Wikipedia page
            String url = "https://en.wikipedia.org/wiki/Women_in_computing";

            // Fetch the page content using Jsoup
            Document document = Jsoup.connect(url).get();

            // Use Jsoup to select all image elements
            Elements imgElements = document.select("img");

            // Define a regular expression pattern to match image filenames
            Pattern pattern = Pattern.compile("/([^/]+)$");

            // Initialize a StringBuilder to store image names
            StringBuilder imageNames = new StringBuilder();

            // Iterate through image elements and apply the regular expression
            for (Element imgElement : imgElements) {
                // Get the "src" attribute of the image element
                String imgSrc = imgElement.attr("src");

                // Match the pattern against the "src" attribute
                Matcher matcher = pattern.matcher(imgSrc);

                // If a match is found, append the image name to the StringBuilder
                if (matcher.find()) {
                    String imageName = matcher.group(1); // Group 1 contains the image name
                    imageNames.append(imageName).append("\n");
                }
            }

            // Print the extracted image names
            System.out.println("Extracted Image Names:");
            System.out.println(imageNames.toString().trim());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
