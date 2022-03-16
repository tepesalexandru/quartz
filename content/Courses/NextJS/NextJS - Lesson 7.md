---
title: "NextJS - Lesson 7: Deploying to Vercel"
---
#### Introduction
Hi everyone and welcome to episode 7, the last one in the NextJS series. In this one, you'll learn how to:

🏞️ What you will learn slider

- Style the homepage
- Use `Layouts` in NextJS
- Deploy the app using Vercel

🎬 Show github repository

As always, I'm going to build upon the code from last episode, so be sure to clone the `episode-6` branch in order to follow along.

#### Homepage CSS
Let's start off with the homepage. 

🏞️ Display finished homepage look

This is desired result of how the homepage should look. We have a grid of movies, each one with thier image and a hover effect. When we click on a movie, it redirects us to a page specific to that movie.

Let's get to work.

Open up VSCode, and select the `Home.module.css` file. It should be in the `styles` folder, but if you don't see it be sure to create it.

Inside of it, I'm going to paste the following CSS code:

```css
.container {
  padding: 42px 200px;
}

.grid {
  display: grid;
  column-gap: 24px;
  grid-template-columns: repeat(1, 1fr);
  row-gap: 24px;
}

.movieCard {
  display: flex;
  flex-direction: column;
  gap: 24px;
}

.movieImage {
  position: relative;
  height: 500px;
  width: 100%;
  cursor: pointer;
  transition-duration: 300ms;
}

.movieImage:hover {
  transform: scale(1.1);
  border: 4px solid #FFC300;
}

.movieCard span {
  font-weight: bold;
  font-size: 20px;
  width: 200px;
}
```

And below it, let's add some media queries in order to make the page more responsive:

```css
@media (max-width: 700px) {
  .container {
    padding: 42px 40px;
  }
}

@media (min-width: 700px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);
  }
  .container {
    padding: 42px 100px;
  }
}

@media (min-width: 1000px) {
  .grid {
    grid-template-columns: repeat(3, 1fr);
  }
  .container {
    padding: 42px 100px;
  }
}

@media (min-width: 1280px) {
  .grid {
    grid-template-columns: repeat(4, 1fr);
  }
}

@media (min-width: 1600px) {
  .grid {
    grid-template-columns: repeat(5, 1fr);
  }
}
```

You can find all of these styles in the `github repository` of this episode. 

I'm not going to explain everything that's in here since this isn't a tutorial about CSS, but you are free to use it, modify it and study it.

Great, now that we have all of the styles for the homepage, let's open the `index.tsx` file to make the needed changes.

Let's start off with the `getServerSideProps` function. As of right now, we are only fetching the movie ids. Let's refactor this function in order to get all of the information of the popular movies.

It's quite a simple refactor, we just have to chnage the `.map()` method, and the return value:

```tsx
...
const { results: popularMovies } = await req.json();

return {
  props: {
    popularMovies,
  }
}
```

Let's also fix the compilation errors by changing the Props `type`:

```tsx
type Props = {
  popularMovies: MovieProps[];
};
```

And the name of the prop parameter:

```tsx
const Home: NextPage<Props> = ({ popularMovies })
```

Now, let's get to the component itself. The first thing we're going to do is delete everything under the `<Head>` tag since we're not going to need it.

Also, I'm going to change the page title to `TOPMovies`, since that's what I'm calling this app.

Now, we can start displaying the grid of movies. Create a new `div` with a class of `grid`:

```tsx
<div className={styles.grid}></div>
```

Inside of it, we're going to map over each popular movie and create a div for them, with a class of `movieCard`:

```tsx
{popularMovies.map((movie: MovieProps) => (
  <div className={styles.movieCard} key={`movie-${movie.id}`}>
  </div>
))}
```

Since we're in a map method, be sure to also add a unique key. In my case, I've set the key to be the movie id.

Awesome, now we have the basic grid structure, we just need to fill it with the movie images and their titles.

I'm going to start with the movie image. In order to display it, I'm going to use the same strategy as the landscape image from the movie page. Meaning that I will crete a parent div with the dimensions I want, 

```tsx
<div className={styles.movieImage}>
  
</div>
```

and then the `Image` component will fill the available space in the parent:

```tsx
<Image
  src={`https://image.tmdb.org/t/p/original${movie.poster_path}`}
  alt="Movie image"
  layout="fill"
  objectFit="cover"
