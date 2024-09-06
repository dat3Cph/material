# Threads exercises
- All exercises should use Executors and not be coded with threads directly.

### Exercise 1.

- Write a proram where the main thread creates a number of tasks for an ExecutorService. The first task should print `AAA`, the next `BBB`,`CCC` etc. up to `ZZZ` (there are 25 characters in total). There should be 4 worker threads in the executor service.

### Exercise 2.

- Read up on the concept of 'synchronized' (for example this page "<http://tutorials.jenkov.com/java-concurrency/synchronized.html>").  
- Fix the below code so that the Counter class´s increment method is thread safe:
```java
private static class Counter {
        private int count = 0;

        // Method to increment the count, synchronized to ensure thread safety
        public synchronized void increment() {
            count++;
        }

        // Method to retrieve the current count value
        public int getCount() {
            return count;
        }
    }
```

### Exercise 3.
- Look at the code in this class: https://github.com/HartmannDemoCode/ThreadsDemo/blob/main/src/main/java/dk/cphbusiness/exercises/AddingNumbers.java. It inserts a number into an ArrayList and prints out the size of the list. The list does not always contain a thousand numbers. Why is that? Propose a solution. 
- See if you can come up with a solution that does not use synchronized.

### Exercise 4.
- Most operating systems have a program that shows the performance of the system (windows: taskmanager, mac: activity monitor, linux: System Monitor).
- Create a variation of one of the Executor programs that puts all your cores to work.

### Exercise 5. (ekstra)

- Look at this [list](http://www.javainterview.in/p/java-synchronization-interview-questions.html) of questions for general knowledge about threads. There are new areas here that you can explore on your own if you have time and energy :-)

### Exercise 6. 
- Create a program to get data from 10 differenct web services (APIs) at the same time.
- Get the returned value from the web service and save it in DTOs.
- Collect all the DTO data in a mega DTO and print it out in a nice format.
- Examples of APIs to use:
```java
String[] urls = new String[]{
    "https://icanhazdadjoke.com/api",
    "https://api.chucknorris.io/jokes/random",
    "https://api.kanye.rest",
    "https://api.whatdoestrumpthink.com/api/v1/quotes/random",
    "https://api.spacexdata.com/v5/launches/latest"
};
```
- [More APIs](https://medium.com/codex/15-fun-and-interesting-apis-to-use-for-your-next-coding-project-in-2022-86a4ff3a2742)

