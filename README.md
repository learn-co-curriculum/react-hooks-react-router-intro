# Introduction to React Router
## Objectives

1. How client-side routing works
2. What the trade-off are for client-side routing
3. What `pushState` is



### Client-Side Routing

So we've have learned about building components, changing state, moving state to a store using redux, actions, reducers, etc..., but you are probably wondering how you can make a page with different components. I mean not every app is a todo list, tic-tac-toe or a spreadsheet, so how do we build an app that allows us to have unique pages for the user to see? This is where `Client-Side` routing comes in.  

Client-Side routing is a different beast then what we used with Rails, because we aren't actually making HTTP GET requests anymore.

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


### Limits of Client-Side routing

### Push it, Push it

## Resources

* [React Router Tutorial](https://github.com/reactjs/react-router-tutorial/tree/master/lessons/01-setting-up)
