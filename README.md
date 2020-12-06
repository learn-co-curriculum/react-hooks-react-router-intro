# Introduction to React Router

## Objectives

1. How client-side routing works
2. What the trade-offs are for client-side routing
3. What `pushState` is

### Client-Side Routing

So, we have learned about building components, changing state, passing props,
etc... You may be wondering how you can make an app with multiple URLs that
contain different components. Not every app is a todo list, tic-tac-toe or a
spreadsheet. So how do we build an app that allows us to have unique pages for
the user to interact with? This is where `Client-Side` routing comes in.  

**Client-side** routing is a different beast than what we are used to with
traditional server side routing that comes with **Rails**, **Sinatra**, or
**Node/Express**, because we aren't making constant **HTTP GET** requests.

Lets say that our **client side** app is going to have these routes:

- `/movies/new`
- `/movies`
- `/about`
- `/login`

Our servers's only job is to render the HTML, which will look similar to this:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Movie Maker 2020</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
  </head>
  <body>
    <div id="root"></div>
    <script src="./bundle.js" charset="utf-8"></script>
  </body>
</html>
```

With **client-side** routing, it is now the responsibility of the
**client side code**, rather than the server, to handle the routing, fetching 
and displaying of the data in the browser.

Imagine you've built a personal blog with a navigation that links your home
page, about page and contact page. With client side routing, you might get all
the needed data to render all three pages on the first page load. Then, when a
user clicks around your site, the client side router swaps the 'home page'
component with the 'about page' component and renders faster than it would if
you were requesting a separate page from a server.

Client side routing brings with it some great benefits. The major one is
_speed_. Since we are only making one request to the server, we don't have to
wait for a round trip server call for each page change. We have everything
stored on the client side already, so we just notify our client side code to
display the info as we need it.

### Single Page App (SPA)

In **React** we will likely be building an **SPA**, or Single Page Application.
This means we won't require multiple pages to be loaded from the server, just 
the original **GET** request with our initial HTML, CSS and JS files. This
requires us to figure out how to make the experience of Client-Side routing work
to our advantage.

There are a couple of things that we need to take into consideration:

- We want to make sure that we have a URL that displays what the user is doing
  at that moment. So if they are viewing a bio page it might look like this
  `https://worlds-best-app/bio` instead of this `https://worlds-best-app`.

- We want a user to be able to use the browser's back and forward buttons, as
  well as the browser history, with ease.

- We want a user to be able to input a URL into the address bar and navigate to
  the view they need to see.

This was easy with server side rendering: most MVC frameworks come with this for
free, because we just defined the routes, added the actions needed to the
controller and then made a call to the model to get the info we desired.

### Limits of Client-Side routing

So this all sounds great, but what are the limitations?

- **Loading of CSS & Javascript**: Since we are now loading all of our CSS and
  Javascript on the initial **GET** request it can take a while to load our
  first page. This can be important as the first page load can take a long time
  if you have a huge application.

- **Analytics**: Analytic tools normally track page views, but an SPA doesn't
  have pages in the traditional sense, so this makes it harder for Analytical
  tools to track page views. We will need to add extra scripts to handle this
  limitation.

- They are much harder to design.

We have to plan out all the possibilities that might happen on the
**client side**; this might feel like we are repeating designs that we have
already completed with our server routes and models.

#### Push it, Push it

When we make server calls we are making a **GET** request to a URL and that new
URL is in our address bar. If we have visited a few different URL's that
information is saved in browser history.

Go to the JavaScript console in Chrome and type:

```js
window.history
```

This should return the following code.

```js
History { length: 32, state: null, scrollRestoration: "auto" };
```

The length is how many locations you have visited in this window session.

Now if you type the following code it will take you to the last location in your
browser history.

```JavaScript
window.history.back();
```

Go ahead and try it out.

.............
............
..........

Oh good, you're back!! :)

![no you didn't!](http://i.giphy.com/10VbdHyZElXqso.gif)

So that is the JavaScript to emulate the experience of using the back button in
the browser toolbar. You can also move forward using
**window.history.forward()**.

With the JavaScript's History API we also have the ability to **pushState()** to
the history entries. This method takes in three parameters: **pushState(state,
title, url)**

- `state`: This is a plain JavaScript object that is associated with the new
  history entry we are going to create with the **pushState()** function.

- `title`: This is currently ignored by most browsers and it is safe to just
  pass an empty string or a title here.

- `url`: This is the URL for the new history entry. The browser will not attempt
  to load this URL after it calls pushState().

Why don't we go ahead and create a new url in our browser

```js
const newState = {
  goal: "Learn about pushState()"
};

window.history.pushState(newState, "new state", "new-state");
```

You should notice that your browser has now changed to show `new-state` at the
end of your URL address.

Go ahead and type

```js
window.history.state
```

It should return

```js
Object { goal: "Learn about pushState()" }
```

If you now use the `window.history.back()` function you will not go back to
the previous page, but your URL address will return to the original URL address.
If you use `window.history.forward()` you will move back to our new URL that
ends in **new-state**.

We have now successfully implemented a basic version of **client side** routing.

## Manipulating History with React Router

**React Router** is a library that gives us an easy way to interact with the
History API, much like we have been doing above, from within our React
applications. It will give us several ways to perform **programmatic
navigation** and **client side** routing from React without worrying about
working directly with the History API. 

The examples above give a good idea of what's happening under the hood, but from
here on, we'll be using React Router for all of our client side routing needs!

## A Word About Accessibility

The web was designed, from its inception, to be a platform for _everyone_,
including those who need help interacting with it through assistive devices.
Those requiring captions, inverted contrast, etc. have all been able to
participate in _our_ web because it was designed with the differently-abled
in mind _from the beginning_.

Creating accessible sites using SPA-style applications represents an
additional challenge. Many tutorials breeze past this consideration.

Designing SPA's that work with accessibility in mind proves you that you're not
only a superior developer, but a great person. Here's a [blog post][bp] on
accessibility in React.

## Resources

* [Manipulating Browser History](https://developer.mozilla.org/en-US/docs/Web/API/History_API)
* [React Router Tutorial](https://reacttraining.com/react-router/web/guides/quick-start)

[bp]: https://blog.usejournal.com/getting-started-with-web-accessibility-in-react-9e591fdb0d52

<p class='util--hide'>View <a href='https://learn.co/lessons/react-introduction-to-react-router'>React Introduction To React Router</a> on Learn.co and start learning to code for free.</p>
