---
title: "NextJS - Lesson 4: Pre-Rendering & Data Fetching"
---
Lesson 4 complete code: [Github Repo](https://github.com/The-Boring-Team/nextjs-movies/tree/episode-4)

🏞️ Episode 4 slider

#### Introduction
Hi everyone and welcome to the fourth lesson. After understanding the basics, let's explore the core concepts behind the reason why NextJS is truly a powerful framework. 

🏞️ Introduction slider

By the end of this lesson, you will have learned:
- How Static Site Generation (SSG) works behind the scenes
	- SSG with data
	- SSG without data
- How to import external data using `getStaticProps`

#### Pre-rendering
I've covered the basics of pre-rendering in [Lesson 1](Courses/NextJS/NextJS%20-%20Lesson%201.md). In this lesson, we're going to build on that knowledge.

### Static Site Generation
🏞️ SSG with and without data

Static Site Generation, or SSG for short, is a form of pre-rendering and it can be done with or without data.

By default, all pages that do not require any form of data fetching are statically generated when the application is built for production.

But, you may run in the case that your page **does** need to fetch external data to be built properly. An example could be a blog article that needs to fetch the content inside of it. For this scenario, NextJS offers SSG wtih data.

🏞️ *SSG with data*

How this process differs from SSG without data, is that all pages that require data fetching to be built, will first fetch the needed information, then insert it into the HTML file and store the result. 

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

It's usually placed in the same file as the component we want to fetch data for. In this example, it's for a component named Home. 

I've also added the `GetStaticProps` return type in order to make it type-safe.

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

🏞️ Static generation benefits slide

Again, the benefit of fetching data using `getStaticProps` is that the data is fetched at build time, not when the user requests the page. Therefore, the user can see the page instantly, without waiting for any data to load. On the other hand, if you're using a `create-react-app`, you'd be using Client-Side Rendering (CSR), and have to wait for the data each time.

Let's see how to statically generate a page in our existing project. 

🎬 *Show github episode 3 branch*

If you do not have the code you can clone it from the github repository by selecting the `episode 3` branch. 

### Implementing SSG
First off, open up VS Code. I'm going to use the `getStaticProps` function to fetch data for the movie page.

Let's go to `movie.tsx`, and under the component, write the empty function.

```tsx
export default function Movie() { ... }

export async function getStaticProps(): GetStaticProps {

}
```

For this example, I'm going to use the `moviedb` API to fetch a movie with all of its data. In order to do so, we have to generate an API key from their website by creating an account. This process takes less than a minute.

### Getting the API Key
First off, go to [themoviedb.org](https://www.themoviedb.org/), create a new account, and verify your email.

Then, login with your credentials, click on your profile icon in the upper right corner and select "Settings".

From the left menu, click on "API", and then generate a new API key. 

Lastly, select "Developer" and fill out the form that appears.

After you've completed the process, you should see somewhere on your screen an API key that looks like this:

```
4311457e3cc8a7c606a63fb963646ad1
```

Awesome, now we can continue with the project.

### Fetching Data
Let's fetch a movie from the API and pass the result to the `Movie` component. 

To do so, I'm going to use the native `fetch` function to fetch the movie with an id of `550` from the `moviedb` API and transform the response to JSON format:

```tsx
export async function getStaticProps(): GetStaticProps {
  const req = await fetch(
    "https://api.themoviedb.org/3/movie/550?api_key=<your-api-key>"
  );
  const movieData = await req.json();
}
```

> For security reasons, you don't want other people to see your API Key, but for simplicity, we're going to keep it here.

Lastly, we have to pass the fetched movie as props to the component.

```tsx
export async function getStaticProps(): GetStaticProps {
  const req = await fetch(
    "https://api.themoviedb.org/3/movie/550?api_key=<your-api-key>"
  );
  const movieData = await req.json();

  return {
    props: {
      movieData,
    },
  };
}
```

Awesome, now the component needs to be able to accept the incoming data.

For that, above the `Movie` component, declare a new type for the props and another for the movie properties:

```tsx
type MovieProps = {
  title: string;
  release_date: number;
}

type Props = {
  movieData: MovieProps;
}
```

> In this case, we're looking at only 2 properties of the movie, its `title` and `release_date`. In the future, we'll add more properties.

Then deconstruct the props in the parameter of the function. In this case, we're expecting to receive a prop named `movieData`:

```tsx
export default function Movie({ movieData }: Props)
```

And that's it! Now we have access to the `movieData` prop inside of the component. Let's display the movie title and its release year.

```tsx
export default function Movie({ movieData }: Props) {
  return (
    <div>
    ...
      <div>{movieData.title}</div>
      <div>{movieData.release_date}</div>
    </div>
  );
}
```

Save the file, and start the dev server if it's stopped. Open the browser, and go to the movie page.

Awesome! Everything is displayed correctly.

But, you may have noticed that the `Movie` page did not load instantly. This is because in `development` mode, every page uses Server Side Rendering instead of Static Generation. So, the data is filled in when the user requests the page.

As you've seen previously, static generation happens when we build the application for production. So, let's do that and see if there's a difference.

Run this command to build the app for production:

```cmd
npm run build
```

After the command has finished running, the production build will be in the `.next` folder. To run it, use the command:

```
npm run start
```

Now the local server will simulate a production environment. If we open the browser and go again to the movie page, you'll see that the page loads instantly on click.

### Next up
In the next episode, we'll explore how to create a page for each movie in our app using `dynamic routes`. See you there!
