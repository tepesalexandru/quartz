---
title: "NextJS Research"
---
### Features
NextJS is a **React Framework**. NextJS aims to have the best developer experience and comes with many built in features such as:
- Page-based **routing system** (also supports dynamic routes)
- Pre-rendering, including both SSG (**static generation**) and SSR (**server side rendering**) per page basis.
- Automatic **code splitting** ⇒ faster load times
- **Client-side routing** with optimized prefetching.
- **Fast Refresh** (instant feedback when making edits to react components)
- API Routes to build API endpoints with **Serverless Functions**
- **CSS and SASS** support, or any CSS-in-JS library
- **Typescript** support.

### Setup
- Install NodeJS.
- Have VS Code installed (or any other IDE).

**Create new NextJS project**
```
npx create-next-app nextjs-notes --use-npm
```
Where `nextjs-notes` is the name of the folder where our app will be created.

**App idea: note taking app.**

**Run NextJS Project**
```
cd nextjs-notes
npm run dev
```

Go to localhost:3000 or control click the link from the command prompt. The NextJS server is running. When opening the server, we'll see the starter page of NextJS. Let's make a quick change to see if it works.

To find the starter page, go in the `pages/index.js` file. Here you can edit anything, and it will be update instantly on the browser without the need to refresh. Be sure to have the development server running while saving the file to view the changes in the browser.

