---
title: "NextJS - Lesson 5: Dynamic Routes"
---
🏞️ Episode 5 slider

#### Introduction
Hi everyone and welcome to the fifth episode. In this one, we'll explore a concept in NextJS called `Dynamic Routes`.

🏞️ What you will learn slider

By the end of this lesson, you will have learned:
- How to statically generate pages with `dynamic routes` using `getStaticPaths`
- How to write `getStaticProps` to fetch the data for each page.
- How to link to a page with a `dynamic route`

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

NextJS provides the `getStaticPaths` function to allow us to define the list of `ids` of the pages we want to fetch data for at build time. In our case, we'll define the `ids` of the `movies` we want to show.

### getStaticPaths
🏞️ getStaticPaths slider

The function definition looks like this:

```tsx
export const getStaticPaths: GetStaticPaths = async () => {

}
```

Here we can build the list of ids, and then return them.

```tsx
export const getStaticPaths: GetStaticPaths = async () => {
  const ids = ['1', '2', '3', '4'];

  return {
    paths: ids
  }
}
```
