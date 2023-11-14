# React 2: Fetching from an API

## Fetch and display jokes

### 1.1 Click event

Create a simple React Component that can fetch and display a Chuck Norris joke fetched from this API: `https://api.chucknorris.io/jokes/random` whenever a button “Get ChuckNorris” is clicked.

Use this code, and figure out how the various parts work:

- useState
- useEffect
- fetch

```javascript
import React, { useState, useEffect } from 'react';

function JokeComponent() {
    // State to store the joke
    const [joke, setJoke] = useState('');

    // useEffect to fetch the joke
    useEffect(() => {
        fetch('https://api.chucknorris.io/jokes/random')
            .then(response => response.json())
            .then(data => setJoke(data.value))
            .catch(error => console.error('Error fetching joke:', error));
    }, []); // Empty dependency array means this runs once on mount

    // Render the joke
    return (
        <div>
            <p>{joke}</p>
        </div>
    );
}

export default JokeComponent;

```

### 1.2 useEffect part 1

Add a feature, so that every 10 second (don’t decrease this number, the risk is that they will block our IP) a joke is fetched from this API: `https://icanhazdadjoke.com/`. The documentation is here:  [https://icanhazdadjoke.com/api](https://icanhazdadjoke.com/api).

Hints: you need to add an Accept key to the http header. Indicating that we will fetch a json response. For the 10 second timer, look here: [https://javascript.info/settimeout-setinterval](https://javascript.info/settimeout-setinterval)

### useEffect part 2

Ensure that the required timer for the dad jokes is cancelled when the user leaves the page.

Hint: `clearInterval`is the keyword here