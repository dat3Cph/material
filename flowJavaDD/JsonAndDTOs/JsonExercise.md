# JSON DTO Exercise

## Part 1

Answer the following questions: [link](https://www.w3schools.com/js/js_json_intro.asp)

* What does JSON stand for?
* What is the difference between JSON and XML?
* For what is JSON generally used for?
* Write down the 6 data types in JSON.
* Write down the 4 JSON syntax rules.

## Part 2

1. Create a new file called `account.json`
2. Create a JSON object with the following properties in account.json:

```
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
3. You can use a JAVA library to convert the JSON object to a JAVA object or vice versa. For example [GSON](https://github.com/google/gson) or [Jackson](https://www.baeldung.com/jackson-object-mapper-tutorial).
4. Create a DTO class that has the following properties:

```
 `fullName` (string)
 `city` (string)
 `zipCode` (string)
 `isActive` (string)
```

5. Create a method that can convert an Account object to a DTO object.
6. Create a method that can convert an array of Account objects to an array of DTO objects.
7. Create a method that can print out the DTO objects in the array in a nice format.


