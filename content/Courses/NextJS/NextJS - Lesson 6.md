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

