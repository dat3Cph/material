# JSON

## Part 1

1. Go to https://www.w3schools.com/js/js_json_intro.asp
2. Read the following 5 sections. Ignore the parts about JavaScript.
    - JSON INTRO
    - JSON SYNTAX
    - JSON VS XML
    - JSON DATA TYPES
    - JSON ARRAY

## Part 2

Answer the following questions: (use the link above to help you)

* What does JSON stand for?
* What is the difference between JSON and XML?
* For what is JSON generally used for?
* Write down the 6 data types in JSON.
* Write down the 4 JSON syntax rules.

## Part 3

1. Create a new file called `account.json`
2. Create a JSON object with the following properties in account.json:

```
 `firstName` (string)
 `lastName` (string)
 `birthDate` (string)
 `address` (object)
        - `street` (string)
        - `city` (string)
        - `zipCode` (string)
 `account` (object)
        - `id` (string)
        - `balance` (string)
        - `isActive` (boolean)
```

3. Wrap the JSON object in an array 
4. Add 5 more accounts to the array 
5. Save the file
6. Open the file in a browser and verify that it is valid JSON. You do this by paste the absolute path to the file in the browser address bar. For example: `file:///Users/username/Desktop/account.json

## Optional

- Install a JSON viewer plugin in your browser. This will make it easier to read JSON files in the browser. One possible plugin is [JSONView](https://chrome.google.com/webstore/detail/jsonview/gmegofmjomhknnokphhckolhcffdaihd) for Chrome and Firefox.
