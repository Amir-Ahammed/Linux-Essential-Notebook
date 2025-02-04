# NPM Notes

## What is NPM?
NPM (Node Package Manager) is the default package manager for **Node.js** and **JavaScript** projects. It helps you:
- Install and manage **dependencies** (libraries and tools).
- Run scripts for building, testing, and starting your project.
- Share and reuse code through the NPM registry.

---

## How Does NPM Work?
1. **`package.json` File**:
   - This file is the heart of your project. It contains:
     - **Dependencies**: Libraries your project needs to run.
     - **DevDependencies**: Tools needed only for development.
     - **Scripts**: Commands to build, test, or start your project.
   - Example:
     ```json
     {
       "name": "my-project",           // The name of your project.
       "version": "1.0.0",             // The current version of your project.
       "scripts": {                    // Custom commands you can run using `npm run <script-name>`.
         "start": "node app.js",
         "build": "node app.js",
         "test": "jest"
       },
       "dependencies": {               // Libraries your project needs to run in production.
         "express": "^4.17.1",
         "react": "^18.2.0",
       },
       "devDependencies": {            // Tools your project needs only during development.
         "jest": "^27.0.0"
       }
     }
     ```

2. **`node_modules` Folder**:
   - When you run `npm install`, NPM installs all the dependencies listed in `package.json` into this folder.

3. **NPM Commands**:
   - Install dependencies:
     ```bash
     npm install
     ```
   - Start the project:
     ```bash
     npm start
     ```
   - Run tests:
     ```bash
     npm test
     ```
   - Install a specific package:
     ```bash
     npm install package-name
     ```

---

## How to Determine if Your Project Needs NPM
You’ll need NPM if your project:
1. **Has a `package.json` File**:
   - This file indicates that the project uses NPM to manage dependencies and scripts.

2. **Uses JavaScript Frameworks or Libraries**:
   - If your project uses **Angular**, **React**, **Vue.js**, **Express.js**, or other JavaScript frameworks, it likely needs NPM.

3. **Requires Build Tools**:
   - If your project uses tools like **Webpack**, **Babel**, **TypeScript**, or **Jest**, NPM is required to install and manage these tools.

4. **Includes a `node_modules` Folder**:
   - If the project has a `node_modules` folder, it means NPM was used to install dependencies. However, this folder is usually excluded when sharing projects, so you’ll need to run `npm install` to recreate it.

5. **Uses NPM Scripts**:
   - If the project documentation or team members tell you to run commands like `npm install`, `npm start`, or `npm build`, you’ll need NPM.

---

## When You Don’t Need NPM
You **don’t need NPM** if:
- Your project is **plain HTML, CSS, and JavaScript** without any frameworks or build tools.
- It uses a different package manager like **Yarn** or **pnpm** (though NPM can still work in most cases).

---

## How to Install NPM
1. **Install Node.js**:
   - NPM comes bundled with Node.js. Download and install Node.js from [https://nodejs.org](https://nodejs.org).
   - Choose the **LTS (Long Term Support)** version for stability.

2. **Verify Installation**:
   - After installing Node.js, check if NPM is installed by running:
     ```bash
     npm -v
     ```

---
