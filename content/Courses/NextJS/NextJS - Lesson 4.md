---
title: "NextJS - Lesson 4: Pre-Rendering & Data Fetching"
---
Lesson 4 complete code: [Github Repo](https://github.com/The-Boring-Team/nextjs-movies/tree/episode-4)
Slides: [Canva](https://www.canva.com/design/DAE4Pq3KOps/IIvVMNXin15a7KZ-Enk3dg/view?utm_content=DAE4Pq3KOps&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink) (In progress)

🏞️ Episode 4 slider

#### Introduction
Hi everyone and welcome to the fourth lesson. After understanding the basics, let's explore the core concepts behind the reason why NextJS is truly a powerful framework. 

🏞️ Introduction slider

By the end of this lesson, you will have learned:
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

Let's see how this would look in practice.

### The getStaticProps function
🏞️ getStaticProps function

To fetch data for a static page when it is built, the `getStaticProps` function is used. The skeleton of the function looks like this.

```tsx
export default function Home(props: Props) { ... }

export async function getStaticProps(): GetStaticProps {
  
}
```

It's usually placed in the same file as the component we want to fetch data for. In this example, it's for a component named Home. I've also added the `GetStaticProps` return type in order to make it type-safe.

So far, the function is empty. But, inside of it, we can fetch data coming from many sources, such as the file system, an API, a database, and so on. An example would look like this

```tsx
export async function getStaticProps(): GetStaticProps {
  const data = await fetchData();
}
```

We can use the `await` keyword to wait for the result since the function is asyncronous. The `fetchData()` function is a just a generic example of a function that you would build to fetch external data. We'll see a concrete example in our code in just a bit.

Lastly, the `getStaticProps` function, returns an object containing the props passed to the component.

```tsx
export async function getStaticProps(): GetStaticProps {
  const data = await fetchData();

  return {
    props: {
      data
    }
  }
}
```

Now, inside of the Home component, we have access to `props.data` and can work with it.

Essentially, this whole process allows you to tell NextJS: "This page has data dependencies, so when you pre-render this page at build time, make sure to resolve them first!"

Again, the benefit of fetching data using `getStaticProps` is that the data is fetched at build time, not when the user requests the page. Therefore, the user can see the page instantly, without waiting for any data to load. 

Let's see how this process would look in our existing project. If you do not have the code you can clone it from the github repository by selecting the `episode 3` branch. 

### Implementing SSG
First off, open up VS Code. I'm going to use the `getStaticProps` function to fetch data for the movie page.

Let's go to `movie.tsx`, and under the component, write the empty function.

```tsx
export default function Movie() { ... }

export async function getStaticProps(): GetStaticProps {

}
```

For this example, I'm going to fetch data from a `.json` file. The file does not exist yet, so let's create it.

In the base directory, create a new folder named `data` and inside of it, create a new file named `movie.json`. Inside of the file, insert the the following content.

```JSON
{
  "Title": "Iron Man",
  "ReleaseYear": 2008
}
```

This will be the data we want to fetch and pass to the `Movie` component. To access this data, I'm going to use the native `fetch` function and transform the response to JSON format:

```tsx
export async function getStaticProps(): GetStaticProps {
  const req = await fetch("http://localhost:3000/movie.json");
  const movieData = await req.json();
}
```

And lastly, we have to pass it as props to the component.

```tsx
export async function getStaticProps(): GetStaticProps {
  const req = await fetch("http://localhost:3000/movie.json");
  const movieData = await req.json();

  return {
    props: {
      movieData,
    },
  };
}
```

Awesome, now the data is going towards the `Movie` component. What we have to do now is accept the incoming data.

For that, above the `Movie` component, declare a new type for the props:

```tsx
type Props = {
  movieData: MovieProps;
}
```

And then deconstruct the prop in the parameter of the function:

```tsx
export default function Movie({ movieData }: Props)
```

And that's it! Now we have access to the movie prop inside of the component. Let's display the movie title and its release year.

```tsx
export default function Movie({ movieData }: Props) {
  return (
    <div>
    ...
      <div>{movieData.title}</div>
      <div>{movieData.releaseYear}</div>
    </div>
  );
}
```

Save the file and let's check the browser. 

Awesome! Everything is displayed correctly.

### Next up
In the next episode, we'll explore how to create a page for each movie in our app using `dynamic routes`. See you there!
