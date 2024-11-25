---
title: React Fetching
description: Exercises for Frontend Week I
layout: default
nav_order: 12
grand_parent: JS and React I
parent: Exercises
permalink: /frontend/javascript-react-intro/exercises/fetch/
---

# React 3: Fetching from an API

These exercises introduces two important aspects of React.

1. useState (how to store data on the client in variables)
2. useEffect (how to evoke functions on life cycle events)

And then we will work with more Javascript functionality:

1. fetch (fetching data from api's)
2. click events

## Fetch and display jokes

### 3.1.1 Click event

Create a simple React Component that can fetch and display a Chuck Norris joke fetched from this API: `https://api.chucknorris.io/jokes/random` whenever a button “Get ChuckNorris” is clicked.

Use this code to get started, and figure out how the various parts work:

- useState
- useEffect
- fetch

```react
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

Then add the button and click-event. Check here [how to add an `onClick` event](https://react.dev/learn#responding-to-events) to a button component. Refactor the fetching part in a separate function would be a good way to start ...

### 3.1.2 useEffect part 1

Add a feature, so that every 10 second (don’t decrease this number, the risk is that they will block our IP) a joke is fetched from this API: `https://icanhazdadjoke.com/`. The documentation is here:  [https://icanhazdadjoke.com/api](https://icanhazdadjoke.com/api).

Hints: you need to add an Accept key to the http header. Indicating that we will fetch a json response. For the 10 second timer, look here: [https://javascript.info/settimeout-setinterval](https://javascript.info/settimeout-setinterval)

### 3.1.3 useEffect part 2

Ensure that the required timer for the dad jokes is cancelled when the user leaves the page.

Hint: `clearInterval`is the keyword to look for. Check [this article for details](https://www.codementor.io/@damianpereira/how-to-use-clearinterval-inside-react-s-useeffect-and-why-it-is-important-1si7mztjlk). The article demonstrates why `clearInterval` is important, and how to implement it in a useEffect hook.
