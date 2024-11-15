---
title: Lists and keys
description: Exercises for Frontend Week II
layout: default
nav_order: 3
grand_parent: React II
parent: Exercises
permalink: /frontend/react-2/exercises/lists
---

# React: Lists and keys

Source: [react.dev](https://react.dev/learn/rendering-lists)

This exercise will teach you how to generate lists and tables in React.

## 1. Setting up the exercise

1.1 Add a new file (component) `ListDemo.jsx` to the project you started in the previous exercise, and paste in the unfinished code below:

```react
import {useState} from "react";

function MemberTable({ members }) {
  return (
    <table>
      <thead></thead>
      <tbody></tbody>
    </table>
  );
}

function MemberDemo(props) {
  return (
    <div>
      <h4>All Members</h4>
    </div>
  );
}

export default function ListDemo() {

  const initialMembers = [{name : "Peter", age: 18},
                          {name : "Hanne", age: 35},
                          {name : "Janne", age: 25},
                          {name : "Holger", age: 22}];

  const [members,setMembers] = useState(initialMembers)
  
  return (<MemberDemo members={members} />);
}
```

1.2 Import the component into `App.jsx` and insert the component to show it's content.

1.3 Change `MemberTable` to render a table of members passed in via props.

1.4 Add the missing part in `MemberDemo` to use `MemberTable` and pass down members to it

1.5 Fix the code to avoid the error: “Warning: Each child in a list should have a unique "key" prop". Hint: You might use `crypto.randomUUID()` as key.

## 2. Please reflect on the following questions

2.1 What is the purpose of the key value, which must be given to individual rows in a react-list

2.2 It's recommended to use a unique value from your data if available (like an ID). How do you get a unique value in a map callback, for data without a unique id?

2.3 What is the difference(s) between state and props?

2.4 For which scenarios would you use props, and for which would you use state?
