---
title: "NextJS Research"
---

Idea:  The best 3 NextJS projects will be features in a blog article on the Boring Team publication. To enter, submit your github link in the google forms down in the video description.

#### Assets
NextJS can serve static assets, such as images, under the top-level `public` directory. They can be referenced by your code from the base URL: `/`.

For example, the image at `public/car.png` can be referenced in your code in this way:

```tsx
import Image from 'next/image'

function Car() {
  return <Image src="/car.png" alt="me" width="64" height="64" />
}

export default Car
```

The `public` folder also contains other useful data, such as the `favicon.ico`, `robots.txt` , Google Site Verification and any other static files.

Usually, images are stored in a `images` folder inside the `public` directory.

With regular HTML, you'd display the image in the browser in this way:

```tsx
<img src="/images/profile.jpg" alt="Your Name" />
```

However, this means you have to manually handle:
-   Ensuring your image is responsive on different screen sizes
-   Optimizing your images with a third-party tool or library
-   Only loading images when they enter the viewport

This is the unoptimized way. Let's do better.

NextJS provides the `Image` component out of the box to handle this for you.

[`next/image`](https://nextjs.org/docs/api-reference/next/image) is an extension of the HTML `<img>` element, evolved for the modern web.

Automatic Image Optimization works with any image source. Even if the image is hosted by an external data source, like a CMS, it can still be optimized.

### Metadata
NextJS offers the `Head` component out of the box, which is used to modify the `head` part of the page, such as the page title. You can view an example in `index.tsx`.

To change the title of another page, simply add the `Head` tag in it. To do that, follow these steps:

```tsx
import Head from 'next/head'
```

and then in your component add the following:

```tsx
 <Head>
    <title>Iron Man</title>
 </Head>
```

And now the title of that page will be "Iron Man".

#### Third-Party JS
In addition to metadata, scripts that need to load and execute as soon as possible are usually added within the `head` of page. 

Using regular HTML, an external script would be added like this:

```tsx
<Head>
  <title>Iron Man</title>
  <script src="https://connect.facebook.net/en_US/sdk.js" />
</Head>
```

Although this approach works, including scripts in this manner does not give a clear idea of when it would load with respect to the other JavaScript code fetched on the same page. If a particular script is render-blocking and can delay page content from loading, this can signficiantly impact performance.

NextJS provides the `Script` component to better handle external scripts, exported from `next/script`.

```tsx
import Script from 'next/script'
```

```tsx
<Script
  src="https://connect.facebook.net/en_US/sdk.js"
  strategy="lazyOnload"
  onLoad={() =>
    console.log(`script loaded correctly, window.FB has been populated`)
  }
/>
```

-   `strategy` controls when the third-party script should load. A value of `lazyOnload` tells Next.js to load this particular script lazily during browser idle time
-   `onLoad` is used to run any JavaScript code immediately after the script has finished loading. In this example, we log a message to the console that mentions that the script has loaded correctly

The Facebook SDK script was used just as an example to see how to load scripts in an efficient way. We'll remove it now.