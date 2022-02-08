---
title: "NextJS - Lesson 4: Pre-Rendering & Data Fetching"
---
Work in progress

#### Introduction
Hi everyone and welcome to the fourth lesson. After understanding the basics, let's explore the core concepts behind the reason why NextJS is truly a powerful framework. By the end of this lesson, you will have learned:
- Pre-rendering in NextJS
- How Static Site Generation (SSG) works behind the scenes
- How to import external data using `getStaticProps`

#### Pre-rendering
Before we talk about data fetching, let's talk about one of the most important topics in NextJS: pre-rendering.

I've covered the basics of pre-rendering in [Lesson 1](Courses/NextJS/NextJS%20-%20Lesson%201.md). In this lesson, we're going to build on that knowledge.

### Static Site Generation
🏞️ SSG with and without data

Static Site Generation, or SSG for short, can be done with or without data.

By default, all pages that do not require any form of data fetching are statically generated when the application is built for production.

But, you may run in the case that your page **does** need to fetch external data to be built properly. An example could be a blog article that needs to fetch the content inside of it. For this scenario, NextJS offers SSG wtih data.

🏞️ *SSG with data*

How this process differs from SSG without data, is that all pages that require data fetching to be built, will fetch the needed information, insert it into the HTML file and store the result. 

This process will happen only once, when the application is built for production.

