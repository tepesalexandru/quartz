---
title: "NextJS - Lesson 3: Assets, Metadata & Scripts"
---
Lesson 3 complete code: [Github Repo](https://github.com/The-Boring-Team/nextjs-movies/tree/episode-3)

#### Introduction

Hi everyone and welcome to the third episode in this series. Now that we have a basic understanding of routing in NextJS, let's explore other interesting topics. In this episode, I'm going to cover how to work with assets, how to modify the metadata of a page, and how to load external scripts.

#### Assets
![Assets](https://pomodoroapi44ff78.blob.core.windows.net/obsidian-courses/Courses/NextJS/Episode3/2.png)

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

NextJS removes this hurdle by offering a custom React component that takes care of all of those, the `Image` component.

Let's see a practical example. I'm going to display a simple profile picture using the Image component.

First off, I'm going to create the `images` folder inside the `public` directory. I have prepared a .png file for this, but you can use any other image. 

🎬 *Drag your .png file inside the `images` folder*

After we've done that, let's go to `movie.tsx` and import the Image component, which is exported from `next/image`.

```tsx
import Image from 'next/image'
```

Under the `Link` tag, create the `Image` component and inside of it, you must provide 4 properties:
- src: The source of the image, in our case the path in the `public` directory: `/images/profile.png`
- alt: An alternative text in case the image does not load or gets corrupted
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

The width and height are necessary for NextJS to let it know how much space it needs to hold for the image while it's still loading. This also solves a problem in web development known as Cumulative Layout Shift or CLS for short. CLS is also a metric used by Google Search Ranking to rank your website higher. So, be sure to use it whenever possible.

Let's start the app and see if it works

🎬 *Start the dev server*

Before I go to the `/movie` route, I want to show you something. I'm going to open console and go in the Network tab. 

🎬 *Open the Network tab*

Let's hit refresh. As you can see, the profile picture has not loaded yet. That's because the image is not in this page. It will load when I go to the `movie` page. Let's try that.

🎬 *Click the link on the homepage that goes to `/movie`*

As you see, it's right here.

Let's see how to work with Metadata.

#### Metadata
![Metadata](https://pomodoroapi44ff78.blob.core.windows.net/obsidian-courses/Courses/NextJS/Episode3/4.png)

Metadata refers to the information related to a page. This includes things such as the title of the page, the favicon and many more. In regular HTML, the `head` tag would be used for these things.

NextJS offers a special component for this, which can be imported from `next/head`, and is used to modify anything normally present in the head tag.

For example, let's change the title of the page `movie`.

Go inside the `movie.tsx` file and import the `Head` component.

```tsx
import Head from "next/head";
```

Then, in the return statement, place it somewhere at the top.

Inside of it, let's open the `title` tag and change the page title to "Iron Man". 

```tsx
<Head>
  <title>Iron Man</title>
</Head>
```

Save your changes and go back to the browser. 

🎬 *Open browser in the /movie route*

As you can see, the page title is now Iron Man. 

You can also change the favicon on this page by using the `link` tag, and giving it an image. Let's do that with the existing profile image.

```tsx
<Head>
  <title>Iron Man</title>
  <link rel="icon" href="/images/profile.png" />
</Head>
```

🎬 *Open browser*

And now the favicon has also changed. But, if you navigate back to the homepage, you'll also see that both the title and the favicon have changed. 

🎬 *Click the link to the homepage*

This is because in the `index.tsx` file, another `Head` tag is defined with other information.

Lastly, let's take a look at Third-Party Scripts.

#### Third-Party JS
![Scripts](https://pomodoroapi44ff78.blob.core.windows.net/obsidian-courses/Courses/NextJS/Episode3/5.png)

What I actually mean by third-party is a script that was not written by us, but we need it in our application. An example would be us having to use the Facebook SDK. This will be just an example, and I will delete it later since we don't actually need it. 

So, to use the SDK, we'd need to import an external javascript file in our app. NextJS enables us to do that using the `Script` component, exported from `next/script`.

Let's import it in the `movie` page.

First off, go to `movie.tsx` and import the `Script` component.

```tsx
import Script from 'next/script'
```

Then, right after the `Head` tag, open the `Script` tag with the source of the Facebook SKD, in this case, it's this link right here..

```tsx
<Script
  src="https://connect.facebook.net/en_US/sdk.js"
/>
```

Other attributes can be assigned to the `Script` tag that are not present in regular HTML, such as a loading strategy and a onLoad function.

For example, I'll be putting a strategy of `lazyOnLoad`, which tells NextJS to only load the script when the browser is not fetching any other data. As for the onLoad function, let's put the message `script loaded successfully.`

```tsx
<Script
  src="https://connect.facebook.net/en_US/sdk.js"
  strategy="lazyOnload"
  onLoad={() =>
    console.log(`script loaded successfully.`)
  }
/>
```

Let's go to the browser, open up the Network tab and hit refresh. 

We can see that the sdk.js has loaded, and that in the console tab the message appears. 

The Facebook SDK populates the `window.FB` object, and you can see that by typing in `window.FB` in the console and hitting enter. 

As you can see, there is a lot of stuff here provided by the SDK.

#### Recap
Awesome. Before we go any further let's quickly recap what you've learned so far.

You've learned how to setup a new NextJS project, how to create create new pages and how to navigate between them, and also how to work with images, metadata and third-party scripts.

#### Ending
In the next episode, we'll take a deeper look at pre-rendering and data fetching in NextJS. See you soon!

#### [NextJS - Lesson 4](Courses/NextJS/NextJS%20-%20Lesson%204.md)