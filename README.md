# Introduction to React Router

## Objectives

1. How client-side routing works
2. What the trade-offs are for client-side routing
3. What `pushState` is


#### Client-Side Routing

So, we have learned about building components, changing state, passing props,
etc... You may be wondering how you can make an app with multiple URLs that
contain different components. Not every app is a todo list, tic-tac-toe or a
spreadsheet. So how do we build an app that allows us to have unique pages for
the user to interact with? This is where `Client-Side` routing comes in.  

__Client-Side__ routing is a different beast than what we are used to with
traditional server side routing that comes with __Rails__, __Sinatra__, or
__Node/Express__, because we aren't making constant __HTTP GET__ requests.

Lets say that our __Client-Side__ app is going to have these routes

https://www.movie-maker-2016/movies/new

https://www.movie-maker-2016/movies

https://www.movie-maker-2016/about

https://www.movie-maker-2016/login

Our `servers` only job is to render the `HTML`. Which will look similar to this.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Movie Maker 2016</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
  </head>
  <body>
    <div id="container"></div>
    <script src="./bundle.js" charset="utf-8"></script>
  </body>
</html>
```

With __Client-Side__ routing, it is now the responsibility of the
__Client-Side-Code__ to handle the routing, fetching and displaying of the data
in the browser instead of the server.

Imagine you've built a personal blog with a navigation that links your home
page, about page and contact page. With Client-Side routing, you might get all
the needed data to render all three pages on the first page load. Then, when a
user clicks around your site, the Client-Side router swaps the 'home page'
component with the 'about page' component and renders faster than it would if
you were requesting a separate page from a server.

Client-Side routing brings with it some great benefits. The major one is
*Speed*. Since we are only making one request to the server we don't have to
wait for a round trip server call for each page change. We have everything
stored on the Client-Side already, so we just notify our Client-Side code to
display the info as we need it.

#### Single Page App (SPA)

In __React__ we will likely be building a __SPA__, or Single Page Application.
This means we wont require multiple pages being loaded, just the original
__GET__ request with our initial HTML, CSS and JS files from the Server. This
requires us to figure out how to make the experience of Client-Side routing work
to our advantage.

There are a couple of things that we need to take into consideration:

* We want to make sure that we have a URL that displays what the user is doing at
that moment. So if they are viewing a bio page it might look like this
https://worlds-best-app/bio instead of this https://worlds-best-app.

* We want a user to be able to use the browser's back and forward buttons with ease.

* We want a user to be able to input a URL into the address bar and navigate to
the view they need to see.

This was easy with server side rendering: most MVC frameworks come with this for
free, because we just defined the routes, added the actions needed to the
controller and then made a call to the model to get the info we desired.


#### Limits of Client-Side routing

So this all sounds great, but what are the limitations?

* Loading of CSS & Javascript

  Since we are now loading all of our CSS and Javascript on the initial __GET__
  request it can take a while to load our first page. This can be important as
  the first page load can take a long time if you have a huge application.

 * Analytics

  Analytic tools normally track page views, but a SPA doesn't have pages in the
  traditional sense, so this makes it harder for Analytical tools to track page
  views. We will need add extra scripts to handle this limitation. It is good to
  know though, that modern search engine spiders _are_ able to read

  * They are much harder to design.

  We have to plan out all the possibilities that might happen on the
  __Client-Side__, this might feel like we are repeating designs that we have
  already completed with our server routes and models.

#### Push it, Push it

When we make server calls we are making a __GET__ request to a URL and that new
URL is in our address bar. If we have visited a few different URL's though that
information is saved in browser history.

Go to the JavaScript console in Chrome and type

```JavaScript
window.history
```

This should return the following code.

```JavaScript
History { length: 32, state: null, scrollRestoration: "auto" };
```

The length is how many locations you have visited in this window session.

Now if you type the following code it will take you to the last location in your browser history.

```JavaScript
window.history.back();
```

Go ahead and try it out.

.............
............
..........

Oh good, you're back!! :)

![](http://i.giphy.com/10VbdHyZElXqso.gif)

So that is the JavaScript to emulate the experience of using the back button in
the browser toolbar. You can also move forward using
__window.history.forward()__.

With the JavaScript's History API we also have the ability to __pushState()__ to
the history entries. This method takes in three parameters: __pushState(state,
title, url)__

* state object:

  This is a plain JavaScript object that is associated with the new history
  entry we are going to create with the __pushState()__ function.

* title:

  This is currently ignored by most browsers and it is safe to just pass an
  empty string or a title here.

* url:

  This is the URL for the new history entry. The browser will not attempt to
  load this URL after it calls pushState().

Why don't we go ahead and create a new url in our browser

```JavaScript
var newState = {
  goal: "Learn about pushState()"
};

window.history.pushState(newState, "new state", "new-state");
```

You should notice that your browser has now changed to show `new-state` at the
end of your URL address.

Go ahead and type

```JavaScript
window.history.state
```

It should return

```JavaScript
Object { goal: "Learn about pushState()" }
```

If you now use the __window.history.back()__ function you will not go back to
the previous page, but your URL address will return to the original URL address.
If you use __window.history.forward()__ you will move back to our new URL that
ends in __new-state__

We have now successfully implemented a basic version of __Client-Side__ routing.

As we start learning about __React Router__ we will start implementing
__pushState()__ within the context of a __React__ app.

## Resources

* [React Router Tutorial](https://reacttraining.com/react-router/web/guides/quick-start)
* [Manipulating Browser History](https://developer.mozilla.org/en-US/docs/Web/API/History_API)

<p class='util--hide'>View <a href='https://learn.co/lessons/react-introduction-to-react-router'>React Introduction To React Router</a> on Learn.co and start learning to code for free.</p>
