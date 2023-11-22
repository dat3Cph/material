# React  CRUD & Form

This is a guided tutorial in which we will:

1. Fetch person data from an api ([JSON Server](https://www.npmjs.com/package/json-server))

2. Show a list of persons

3. Implement simple `CRUD` operations on the persons. This includes `GET`, `POST`, `PUT`, and `DELETE` http requests by using Javascripts' `fetch` method.

4. Do a little styling with css and Bootstrap.

## The video series

Code happily along with the video tutorials - and use the snippets from this file when needed. In this way we can speed up the work a bit.

### 1. Getting the project configured

- Create a React project with [Vite](../../setup/vite.md)
- Cleaning up stuff

### 2. Using JSON server

- Configuring the JSON server. Copy this json snippet and insert into a `db.json` file.

```json
{
    "api":
    [
      {
        "id": 1,
        "age": "22",
        "name": "Steve",
        "email": "steve@test.com",
        "gender": "male"
      },
      {
        "id": 2,
        "age": "19",
        "name": "Michelle",
        "email": "michelle@test.com",
        "gender": "female"
      },
      {
        "id": 3,
        "age": "30",
        "name": "Anna",
        "email": "anna@test.com",
        "gender": "female"
      },
      {
        "id": 4,
        "age": "45",
        "name": "Karl",
        "email": "karl@test.com",
        "gender": "male"
      },
      {
        "id": 5,
        "age": "15",
        "name": "Michael",
        "email": "michael@test.com",
        "gender": "male"
      }
    ]
  }
```

A snippet for the `package.json`:

```json
    "jsonserver": "json-server --watch data/db.json --port 3000"
```

And one for the `vite.config.js`:

```json
server: {
    proxy: {
      '/api': 'http://localhost:3000'
    }
  }
```

### 3. Creating components

- PersonForm.jsx

```html
<form>
    <label htmlFor="id">Id</label>
    <input id="1" type="number" readOnly placeholder="id" />
    <label htmlFor="name">Name</label>
    <input id="name" type="text" placeholder="name" />
    <label htmlFor="age">Age</label>
    <input id="age" type="number" min="1" max="120" placeholder="age" />
    <label htmlFor="email">Email</label>
    <input id="email" type="email" placeholder="email" />
    <label htmlFor="gender">Gender</label>
    <select id="gender">
        <option defaultChecked>Select Gender</option>
        <option value="male">Male</option>
        <option value="female">Female</option>
        <option value="other">Other</option>
    </select>
</form>
```

- PersonList.jsx

```html
<table className="table table-striped">
    <thead>
        <tr>
        <th>Id</th>
        <th>Name</th>
        <th>Age</th>
        <th>Email</th>
        <th>Gender</th>
        <th>Action</th>
        </tr>
    </thead>
    <tbody>
        <tr>
        <td>1</td>
        <td>Bingo</td>
        <td>34</td>
        <td>bingo@gmail.com</td>
        <td>Malicious</td>
        <td>
            <button>Edit</button>
            <button>Delete</button>
        </td>
        </tr>
    </tbody>
    </table>
```

### 4. Activating Bootstrap css styles

Insert into `index.html` in the `head` section:

```html
 <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-Zenh87qX5JnK2Jl0vWa8Ck2rdkQ2Bzep5IDxbcnCeuOxjzrPF/et3URy9Bv1WTRi" crossorigin="anonymous">
```

### 5. Setting up states

### 6. Fetching persons from the JSON-server

Create a new folder `util` and a file `persistence.js`:

```javascript
export function fetchData(url, callback, method, body) {

    const headers =
        {
            'Accept': 'application/json'
        }

    if (method === 'POST' || method === 'PUT') {
        headers['Content-Type'] = 'application/json'
    }

    const options = {
        method,
        headers
    }

    if (body) {
        options.body = JSON.stringify(body);
    }

    fetch(url, options)
        .then(res => res.json())
        .then(data => callback(data))
        .catch(err => {
            if (err.status) {
                err.fullError.then(e => console.log(e.detail))
            } else {
                console.log("Network error");
            }
        })
}
```

### 7. Showing the persons

### 8. Inserting new persons

### 9. Editing persons

### 10. Deleting persons

### 11. Styling
