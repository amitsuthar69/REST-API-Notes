## Middlewares in ExpressJs

A Middleware is any function that run between a request & a response which helps us to actually handle the request in a better way.

Hence, Middlewares can be used to perform tasks (which are meant to be done before a client gets access to a particular route) such as an authentication process, logging in, error handling, caching or compression.

Example :

```js
const express = require("express");
const app = express();

const name = "amit";
const pass = 12345;

// the middleware function
const authUser = (req, res, next) => {
  if (name == "amit" && pass == 12345) {
    next();
  } else {
    res.send("Unidentified user");
  }
};

app.get("/", (req, res) => {
  res.send("Please Login");
});

app.get("/feed", (req, res) => {
  res.send("Feed Page!");
});

// using middleware for authentication
app.use(authUser);

app.get("/:profile", (req, res) => {
  res.send(`Hello ${req.params.profile}!`);
});

app.listen(8080);
```

### Let's Breakdown the code :

In the above code, we've used `app.use()` method to create a middleware.

The `app.use()` method takes two arguments, **path** and a **middleware function**.

The path argument is optional. If a path is provided, the middleware function will only be executed for requests that are made to the specified path or a subpath of the specified path.

The middleware function **necessarily** takes three arguments, `req`, `res` and `next`.

The `next` argument is required because the middleware function needs to be able to tell Express.js to continue processing the request.

If the `next()` argument is not provided, the request will be left hanging. This means that the server will not send a response to the client.

---

### Order of creation :

Any middleware functions that are registered after any middleware function that does not provide the `next()` argument will not be executed.

**Hence, While creating middlewares, the order of it's creation matters a lot.**

From our code, the client can use the `/feed` endpoint without passing the authentication but cannot use the `:/profile` endpoint as a middlewares comes in between.

```js
// accessible without authenication
app.get("/feed", (req, res) => {
  res.send("Feed Page!");
});

app.use(authUser); // a middleware layer

app.get("/:profile", (req, res) => {
  res.send(`Hello ${req.params.profile}!`);
});
```
