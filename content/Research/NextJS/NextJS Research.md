---
title: "NextJS Research"
---
### Multiple pages
- create a new page using the integrated file system routing
- use the Link component to enable client side navigation between pages
- learn about built-in support for code splitting and prefetching

A page in NextJS is a react component exported from the `pages` directory.

Pages are associated with a route based on their file name. For example:
- `pages/index.tsx` will be at the `/` route
- `pages/posts/first-post.tsx` will be at the `/posts/first-post` route

// to do: tsconfig.json

#### Create a page
Create any file inside the `pages` directory. The component can have any name, but it must be exported as default.

#### Linking pages
Normally, in HTML you link pages with an `<a>` tag, but in NextJS you use the `<Link>` component that comes from `next/link`.

It looks like this:
```Link
<Link href="/post">
	Click me!
</Link>
```

#### Client-side navigation
The `Link` component enables client-side navigation between two pages in the same NextJS app.

Client side navigation means that the page transition is done via javascript instead of the browser, which leads to faster navigation.