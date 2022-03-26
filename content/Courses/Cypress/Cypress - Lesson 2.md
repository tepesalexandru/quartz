---
title: "Cypress - Lesson 2: Your first test"
---
Now that everything is set up, we can write the first test for our application.

In essence, an automated test is a set of instructions that lives inside a javascript file. In the previous lesson, we've learned that test files are contaiend in the `integration` folder of our directory, and usually end with the extension `.spec.js`.

Let's create our very first Cypress test by creating a new file in the `integration` folder, named `first.spec.js`, indicating that this is our first test.

#### describe()
There are a few things we need to insert here, the first of which will be the `describe` function. This function will be present in each one of your tests and is used to describe what your test is about, in order to make your test results more human readable.

The `describe()` function takes in two arguments, the first one being a string describing your test file, and the second a callback function. In my case, I'll describe this test as "My first test":

```js
describe("My first test", () => {

})
```

The callback function will contain all the logic needed for our test file.

#### it()
You can think of a test file as a collection of smaller tests. The `describe()` function contains the logic for all the tests, and an `it()` function contains the logic for just one small test.

Let's create our first small test inside of the callback function using the `it()` function. This function is similar in structure as the `describe()` function, since it takes the same parameters: a string describing the test and a callback function.

In my case, I want this first test to be called "Should say hello to me":

```js
describe("My first test", () => {
  it("Should say hello to me", () => {
    console.log("hello!")
  })
})
```

Awesome, thats all we need to get started. We can check that everything works using

```bash
npx cypress open
```

and clicking on `first.spec.js`.

As of right now, our test does absolutely nothing, but by looking at the left side of the screen, you can better visualize what the `describe` and `it` functions did. The `describe` function works like a wrapper to all the smaller tests, while it `it` function contains one small test.

Of coure, the current test is not very useful, so let's make it do something more interesting, such as visiting a web page.

We can do that using the `cy.visit()` function.

#### cy.visit()
Let's keep the first test, and under it write another one. As an example, let's make it visit the google homepage. So, an easy to read test would look like this:

```js
it("Should navigate to the google homepage", () => {
  cy.visit("www.google.com")
})
```

Save the file and go back to the automated browser. As you can see, the tests ran automatically upon saving the file, and you can see the google homepage on the right side. Awesome!

This is getting really cool, but we can do even better. Cypress allows you to check the value of certain things in your automated tests. We can check for things such as does a button appears on the page, or if a certain input is disabled, or even count how many divs are on a page. These are very basic examples, but Cypress is even more powerful than that. 

The action of checking things in our tests are called `assertions`. In the next lesson, we're going to explore how to write your first assertion in Cypress.

#### [Lesson 3: Assertions](Courses/Cypress/Cypress%20-%20Lesson%203.md)
