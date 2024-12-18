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

With **Vite**, you can achieve dynamic API base URL configuration using **environment variables**. Here's how you can set it up:

---

### 1. Define Environment Variables

In Vite, you can use `.env` files to define environment-specific variables:

#### a. Create `.env` Files

1. For **local development**:

   - Create a file named `.env` (or `.env.development`):

     ```plaintext
     VITE_API_BASE_URL=http://localhost:5000
     ```

2. For **production**:

   - Create a file named `.env.production`:

     ```plaintext
     VITE_API_BASE_URL=https://your-deployed-api.com
     ```

3. For additional environments (e.g., staging), you can create `.env.staging`:

   ```plaintext
   VITE_API_BASE_URL=https://staging-api.com
   ```

---

### 2. Access the Environment Variables in Code

In your code, use `import.meta.env` to access the environment variables. For example:

```javascript
const BASE_URL = import.meta.env.VITE_API_BASE_URL;

async function fetchData() {
  const response = await fetch(`${BASE_URL}/endpoint`);
  const data = await response.json();
  console.log(data);
}
```

⚠️ **Note:** Environment variables in Vite must start with the prefix `VITE_` for them to be accessible via `import.meta.env`.

---

### 3. Building and Running

- When you run `npm run dev` (or `yarn dev`), Vite uses `.env` or `.env.development` by default.
- When you run `npm run build` (or `yarn build`), Vite uses `.env.production`.

---

### 4. Customize for Multiple Environments

To build for other environments (e.g., staging), you can specify the environment file using the `--mode` flag:

```bash
# Use staging environment
vite build --mode staging
```

Vite will then use `.env.staging` during the build process.

---

### 5. Example Directory Structure

```
project/
├── .env
├── .env.development
├── .env.production
├── .env.staging
├── src/
│   ├── main.js
│   ├── App.jsx
```

---

### 6. Additional Notes

- **Environment Variable Precedence**: If a variable is defined in multiple `.env` files, the file matching the mode takes precedence.
- **Accessing All Variables**: You can log `import.meta.env` to inspect all available environment variables.
- **Security Warning**: Never include sensitive information in your `.env` files, as they are bundled into the final build.

With this setup, Vite dynamically uses the correct base URL for your API depending on the environment.
