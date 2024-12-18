---
title: Changing base URL
description: How to change baseurl between localhost and production
layout: default
nav_order: 13
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/baseurl
---

![Codelab](./images/reactlogo.png){: style="display: block; margin: 0 auto; width:50%" }

# How change the base url between localhost and production

This is a common practice in React applications. You can achieve base-url switching by using **environment variables** that differentiate the API base URL based on the environment (development vs. production). Here's how you can set it up:

### 1. Use Environment Variables

React apps (created using `create-react-app` or similar setups) support environment variables. You can define different variables for different environments.

#### a. Create `.env` files

1. For local development:
   - Create a file named `.env.development`:

     ```plaintext
     REACT_APP_API_BASE_URL=http://localhost:5000
     ```

2. For production:
   - Create a file named `.env.production`:

     ```plaintext
     REACT_APP_API_BASE_URL=https://your-deployed-api.com
     ```

React will automatically use the appropriate file when you build or run the app (`.env.development` for `npm start` or `yarn start` and `.env.production` for `npm run build` or `yarn build`).

---

### 2. Access the Environment Variables in Code

In your code, you can use the environment variable like this:

```javascript
const BASE_URL = process.env.REACT_APP_API_BASE_URL;

async function fetchData() {
  const response = await fetch(`${BASE_URL}/endpoint`);
  const data = await response.json();
  console.log(data);
}
```

---

### 3. Building and Deployment

- During **development**, when you run the development server (`npm start`), the app will use `http://localhost:5000` as the base URL.
- When you **build the app for production** (`npm run build`), React will embed the production API base URL (`https://your-deployed-api.com`) into the build files.

---

### 4. Additional Notes

- **Security**: Be careful not to expose sensitive credentials in environment variables, as they are bundled into the final build.
- **Debugging**: If something doesn’t work as expected, log `process.env` to ensure your environment variables are loaded correctly.
- **Custom Builds**: If you need more flexibility (e.g., different staging or testing environments), you can create additional `.env` files like `.env.staging` and load them using `npm run env-cmd`.

This setup ensures your app fetches data from the correct API base URL depending on the environment.