/>
```

Under the `movieImage` div, I'm going to display the movie title in a simple `span` tag:

```tsx
<span>{movie.title}</span>
```

Awesome, let's run the app in development mode to view the current result:

```
npm run dev
```

Open up the browser, and here it is. The images are displayed nicely in a grid, and we have a nice hover effect on the images. The only thing missing, is the ability to click a movie to view its details.

Let's go back to VSCode and do just that. It's quite straight forward. We need to wrap the `movieImage` div with a `Link` tag, that has an href that goes to that movie, but also an extra prop named `passHref` , and we're going to set that to true.

```tsx
<Link href={`/movies/${movie.id}`} passHref={true}>
  <div className={styles.movieImage}>
  ...
  </div>
</Link>
```

The `passHref` prop allows us to pass the navigation logic to the first child of the `Link` component, even if it's not an `a` tag.

Save the file, and let's check the browser. Now, when we click an image, it redirects us to that movie page. Awesome.

#### Layouts
One more feature I want to discuss before deploying our project to Vercel is `Layouts`.

Layouts allow us to wrap every page with a component. This is perfect in case our website needs a header or a footer. In our project, I'm going to use `Layouts` in order to display a basic header on every page.

In order to create a `Layout`, we need a new folder to store it. In essence, a `Layout` is just a component with a `children` prop. 

Let's start off by a creating a new folder named `components` in the root directory, and inside of it a new file named `Navbar.tsx`. After that, insert the basic component snippet with `tsrfc`:

```tsx
import React, { ReactElement } from "react";

type Props = {

};

export default function Navbar({}: Props) {
  return (
    <div></div>
  );
}
```

The most import thing about this `Layout` component is that it will wrap around the existing app. In order to do that, it must accept a prop named `children`, so we're going to add to the `type` and deconstruct it:

```tsx
type Props = {
  children: ReactElement;
};

export default function Navbar({ children }: Props)
```

This component will contain two things, the navbar itself, as well as the rest of the app, denoted as `children`. A basic structure for the component looks like this:

```tsx
<div>
  <div>{/* Navbar */}</div>
  {children}
</div>
```

For this example, I'm going to buid a very simple header, only containing the title of the app, in this case `TOPMovies`, that when clicked it redirects the user to the homepage.

We've already learned how to do that by using a `Link`:

```tsx
<Link href="/">
  <a>TOPMovies</a>
</Link>
```

That's all we need, but I'd like to make the navbar a little better to look at, so I'm going to add some css to it.

I'm going to create a new css file just for the navbar in the `styles` folder, named `Navbar.module.css`. Inside of it, I'm going to paste the following styles:

```css
.navbar {
  padding: 14px 40px;
  background-color: #001D3D;
  font-weight: bold;
  font-size: 30px;
}
```

Great, now that we have those, let's return to the `Navbar` component and import them:

```tsx
import styles from "../styles/Navbar.module.css";
```

as well as giving the class to the parent of the `Link` component:

```tsx
<div className={styles.navbar}>
  <Link href="/">
    ...
  </Link>
</div>
```

Perfect, the `Navbar` component is now ready to use. We can wrap every page in our app with this component by going in the `_app.tsx` file, importing the `Navbar` and wrapping the `Component` tag with it.

```tsx
import Navbar from "../components/Navbar";

...
return (
  <Navbar>
    <Component {...pageProps} />
  </Navbar>
);
```

That's all there is it to. Let's save everything and check the browser again.

As you can see, now we have a simple navbar, and when we click on a movie, it stays right there. We can also click the app title in order to go back to the homepage.

Since now we have this functionality, we no longer need the `Link` to the homepage in the movie page. Let's quickly delete it from the `[id].tsx` file:

```tsx
<Link href="/">
  <a>Homepage</a>
</Link>
```

Awesome. We are done developing the app. Of course, you can keep going with it and have fun implementing new features.

The last step when building an application is actually deploying it. So let's do that next.

#### Deploying to Vercel
Vercel is the perfect platform to deploy NextJS applications. The process is very simple and fast.

To get starter, head over to [Vercel](https://vercel.com/) and login with your Github Account. After you're logged in, you'll a dashboard with all of the projects you have deployed so far. 

In order to deploy our TOPMoives project, click on the "+ New Project" button.  Here, select your github account and then click on "Import" where you see your project's name. In my case, this project is called "nextjs-movies" on Github. 

We get redirected to a new screen with more options. They look fine to me, so let's deploy the application. Now the deployment process has begun, and we just have to wait a few minutes.

Awesome, now the application has been deployed successfully, and we can check it out from the link generated by Vercel.

And there it is, everything works perfectly. You can give this link to anyone and they will be able to see your project.

#### Ending
Thank you so much everyone for sticking around and enjoying the series. This is the last episode involving NextJS, but I encourage you to check out the other videos on this channel. See you in the next one!