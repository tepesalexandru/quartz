---
title: "NextJS - Lesson 1: Introduction"
---
If you prefer the video version of this lesson, click here: [Youtube Video](https://www.youtube.com/watch?v=uAXPlgB0YgM).

Hi everyone and welcome to the first lesson. I'll be covering everything you need to know to get started with NextJS and create your own projects. This is a hands-on course, where you can follow along coding. We'll be building a simple Movie app while covering the core concepts of NextJS, and you will be able to publish it at the end of the course.

#### What is NextJS?
Before I dive any deeper, let's take some time to look at what NextJS is and what it can offer.

NextJS is a **React Framework** that aims to have the best developer experience, and also comes with many built in features, such as:
- Page based routing
- Pre-rendering, including both Static Generation and Server Side Rendering (more on that later)
- Image optimization.
- Fast Refresh.
- Typescript support.
- And many more.

![Image2](https://pomodoroapi44ff78.blob.core.windows.net/obsidian-courses/Courses/NextJS/Episode1/2.png)

Pre-rendering is one of the key features that make NextJS truly a powerful framework, let's see what pre-rendering is and what it does under the hood.

#### Pre-rendering
By default, NextJS pre-renders every page. This means that NextJS generates the HTML needed for each page in advance, instead of having it all done by client-side javascript. This results in better performance and SEO.

There are two forms of pre-rendering Static Generation (SSG) and Server Side Rendering (SSR). The difference between them is in **when** NextJS generated the HTML for a page.

For Static Generation, which is always recommended when possible, HTML is generated at **build time**, and will be reused on each request.

For Server Side Rendering, the HTML will be generated on **each request**.

![Image3](https://pomodoroapi44ff78.blob.core.windows.net/obsidian-courses/Courses/NextJS/Episode1/3.png)

Each HTML file from the pre-rendered pages comes with minimal javascript neccessary for that page. When the page is loaded, the js code gets executed and makes the page fully interactive. This process is called hydration.

![Image4](https://pomodoroapi44ff78.blob.core.windows.net/obsidian-courses/Courses/NextJS/Episode1/4.png)

For now, this is everything you need to know to get started with NextJS. I'll dive deeper into the other concepts whenever I will be making use of them. Now, let's setup everything we need to get started.

#### Setup 
First off, be sure to install the latest stable version of [NodeJS](https://nodejs.org/en/)  (Version MUST be >= 12.22.0). You can check if you have node installed by opening up the command prompt and typing in `node -v`. If it's installed, the node version on your computer will appear on the screen. The links to everything you need to download will be in the video description down below.

Secondly, you will need an IDE. My personal preference is VS Code, which you can download from [here](https://code.visualstudio.com/).

That's all you need to get started. Let's create the base NextJS project.

#### Creating the base project
Open up VS Code and select the folder in which you'd like to create the project.
After that, go to the command prompt in VS Code and open up the terminal using **CTRL + ~**. 

To create a new NextJS project, run the following command:

```bash
npx create-next-app@latest nextjs-movies --typescript
```

Here, `nextjs-movies` is the name of the folder where the NextJS app will be created. The flag `--typescript` indicates that we're going to be using Typescript in this project.

Now that the files have been created, type in the following commands to run the project locally

```
cd nextjs-movies
npm run dev
```

To view your project, go to localhost:3000 or press **CTRL + Click** on the URL that appears in the command prompt. If everything went as expected, you should see the base NextJS project running. 

All of the content on the page was automatically created when we ran the scripts, and it can be edited. Let's make a change to see Fast Refresh in action.

The content of the main page is situated in the `pages/index.tsx` file. Here you can edit anything, and it will be updated instantly on the browser without the need to refresh. 

Try editing something, and be sure to save the file and have the development server running. 

As you can see, the browser updated instantly. That's Fast Refresh in action. We have instant feedback on any changes we make in our files.

#### Ending
In the next lesson, we'll take a look at navigation in NextJS and how to have multiple pages in our app, since currently theres only this one. Tune in for the next episode to learn more. See you there!

#### [NextJS - Lesson 2: Routing](Courses/NextJS/NextJS%20-%20Lesson%202.md)
