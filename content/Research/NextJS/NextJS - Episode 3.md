---
title: "NextJS - Episode 3"
---
### NextJS - Episode 3: Assets, Metadata & Scripts

#### Introduction
Hi everyone and welcome to the third episode in this series. Now that we have a basic understanding of routing in NextJS, let's explore other interesting topics. In this episode, I'm going to cover how to work with assets, how to modify the metadata of a page, and how to load external scripts.

#### Assets
Let's start off with assets. All files that are not sources of code for your application can be considered assets. A few examples are images, videos, and SVGs.

All asset files in NextJS must be put inside of the `public` directory. This folder can also contain other useful data, such as the `favicon.ico`, `robots.txt`, Google Site Verification and any other static file. For this reason, files such as images are usually stored in an `images` folder inside the `public` directory.