---
title: "NextJS - Lesson 6: Server Side Rendering"
---
#### Introduction
Hi everyone and welcome to episode 6 in the NextJS series. In this one, we're going to tackle some very interesting topics. By the end of this episode, you will have learned how to:

🏞️ What you will learn slider

- Always fetch the most recent data using `Server Side Rendering`
- Implement the `getServerSideProps` function
- Optimize loading time of `external images`
- Improve the website's appearence using `CSS`  

🎬 Show github repository

I'm going to build upon the code from last episode. If you want to follow along, be sure to clone the `episode-5` branch.

#### Server Side Rendering
Server Side Rendering, or SSR for short, is a form of pre-rendering. It's very similar to Static Site Generation, the only difference being that instead of fetching the data only once at build time, the data is fetched on every refresh of the page.

This is useful when you need the most recent data to be shown on the page. The downside of using SSR compared to SSG is that page load time increases and is no longer instant.

To fetch data using Server Side Rendering, the `getServerSideProps` function is used.

#### The getServerSideProps function
🏞️ getServerSideProps function

To fetch data for a page while its loading, the `getServerSideProps` function is used. The skeleton of the function looks like this:

```tsx
export default function Home(props: Props) { ... }

export const getServerSideProps: GetServerSideProps = async (context) => {
  
}
```

Since this function is executed when someone requests a page, we can access extra information about the request parameters. That information is contained in the `context` parameter.

Similar to `getStaticProps`, the `getServerSideProps` also returns an object with the `props` property:

```tsx
export const getServerSideProps: GetServerSideProps = async (context) => {
  return {
    props: {
      // component props
	}
  }
}
```

Let's go back to our project and implement Server Side Rendering on the Home component.

#### Implementing SSR
As always, let's open up VS Code. I'm going to use the `getServerSideProps` function in order to fetch the most popular movies and display them on the homepage.

Open the `index.tsx` file, and scroll down to the `getStaticProps` function. If you remember from last episode, we've already implemented the functionality of fetching the most popular movies, the only problem being that they are fetched only at build time.

As we all know, the list of popular movies changes frequently in real life. Therefore, it would be nice to always display the most recent information when we load the homepage. SSR allows us to do exactly that.

Let's refactor the pre-rendering method to be Server Side Rendering instead of Static Site Generation for this component.

It's quite simple, the only thing we have to change is the name of the function and its interface.

```tsx
export const getServerSideProps: GetServerSideProps = async () => {
  ...
};
```

Now, when we build the application for production the most recent information will be fetched on the home component.

🏞️ "The new problem" slide

But by doing this, a new problem arises. What if the list of popular movies updates, but we haven't statically generated the page for that movie? In a previous episode, we've seen that if the movie id wasn't present in the `getStaticPaths` function, then a `404 Page` would be displayed.

We don't want to show a `404 Page` for the new popular movies that appear. NextJS comes with a very handy solution for this exact problem. The `fallback` property inside of the `getStaticPaths` function.

🏞️ Fallback property slide

If `fallback` is set to `false`, then any page with an id that isn't present in the `paths` property, will return a `404 Page`.

If `fallback` is set to `"blocking"`, then any page with an id that isn't present in the `paths` property, will statically generate that page when it is requested for the first time, cache it for future requests and add its `id` to the `paths`.

This is exactly what we need. Let's go back to the project and open the `[id].tsx` file, where we have the `getStaticPaths` function. Here, lets set the `fallback` property to `"blocking"`.

Awesome, now the website is a lot more dynamic. From now on, we'll only improve the website appearence.

Let's begin by displaying the image of the movie after we click on it.

#### External Images
The `moviedb` API allows us to fetch the image of a particular movie. By reading [the docs](https://developers.themoviedb.org/3/getting-started/images) we see that the movie images are stored at this URL:

```
https://image.tmdb.org/t/p/original<movie-poster-path>
```

The poster path is a property that is present on each movie when we fetch them. Let's begin by adding this property to the `MovieProps` interface. Go to `types.ts` and add it there.

```tsx
export type MovieProps = {
  ...
  poster_path: string;
};
```

Back in the `[id].tsx` file, let's import the `Image` component:

```tsx
import Image from "next/image";
```

And above the movie title, display the movie image:

```tsx
<Image
  src={`https://image.tmdb.org/t/p/original${movieData.poster_path}`}
  alt="Movie image"
  height={400}
  width={300}
 />
```

Let's run the app in development mode to see what happens.

```
npm run dev
```

Open the browser, and click on any movie id. An error appears, saying that the hostname "image.tmdb.org" is not configured under images in your `next.config.js`. This is because by default, NextJS doesn't know how to optimize images coming from external sources. 

We can fix this error by going into the `next.config.js` file, and adding a new property named `images`, that contains the `domains` of possible sources for the external images. In our case, that would be "image.tmdb.org":

```tsx
const nextConfig = {
  reactStrictMode: true,
  images: {
    domains: ["image.tmdb.org"],
  },
};
```

Let's run the app again. Now, when we click on a movie, everything works correctly and the image is displayed.

Let's add some CSS to improve the page appearence

#### CSS
