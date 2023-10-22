## What's Express Js

1. Express.js is a popular and powerful web application framework for Node.js, a server-side JavaScript runtime environment.

2. Express.js acts as a middleman between the client (user's browser) and the server, simplifying the process of handling these requests and responses.

3. Express.js is based on the concept of routes. A route is like a mapping between a URL (path) and a specific function or handler.

4. When a user makes a request to a specific URL, Express.js looks for the corresponding route and executes the associated function, generating the response that the client receives.
<hr>

### Node Js vs Express Js

- Why we need an another framework if it can be done using Node js itself ?

1. Node.js itself provides a basic HTTP module for building servers, but it's relatively low-level. Express.js abstracts away some of the complexity of raw HTTP handling, making it faster and easier to create web applications.

2. Express.js provides a clean and organized way to handle routes and map them to specific functions. This makes it easier to manage different URL paths and keeps your code structured and maintainable.

3. While it's possible to build web applications using only Node.js, using Express.js as a framework offers a higher level of abstraction, better organization, and additional features that streamline the development process.

## Getting Started with Express JS

- Install the Express.js package in your Node.js project :

  ```npm install express```

- Create an Entry Point File Create a new file in your project folder and name it `server.js`. 

- This will be the entry point of your Express.js application.

- Set Up Your Express Application In the `server.js` file, import Express and create your application.


## Middlewares

**Middleware** functions are functions that have access to the request object `(req)`, the response object `(res)`, and the `next` middleware function in the application’s request-response cycle. The next middleware function is commonly denoted by a variable named next.

Middleware functions can perform the following tasks:

- Execute any code.
- Make changes to the request and the response objects.
- End the request-response cycle.
- Call the next middleware function in the stack.

If the current middleware function does not end the request-response cycle, it must call `next()` to pass control to the next middleware function. Otherwise, the request will be left hanging.

**In Simple words, A middleware is you can imagine it as a function that executes when a specific route, routes are being hit**

```js
// app.use('/route', callBack());

app.use("/posts", () => {
  console.log("You just visited /posts");
})

app.get('/posts', function(req, res){
   res.send("Hello world!");
)}
```
## Routes
**It's good to have a seperate `routes` folder to have all of your routes in it.**

Make a routes folder and add a file `posts.js` in it. After that add the following code in your `posts.js` file.

```js
const express = require("express");

// import the router function
const router = express.Router();

// now instead of app.get(), we'll use router.get()
router.get("/", (req, res) => {
  // no need to add '/posts' as it serves it now as a root
  res.send("We are on Posts.");
});

router.get("/post1", (req, res) => {
  // add a route for '/' which will serve as /posts/post1
  res.send("This is Post One.");
});

module.exports = router;
```

**Now import router folder in your `server.js` and use a middleware to use routes**
```js
// inside server.js

const postRoutes = require('./routes/posts')
app.use('/posts', postRoutes) 

// app.use(everytime you go to /posts, make sure you go to postRoute)
```