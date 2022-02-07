---
title: "NextJS Research"
---
### Pre-rendering and Data Fetching

What you'll learn in this lesson:
- Pre-rendering in NextJS
- The two forms of pre-rendering: SSG and SSR
- SSG with data, and without data.
- `getStaticProps` to import data
- useful information about `getStaticProps`

In development mode (when you run `npm run dev`), every page is pre-rendered on each request, even for pages that use SSG.

NextJS let's you choose which form of pre-rendering each one of your pages uses. This allows to build an SSR/SSG hybrid app.

### When to use SSG vs SSR
SSG is recommended whenever possible, since your page only needs to be built once and served by a CDN, which makes it much faster than having a server render the page on every request.

Popular types of pages that use SSG:
- Marketing pages
- Blog posts
- E-commerce product listings
- Help and documentation

You should ask yourself the following question: "Can I pre-render this page `ahead`  of a user's request?". If the answer is `yes`, then you should choose SSG.

On ther other hand, SSG is not a good idea if you can't pre-render the page ahead of the user's request. In some cases, you need to update the date on each request, an example being a dashboard.

For these cases, you can use SSR. It will be slower, but you can be assured that your data will always be up to date.

Otherwise, you can skip pre-rendering and use client-side javascript to populate frequently updated data.

For now, we'll focus on SSG.

### SSG with and without data
SSG can be done with and without data.

All pages that do not require fetching data are automatically statically generated when the app is built for production.

You may run in the case that the HTML for some pages cannot be built before making a request to an API for example. For this case, NextJS provides support for SSG with data. When the app is built, all the necessary fetches are done and the HTML is built.

### The getStaticProps function
`getStaticProps` runs at build time in production. Inside of the function, you can fetch external data and send it as props to the page.

```tsx
export default function Home(props) { ... }

export async function getStaticProps() {
  // Get external data from the file system, API, DB, etc.
  const data = ...

  // The value of the `props` key will be
  //  passed to the `Home` component
  return {
    props: ...
  }
}
```

Essentially, getStaticProps allows you to tell NextJS: "This page has data dependencies, so when you pre-render this page at build time, make sure to resolve them first!"

### Tips
Since getStaticProps only runs at build time, you cannot access data that's available only at request time, such as the HTTP headers.

In the getStaticProps function you can also fetch external APIs and directely query a database, since this code will never run on the client-side in the browser.

If you need to fetch data at request time, then SSG is not a good idea. Using SSR would be a better strategy here.

You should use client-side rendering for private, user-specific pages where SEO is not relevant.

### SSR
For when you need to fetch data at request time, use the following function instead:

```tsx
export async function getServerSideProps(context) {
  return {
    props: {
      // props for your component
    }
  }
}
```

### SWR
React Hooks for Data Fetching (could make a video about this)

### Next up
Next up, we'll take a deeper look at `dynamic routes`.