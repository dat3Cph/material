---
title: Setup with Vite
description: Start new React Project
layout: default
nav_order: 2
parent: React
grand_parent: Toolbox
has_children: false
permalink: /toolbox/react/vite
---


# Starting a new React project with Vite

<img src="./images/vitelogo.png" width="200" align="right">

Vite is a build tool that significantly improves the frontend development experience. It's designed to offer faster build times and a simpler configuration compared to older bundlers like Webpack.

Here are the steps to start a React project using Vite:

1. **Install Node.js**: Ensure you have Node.js installed on your system.

2. **Create a New Vite Project**: Open your terminal and run the following command to create a new project. This command scaffolds a project with a basic Vite and React setup.

   ```bash
   npm create vite@latest my-react-app -- --template react
   ```

   Replace `my-react-app` with your desired project name.

3. **Navigate to the Project Directory**:

   ```bash
   cd my-react-app
   ```

4. **Install Dependencies**: Run the following command to install the necessary dependencies.

   ```bash
   npm install
   ```

5. **Start the Development Server**: Start your development server with:

   ```bash
   npm run dev
   ```

   This will start the Vite development server. You can view your application by opening `http://localhost:5173` in your web browser (or the port that Vite suggests).

6. **Building and Running in Production**: To build the application for production, use:

   ```bash
   npm run build
   ```

   This will create a `dist` folder which contains the production build of your app. To preview it locally, you can run:

   ```bash
   npm run preview
   ```

7. **Customizing Your Project**: You can customize your project by editing the files in the `src` folder. Vite supports hot module replacement (HMR), so your changes will be reflected in the browser almost instantly.

8. **Adding Additional Dependencies**: If you need to add more packages or libraries to your project, use npm or yarn to install them as you would in any other Node.js project.
For example React Router (newest version):

```console
npm i react-router
```

9. **Consult the Documentation**: For more advanced configurations and optimizations, refer to the [Vite documentation](https://vitejs.dev/guide/) and [React documentation](https://react.dev/learn).

Starting with Vite offers a modern, fast, and efficient way to build React applications, making it a great choice for both beginners and experienced developers.
