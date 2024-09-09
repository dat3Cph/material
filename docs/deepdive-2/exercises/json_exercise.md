---
title: JSON DTO Exercise
description: Java Deep Dive II Exercise DTO and JSON
layout: default
nav_order: 2
has_children: false
grand_parent: Java Deep Dive II
parent: Exercises
permalink: /deepdive-2/exercises/json-dto
---

# JSON DTO Exercise

## Part 1

Answer the following questions: [link for help](https://www.w3schools.com/js/js_json_intro.asp)

* What does JSON stand for?
* What is the difference between JSON and XML?
* For what is JSON generally used for?
* Write down the 6 data types in JSON.
* Write down the 4 JSON syntax rules.

## Part 2

1. Create a new file called `account.json`
2. Create a JSON object with the following properties in account.json (the notation is pseudo code):

```plaintext
 `firstName` (string)
 `lastName` (string)
 `birthDate` (string)
 `address` (object)
        - `street` (string)
        - `city` (string)
        - `zipCode` (integer)
 `account` (object)
        - `id` (string)
        - `balance` (string)
        - `isActive` (boolean)
```

3. Wrap the JSON object in an array
4. Add 5 more accounts to the array
5. Save the file
6. Open the file in a browser and verify that it is valid JSON. You do this by paste the absolute path to the file in the browser address bar. For example: `file:///Users/username/Desktop/account.json

## Part 3

1. Open a Java project in your IDE and create classes for the JSON object you created in part 2.
2. Create a method that can read the JSON object from the file and return an array of Account objects.
3. You can use a JAVA library to convert the JSON object to a JAVA object or vice versa. For example [Jackson](../../toolbox/dataintegration/jackson.md).
4. Create a DTO class that has the following properties:

```plaintext
 `fullName` (string)
 `city` (string)
 `zipCode` (string)
 `isActive` (string)
```

5. Create a method that can print out the DTO objects in the array in a nice format.

## Hint! - if you need help reading the JSON file in Java

<details markdown="block">
<summary>
Here’s a Java method called `readJsonFromFile` that reads a JSON file from the resources folder into a `String`:
</summary>

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.nio.charset.StandardCharsets;
import java.util.stream.Collectors;

public class JsonFileReader {

    public static String readJsonFromFile(String filename) {
        // Get the resource file from the classpath
        InputStream inputStream = JsonFileReader.class.getClassLoader().getResourceAsStream(filename);

        if (inputStream == null) {
            throw new IllegalArgumentException("File not found: " + filename);
        }

        // Read the file content into a string
        try (BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream, StandardCharsets.UTF_8))) {
            return reader.lines().collect(Collectors.joining("\n"));
        } catch (IOException e) {
            throw new RuntimeException("Failed to read the file: " + filename, e);
        }
    }
}
```

### Explanation

1. **`InputStream`**: This reads the file as a stream from the resources folder using `getResourceAsStream()`.
2. **`BufferedReader`**: Wraps the input stream for efficient reading.
3. **`Collectors.joining("\n")`**: Collects the lines of the file into a single string, separated by newlines.
4. **Exception Handling**: If the file is not found, an `IllegalArgumentException` is thrown. If an I/O error occurs, a `RuntimeException` is thrown.

### How to use

Place your JSON file in the `resources` folder, and call the method like this:

```java
String jsonString = JsonFileReader.readJsonFromFile("data.json");
System.out.println(jsonString);
```

This will read the contents of the `data.json` file into a `String`. Make sure the JSON file is in the `resources` folder within the project structure.

</details>
