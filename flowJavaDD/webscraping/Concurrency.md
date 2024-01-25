# Crawl or visit multiple pages using threads
To crawl multiple web links concurrently using threads in Java, you can use the `ExecutorService` and `Callable` interface from the Java Concurrency framework. Here's an example that demonstrates how to do this:

```java
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.*;

public class WebCrawler {
    public static void main(String[] args) {
        // List of URLs to crawl
        List<String> urlsToCrawl = new ArrayList<>();
        urlsToCrawl.add("https://example.com/page1");
        urlsToCrawl.add("https://example.com/page2");
        urlsToCrawl.add("https://example.com/page3");
        // Add more URLs as needed

        // Number of concurrent threads to use
        int numThreads = urlsToCrawl.size();

        // Create an ExecutorService with a thread pool
        ExecutorService executorService = Executors.newFixedThreadPool(numThreads);

        // Create a list to hold future results
        List<Future<String>> futures = new ArrayList<>();

        // Submit tasks for each URL
        for (String url : urlsToCrawl) {
            Callable<String> callable = new WebCrawlTask(url);
            Future<String> future = executorService.submit(callable);
            futures.add(future);
        }

        // Process the results when each task is done
        for (Future<String> future : futures) {
            try {
                String result = future.get(); // Get the result of the task
                System.out.println("Crawled: " + result);
            } catch (InterruptedException | ExecutionException e) {
                e.printStackTrace();
            }
        }

        // Shutdown the executor service
        executorService.shutdown();
    }
}

class WebCrawlTask implements Callable<String> {
    private final String url;

    public WebCrawlTask(String url) {
        this.url = url;
    }

    @Override
    public String call() throws Exception {
        // Replace this with your web crawling logic
        try {
            // Simulate web crawling by sleeping for a while
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        return url; // Return the crawled URL as the result
    }
}
```

In this example:

1. We have a list of URLs to crawl (`urlsToCrawl`) and specify the number of concurrent threads (`numThreads`) to use.

2. We create an `ExecutorService` with a fixed thread pool size to manage the threads.

3. We submit tasks for each URL to the executor service. Each task is represented by the `WebCrawlTask` class, which implements the `Callable` interface. The `WebCrawlTask` class defines the web crawling logic for each URL.

4. We store the `Future` objects returned by the `submit` method in a list (`futures`) to keep track of the results.

5. We iterate through the `futures` list and retrieve the results of each task when it's done. In this example, we simply print the crawled URL, but you can replace this with your web scraping logic.

6. Finally, we shut down the executor service when we're done with all the tasks.