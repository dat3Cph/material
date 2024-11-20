---
title: Json Mock Server
description: How to create a JSON mock server with JSON Server
layout: default
nav_order: 13
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/json-server
---

# JSON Mock Server

[npm json server](https://www.npmjs.com/package/json-server) and [json-server](github.com/typicode/json-server) is a great tool for creating a mock server for your frontend projects. It is easy to use and can be set up in minutes.

1. **Prerequisites** Make sure you have the following installed:

- node and npm

2. install json-server in the project

   ```
   npm install --save json-server
   ```

3. Ad a script to package.json (like line 5 below:) (todos.json is the file created in step 1 above)

   ```json
    "scripts": {
       "start": "node scripts/start.js",
       "build": "node scripts/build.js",
       "test": "node scripts/test.js --env=jsdom",
       "backend": "json-server -p 4000 --watch booksdb.json"
     },
   ```

4. create dummy data by making a javascript program and run it with node.   

5. Create a file in the working folder: mockdata.js:

```javascript
import casual from 'casual';

// Create an object for config file
var db = {books:[]};

for(var i=101; i<=115; i++){
    var book = {};
  book.id = i;

  // Create a random 1-6 word title
  book.title = casual.words(casual.integer(1,6));
  book.author = casual.first_name + ' ' + casual.last_name;
  
  // Randomly rate the book between 0 and 5
  book.rating = Math.floor(Math.random()*100+1)/20;

  // Assign a publishing year between 1700 and 2016
    book.year_published = casual.integer(1700,2016)
    db.books.push(book);
}
console.log(JSON.stringify(db));
```

6. This script is using `casual` to generate random data. Install it into the same folder.

```
npm install casual --save-dev
```

**Windows users:** In git bash run the js script like this:
```assembly
bash -c "node mockdata.js > booksdb.json"
```
**Mac and Linux users:** In git bash run the js script like this:
```assembly
node mockdata.js > booksdb.json
```

It will write an array of 15 book objects into a file: booksjb.json

Open the file to see the data format (or in the bash just `node mockdata.js` without the pipe `>` character)


7. Now the json-server can be started with: 

   ```
   npm run backend
   ```

8. In a browser open url: `http://localhost:4000/books` to see the server running.
