---
title: "NextJS - Random Notes"
---
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