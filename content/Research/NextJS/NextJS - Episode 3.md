---
title: "NextJS - Episode 3"
---
### NextJS - Episode 3: Assets, Metadata & Scripts

#### Introduction
Hi everyone and welcome to the third episode in this series. Now that we have a basic understanding of routing in NextJS, let's explore other interesting topics. In this episode, I'm going to cover how to work with assets, how to modify the metadata of a page, and how to load external scripts.

#### Assets
Let's start off with assets. All files that are not sources of code for your application can be considered assets. A few examples are images, videos, and SVGs.

All asset files in NextJS must be put inside of the `public` directory. This folder can also contain other useful data, such as the `favicon.ico`, `robots.txt`, Google Site Verification and any other static file. For this reason, files such as images are usually stored in an `images` folder inside the `public` directory.

With regular HTML, you'd display an image in the browser in this way:

```tsx
<img src="/images/profile.jpg" alt="Your Name" />
```

However, this comes with many downsides you have to take care of, such as:
- Ensuring your image is responsive on different screen sizes
- Optimizing your images with a third-party tool or library
- Only loading images when they enter the viewport

NextJS lifts removes thirs hurdle by offering a custom React component that takes care of all of those, the `Image` component.

Let's see a practical example. I'm going to display a simple profile picture using the Image component.

First off, I'm going to create the `images` folder inside the `public` directory. I have prepared a .png file for this, but you can use any other image. 

🎬 *Drag profile.png file inside the `images` folder*

After we've done that, let's go to `movie.tsx` and import the Image component, which is exported from `next/image`.

```tsx
import Image from 'next/image'
```

Under the `Link` tag, create the `Image` component and inside of it, you must provide 4 properties:
- src: The source of the image, in our case the path in the `public` directory: `/images/profile.png`
- alt: An alternative text in case the image does not load or gets corrupted, let's put "profile picture" here.
- width: 256
- height: 256

```tsx
<Image
  src="/images/profile.png"
  alt="profile picture"
  width={256}
  height={256}
/>
```

The width and height are necessary for NextJS to let it know how much space it needs to hold for the image while it's still loading. This is also solves a problem in web development known as Cumulative Layout Shift or CLS for short. CLS is also a metric used by Google Search Ranking to rank your website higher. So, be sure to use it whenever possible.

Let's start the app and see if it works

🎬 *Start the dev server*

Before I go to the `/movie` route, I want to show you something. I'm going to open console and go in the Network tab. 

🎬 *Open the Network tab*

Let's hit refresh. As you can see, the profile picture has not loaded yet. That's because the image is not in this page. It will load when I go to the `movie` page. Let's try that.

🎬 *Click the link on the homepage that goes to `/movie`*

As you see, it's right here.

#### Recap of first 3 episodes