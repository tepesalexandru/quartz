---
title: "NextJS - Episode 2"
---
### NextJS - Episode 2: Routing
Github Repository: 📂 https://github.com/The-Boring-Team/nextjs-movies
Slides: 🟡 In Progress

#### Introduction
Hi everyone and welcome to the second episode in this series. In this one, we're going to create a new page in the existing project and implement routing back and forth between the main page and the new page. 

As always, you can follow along coding. For everything presented in the video, there is a github repository with the full code. You can view the code for each episode by checking out that specific branch.

🎬 *Show github repository and branches*

#### Creating a new page
Before we get into how to create a page in NextJS, we must understand what's going on underneath.

🎬 *Display a slider with information about NextJS pages*

A page in NextJS is a React component exported from the `pages` directory.

Pages are associated with a route based on their file name. For example:
- `pages/car.tsx` will be at the `/car` route
- `pages/movie.tsx` will be at the `/movie` route

There is a special case, when the page name is `index`
- `pages/index.tsx` will be at the `/` route

This is because index is a special keyword in NextJS, noting that the specified page is the entrypoint of the website.

Routes can also be nested, for example
- `pages/cars/tesla.tsx` will be at the `/cars/tesla` route
- `pages/movies/iron-man.tsx` will be at the `/movies/iron-man` route

Let's create our first page. Go over to the `/pages` directory, right click and create a new file. You can name this file anything, but if you want to follow along, I will be naming it `movie.tsx`.

As I've said before, NextJS pages are just React components underneath. Here, we just need to export a component, but it's very important to export it as default, otherwise NextJS will not recognize it properly. So, let's do just that.

```movie.tsx
export default function Movie() {

}
```

and for now, let's make it return a simple message, such as "My first movie page!"

```movie.tsx
export default function Movie() {
 return <div>My first movie page!</div>;
}
```

This is all you need, but before we see if it works, we need to install the npm packages necessary to run the project with the typescript file (the one ending in .tsx). So, let's go to the command prompt, and type in the following command:

```
npm install --save-dev typescript @types/react
```

After the packages have been installed, let's run the server by typing

```
npm run dev
```

Something interesting has happened. NextJS detected that we're using typescript and automatically created extra files to integrate with it, such as the `tsconfig.json` file.

We can see the new page we've created by going to the `/movie` route in the browser, so let's type that in. And there we go, the message "My first movie page!" appears. Fast refresh also still works, and you can see that by changing the message inside vscode.

Sweet, now we know how to create pages. Let's see how to connect them and enable navigation from one to the other.

#### Navigation
Normally, when linking pages in HTML, an `<a></a>` tag is used. In NextJS it's very similar, the only difference being that the `a` tag is wrapped in a `Link` component that is exported from `next/link`. The `href` attribute is also moved from the `a` tag to the `Link` component.

In our case, let's begin by creating a Link from the `/movie` route back to the `/` route.

First off, import the `Link` component

```movie.tsx
import Link from "next/link";
```

then, down here create a Link that goes to the `/` route.

```movie.tsx
<Link href="/"></Link>
```

Inside of it, put the `a` tag and also some text, such as "Homepage".

```movie.tsx
 <Link href="/">
  <a>Homepage</a>
 </Link>
```

Let's test it by going to the `/movie` route in the browser. Click on "Homepage", and there we go, it worked! As you have seen, it also used client-side navigation, since there was no refresh when we clicked the link.

🎬 *Go on the previous page in the browser and click on homepage again and show that there is no refresh*

As you can see again.

Awesome. Now, let's do the same process by linking the Homepage to the `movie` page

Go to the `index.js` file, and since we're here let's change the extension to `.tsx` so it can use typescript.

First off, import the Link component and let's put it right after the `h1` tag.

```index.tsx
<Link href="/movie">
 <a>Movie page</a>
</Link>
```

Inside of the `a` tag, I'm going to write "Movie page". 

Save the file, and let's see if it works!

🎬 *Navigate back and forth 2-3 times between the homepage and the movie page*

As you can see, it works like a charm.

#### Ending
In the next episode we'll take a look at how to change the metadata of a page, such as the title and also how to work with assets, such as images, in an optimized way. 

🎬 *Display outro and link to next episode*