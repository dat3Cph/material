---
title: Routing
description: How does the React Router work
layout: default
nav_order: 10
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/router
---

# Frontend routing with React Router 6 and 7

React Router enables "client side routing". React Router is currently released as version **7.0.1** (Nov 28 2024). The documentation of **7.0.1** is not totally done yet, but it's a small release, and the previous version **6.28.0** is very similar. So look to a fuller [documentation there](https://reactrouter.com/6.28.0/home). The biggest change is that as of **7.0.1**, you need to import one library: `react-router`. Previously, you needed `react-router-dom` instead. Since **6.4.0** it's recommended to use `createBrowserRouter` and `<RouterProvider router={router} />` as shown below. They are containg all the latest updates and functions. The older `<BrowserRouter>` still works, but hasn't got the latest bling.

## So what is a router in a SPA

In traditional websites, the browser requests a document from a web server, downloads and evaluates CSS and JavaScript assets, and renders the HTML sent from the server. When the user clicks a link, it starts the process all over again for a new page.

Client side routing allows your app to update the URL from a link click without making another request for another document from the server. Instead, your app can immediately render some new UI and make data requests with fetch to update the page with new information.

This enables faster user experiences because the browser doesn't need to request an entirely new document or re-evaluate CSS and JavaScript assets for the next page. It also enables more dynamic user experiences with things like animation.

And having the URL update with each page makes it possible for users to share links to specific pages of your app, or to use the browser's back and forward buttons to navigate between pages.
[Source: Feature Overview](https://reactrouter.com/en/main/start/overview)

## Examples

You can typically place your router in either `main.jsx` or in the `App.jsx`. It's up to you. This is how you can do it in `main.jsx`.

## `main.jsx`

```jsx
import { createBrowserRouter, Route, createRoutesFromElements, RouterProvider } from 'react-router'

const router = createBrowserRouter(
  createRoutesFromElements(
    <Route path="/" element={<App />} errorElement={<ErrorPage />}>
      <Route path="photos" element={<Photos />}>
        <Route path=":id" element={<Photo />} />
      </Route>
      <Route path="articles" element={<h1>Articles</h1>} />
    </Route>
  )
);
```

In the above example,

- the `<App />` component will be rendered when the URL matches `/` or any of its children. The children will be shown in its `<Outlet/>` element.
- The `<Photos />` component will be rendered when the URL matches `/photos` or any of its children.
- The `<Photo />` component will be rendered when the URL matches `/photos/:id` in  the `<Outlet/>` element in the parent (Photos) component.
- The `<h1>Articles</h1>` element will be rendered when the URL matches `/articles`.

### Attaching the router to the DOM

Also in the `main.jsx`:

```jsx
ReactDOM.createRoot(document.getElementById("root")).render(
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
);
```

### Nested routes

In above example, the App component will be rendered when the URL matches `/` or any of its children. The Photos component will be rendered when the URL matches `/photos` or any of its children. The way to achieve this is by using the `Outlet` component.

```jsx
<>
  <div>
    <Header />
  </div>
  <h1>Router example </h1>
  <div className="card">
    <Outlet />
  </div>
</>
```

### Url parameters and navigation

Here we can see how we can use the react router hooks `useParams` and `useNavigate` to get the url parameters and navigate to a new url.

- `photos.js`:

```jsx
import { Outlet, useNavigate, useParams } from "react-router-dom";
...
    <>
      <h1>PHOTOS:</h1>
      {PhotoFacade.getAll().map((photo) => {
        return (
            <img
              key={photo.id}
              onClick={() => {
                navigate(`/photos/${photo.id}`); // Same as javascript: window.location.href = `/photos/${photo.id}`;
              }}
              src={photo.url}
              style={{ width: 300, margin: 6 }}
            />
        );
      })}
      <Outlet />
    </>
```

And the `Photo.js` component:

```jsx
import { useParams } from "react-router-dom";
...
const { id } = useParams();
const [photo, setPhoto] = useState({url:""});

useEffect(() => {
    const photo = photoFacade.getPhoto(Number.parseInt(id));
    setPhoto(photo);
});
```

### Getting the data

- `photoFacade.js`:

```jsx
const photos = [
    {
    id: 1,
    name: 'small goats',
    url: 'https://www.worldvision.org/wp-content/uploads/2020/09/D485-1090-047_Web_Optimized.jpg'
},
    {
    id: 2,
    name: 'child with goat',
    url: 'https://upload.wikimedia.org/wikipedia/commons/thumb/b/b2/Hausziege_04.jpg/1920px-Hausziege_04.jpg'
},
    {
    id: 3,
    name: 'mountain goat',
    url: 'https://upload.wikimedia.org/wikipedia/commons/3/31/Goats_butting_heads_in_Germany.jpg'
},
]
export default {
    getPhoto: (id) => photos.find(photo=>photo.id === id),
    getAll: () => photos,
};
```

### Links

The last thing we need to do is to add links to the urls we want to navigate to. We can do this by using the `Link` or `NavLink` component.

```jsx
const Header = () => {
  return (
    <header className="header">
      <div className="logo">Your Logo</div>
      <nav className="nav-menu">
        <NavLink to="/" exact="true" className={({isActive}) => (isActive ? "active" : 'none')}>
          Home
        </NavLink>
        <NavLink to="/photos" className={({isActive}) => (isActive ? "active" : 'none')}>
          Photos
        </NavLink>
        <NavLink to="/articles" className={({isActive}) => (isActive ? "active" : 'none')}>
          Articles
        </NavLink>
      </nav>
    </header>
  );
};
```

### Styling the Header Component

We can create a `Header.css` file and import it into the `Header.js` component.

```css
/* Header.css */
.header {
    background-color: black;
    color: white;
    display: flex;
    justify-content: space-between;
    align-items: center;
    /* padding: 10px 10px; */
    width: 100%;
  }
  
  .logo {
    font-size: 1.5rem; /* Adjust the font size as needed */
  padding: 1.5em;
  }
  
  .nav-menu {
    display: flex;
  }
  
  .nav-menu a {
    text-decoration: none;
    color: white;
    margin-right: 20px; /* Adjust the spacing between menu items */
  }
  
  .nav-menu a.active {
    font-weight: bold; /* Style for the active link */
    color: red
  }
  
```
