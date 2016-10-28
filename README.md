# Introduction to React Router
## Objectives

1. How client-side routing works
2. What the trade-off are for client-side routing
3. What `pushState` is


### Client-Side Routing

So we've have learned about building components, changing state, moving state to a store using redux, actions, reducers, etc..., but you are probably wondering how can I make an app with multiple URLs that contain different components. I mean not every app is a todo list, tic-tac-toe or a spreadsheet. So how do we build an app that allows us to have unique pages for the user to see? This is where `Client-Side` routing comes in.  

Client-Side routing is a different beast then what we are used to with traditional server side routing with (Rails, Sinatra, Node/Express, etc..) because we aren't actually making HTTP GET requests anymore.

Lets say that our Client-Side app is going to have these routes

https://www.movie-maker-2016/movies/new

https://www.movie-maker-2016/movies

https://www.movie-maker-2016/about

https://www.movie-maker-2016/login

well the `server` is only going to render the same `HTML`. Which will look like this.

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

With Client-Side routing, it is now the responsibility of the Client-Side-Code to handle the routing, fetching and displaying of the data in the browser instead of the server.

We do get some great benefits though. The major one is *Speed*. Since we are only making one request to the server we don't have to wait for a round trip server call for each page change. We have everything stored on the Client-Side already so we just notify our Client-Side code to display this info for us as we need it.

### Single Page App (SPA)

In React we will most likely be building a `SPA`. This means there will never be a new page being loaded just the original GET request that will load the initial HTML, CSS and JS files from the Server. So we need to figure out how to make the experience of Client-Side routing work for us.

There are a couple of things that we need to take into consideration:

* We want to make sure that we have a URL that displays what the user is doing at that moment. So if they are viewing a bio page it might look like this https://worlds-best-app/bio instead of this https://worlds-best-app.

* We want a user to be able to use the browser's back and forward buttons with ease.

* We want a user to be able to input a URL into the address bar and navigate to the view they need to see.

This was easy with server side rendering most MVC frameworks come with this for free, because we just defined the routes, added the actions needed to the controller and then made a call to the model to get the info we desired.


### Limits of Client-Side routing

So this all sounds great, but what are the limitations?

* Loading of CSS & Javascript

  Since we are now loading all of our CSS and Javascript on the initial GET request it can take a while to load our first page. This can be important as the first page load can take a long time if you have a huge application.

 * Analytics

  Analytic tools normally track page views, but a SPA doesn't have pages in the traditional sense, so this makes it harder for Analytical tools to track page views. We will need add extra scripts to handle this limitation.

  * They are much harder to design.

  We have to plan out all the possibilities that might happen on the Client-Side, this might feel like we are repeating designs that we have already completed with out server routes and and models.

### Push it, Push it

When we make server calls we are making a GET request to a URL and that new URL is in our address bar. If we have visited a few different URL's though that information is saved in browser history.

Go to the JavaScript console in Chrome and type

```JavaScript
window.history
```

This should return the following code.

```JavaScript
History {length: 32, state: null, scrollRestoration: "auto"}
```

The length is how many locations you have visited in this window session.

Now if you type the following code it will take you to the last location in your browser history.

```JavaScript
window.history.back()
```

Go ahead and try it out.

.............
............
..........

Oh good, your back!! :)

![](http://i.giphy.com/10VbdHyZElXqso.gif)

So that is the JavaScript to emulate the experience of using the back button in the browser toolbar. You can also move forward using `window.history.forward()`.

With the JavaScript's History API we also have the ability to `pushState()` to the history entries. This method takes in three parameters `pushState(state, title, url)`

* state object:

  This is a plain JavaScript object that is associated with the new history entry we are going to create with the `pushState()` function.

* title:

  This is currently ignored by most browser and it is safe to just pass an empty string or a title here.

* url:

  This is the URL for the new history entry. The browser will not attempt to load this URL after it calls pushState().

Why don't we go ahead and create a new url in our browser

```JavaScript
var newState = {
    goal: "Learn about pushState()"
}

window.history.pushState(newState, "new state", "new-state")
```

You should notice that your browser has now changed to show `new-state` at the end of your URL address.

Go ahead and type

```JavaScript
window.history.state
```

It should return

```JavaScript
Object {goal: "Learn about pushState()"}
```

If you now use the `window.history.back()` you will not go back to the previous page, but your URL address will return to the original URL address. If you use `window.history.forward()` you will move back to our new URL that ends in `new-state`

We have now successfully implemented a basic version of client-side routing.

As we start learning about React-Router we will start implementing `pushState()` within the context of a React app. 

## Resources

* [React Router Tutorial](https://github.com/reactjs/react-router-tutorial/tree/master/lessons/01-setting-up)
* [Manipulating Browser History](https://developer.mozilla.org/en-US/docs/Web/API/History_API)
