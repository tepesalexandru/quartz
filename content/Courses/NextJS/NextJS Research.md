---
title: "NextJS Research"
---
### Episode 5: Dynamic Routes
What you will learn in this episode:
- How to statically generate pages with `dynamic routes` using `getStaticPaths`
- How to write `getStaticProps` to fetch the data for each movie.
- How to link to a page with a `dynamic route`

### Dynamic Routes
SSG allows you to generate a page depending on external data. `Dynamic routes` extend this concept by allowing you to generate page paths depending on external data.

### How to generate dynamic routes
First off, go to the `pages/movies` folder and create a file named `[id].tsx`. Pages that begin with `[` and end with `]` are dynamic routes in NextJS.

Inside of the file, return a component and under it, place the `getStaticPaths` function. The function must return all possible values for the `id` of the movie.

```tsx
export default function Movie() {
  return <div>Hello</div>
}

export async function getStaticPaths() {
  // return possible IDs for the movie
}
```

After that, we must implement the `getStaticProps` function, to fetch the data for the movie with a given id. The function is also given the `params` parameter, which contains the `id` of the movie (because the filename is `[id].tsx`).

```tsx
export async function getStaticProps({ params }) {

}
```

Configure `next.config.json` to allow `theimagedb` images to be fetched

Add a `title` tag to each movie page.