---
title: "NextJS - Lesson 5: Dynamic Routes"
---
🏞️ Episode 5 slider

#### Introduction
Hi everyone and welcome to the fifth episode. In this one, we'll explore a concept in NextJS called `Dynamic Routes`.

🏞️ What you will learn slider

By the end of this lesson, you will have learned how to:
- Statically generate pages with `dynamic routes` using `getStaticPaths`
- Implement the `getStaticProps` function to fetch the data for each page.
- Link to a page with a `dynamic route`

🎬 Show github repository

I'm going to build upon the code from last episode. If you want to follow along, be sure to clone the `episode-4` branch.

#### Dynamic Routes
🏞️ Dynamic routes slider

Static Site Generation allows you to generate a page depending on external data. `Dynamic routes` extend this concept by allowing you to generate page paths depending on external data.

The route we've generated so far looks like this:

```tsx
/movie
```

Dynamic routes allow us to put a parameter inside of the route itself, making the result look like this:

```tsx
/movie/[id]
```

The `[id]` part of the route is what's dynamic about it, since it can be anything we want. 

In our case, we'll want to statically generate a list of movies based on their `id`. 

It's important to clearly define what those `ids` are, since in order for NextJS to statically generate those pages, it will need to fetch the data for each one of them.

### getStaticPaths
🏞️ getStaticPaths slider

NextJS provides the `getStaticPaths` function to allow us to define the list of `ids` of the pages we want to fetch data for at build time.  The function definition looks like this:

```tsx
export const getStaticPaths: GetStaticPaths = async () => {

}
```

In our case, we'll define the `ids` of the `movies` we want to show. But first, let's look at a more generic example.

Here we can build the list of ids of the pages we want to generate, and then return them in an object with the `paths` property containing them. The `paths` property is required by the `GetStaticPaths` interface.

```tsx
export const getStaticPaths: GetStaticPaths = async () => {
  const ids = ['1', '2', '3', '4'];

  return {
    paths: ids
  }
}
```

As of right now, the function is not complete. Although we need to return a list of ids, the `paths` property  must contain an array of objects that have the following structure:

```tsx
{
  params: {
    id: "<page-id>"
  }
}
```

They have a `params` property, and inside of it, the property of `id`. The `params` property on the object actually refers to what parameters we want to insert into each statically generated page. In our case, the `id` property refers to the movie id.

Let's create a new variable holding this information. We're going to map each id to a new object with the `params` property.

```tsx
const paths = ids.map((id: string) => ({
  params: {
    id
  }
}))
```

With a small refactor, the full code looks like this

```tsx
export const getStaticPaths: GetStaticPaths = async () => {
  const ids = ['1', '2', '3', '4'];
  const paths = ids.map((id: string) => ({
    params: {
      id
    }
  }))
  
  return {
    paths
  }
}
```

Great, so far we've told NextJS which pages we want to statically generate. Now, we have to refactor the `getStaticProps` function in order to make it more dynamic. The way we do so, is by receiving the `params` object from the `getStaticPaths` function. In order to do that, insert the parameter `context` into the function definition and then extract the `id` from the `params`.

```tsx
export const getStaticProps: GetStaticProps = async (context) => {
  const { id } = context.params!;
}
```

And that's it, now we have access to the `id` property of the page we want to statically generate. This means that if the `getStaticPaths` function returns the ids `['1', '2', '3', '4']`, we'll have 4 different `getStaticProps` functions, each one of them with their own `id` property.

### Back to the project
Let's apply what we've just learned to our project. Let's start by creating a new `dynamic route`. In order to do so, create a new folder named `movies` and inside of it create a file named `[id].tsx`. As we've just learned, this route is `dynamic`, since the `id` can be anything.

Inside of this file, copy everything that's currently in the `movie.tsx` file, as we won't need it anymore.

Now we have a new `dynamic route` in our project at `/movies/id`.

Next, let's implement the `getStaticPaths` function. First off, import the `GetStaticPaths` interface.

```tsx
import { GetStaticProps, GetStaticPaths } from "next";
```

Then, under the component, create the function definition.

```tsx
export const getStaticPaths: GetStaticPaths = async () => {

}
```

Instead of manually typing the movie ids we want to statically generate, let's fetch the most popular movies and extract their ids.

We can do so by calling the `/movie/popular` endpoint in `themoviedb` API.

```tsx
const req = await fetch(
  "https://api.themoviedb.org/3/movie/popular?api_key=<your-api-key>"
);

const popularMovies = await req.json();
```

There is a lot of information that comes with this request, but all we want from it are the movie ids. We can extract them using a simple map function. Here I've put them directly in the `params` property.

```tsx
const movieIds = popularMovies.results.map((movie: MovieProps) => ({
  params: {
    id: movie.id.toString(),
  },
}));
```

Lastly, return the `movieIds` as `paths`.

```tsx
return {
  paths: movieIds,
  fallback: false
};
```

We also need to add a `fallback` property, telling NextJS to return a `404 Page` to any routes that don't match the provided movie ids.

Great, now let's refactor the `getStaticProps` function in order to use the movie id. 

Insert a new parameter named `context`, and extract the `id` from the `params`.

```tsx
export const getStaticProps: GetStaticProps = async (context) => {
  const { id } = context.params!;
  ...
}
```

Now we can use this `id` in order to fetch that particular movie. Refactor the fetch function in order to get the movie with this `id`.

```tsx
const req = await fetch(
  `https://api.themoviedb.org/3/movie/${id}?api_key=<your-api-key>`
);
```

Awesome, now the flow is complete. 

# Links to Dynamic Routes

We could build the app right now and run it, but we'd have to guess what those movie ids are. Instead of that, let's do one more thing. Generate the list of popular movies on the homepage and create a `Link` between each movie and its `dynamic route`.  

First off, go to the `index.tsx` file and write a new `getStaticProps` function in order to fetch the list of popular movies. The API endpoint for that is `/movie/popular`.

```tsx
export const getStaticProps: GetStaticProps = async () => {
  const req = await fetch(
    "https://api.themoviedb.org/3/movie/popular?api_key=<your-api-key>"
  );
  const popularMovies = await req.json();
}
```

Of course, we'll convert the response to JSON format.

Lastly, let's extract the `id` of each popular movie and pass it in the component `props`:

```tsx
  ...
  const popularMovies = await req.json();
  const movieIds = popularMovies.results.map((movie: MovieProps) =>
    movie.id.toString()
  );

  return {
    props: {
      movieIds,
    },
  };
```

As we've done before, let's define the `type` of the Props and deconstruct them.

```tsx
type Props = {
  movieIds: string[];
};

const Home: NextPage<Props> = ({ movieIds })
```

Using `NextPage<Props>` is the alternative way of applying the props type if the component is defined as an arrow function.

Now that we have the popoular movie ids, let's create a `Link` to each one of them. Inside of the `Home` component, use the `.map()` function to create a new `Link` for every `movie id` in the props. Also, since we're using the `.map()` method, be sure to give each element a unique key, in our case we'll use the movieId.

```tsx
{movieIds.map((movieId: string) => (
  <Link key={`movie-${movieId}`} href={`/movies/${movieId}`}>
    <a>{movieId}</a>
  </Link>
))}
```

The `Link` component has an `href` pointing to `/movies/${movieId}`, which is exactly what we needed.

Let's create a production build and run it.

```
npm run build
npm run start
```

Great, everything works perfectly.

### Next up
In the next episode, we'll dive into `Server Side Rendering`, we'll add external `Images` to our project as well as making everything look better with `CSS`.