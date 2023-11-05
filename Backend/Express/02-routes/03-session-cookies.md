# Session and Cookies

## 1. Session

When a user visits a website, the server creates a unique session ID for the user. This session ID is then stored in a cookie on the user's browser.

On each subsequent request to the server, the browser sends back the session cookie, which allows the server to identify the user and track their session.

Sessions end when the user closes their browser or logs out of the website. The server then deletes the session data.

## 2. Cookie

A cookie is a small text file that is stored on the user's computer by a website.

Cookies store a variety of information, such as login status, shopping cart contents, and language preferences. Cookies can also be used to track the user's activity across multiple websites.

Cookies can be either persistent or session cookies. Persistent cookies are stored on the user's computer until they expire or are deleted by the user.

### In short,

A **session** is some kind of data stored on the server by the client and is sent thorugh a request and **cookie** on the other hand is the data stored on the client (browser) by the server and is sent as a response.

---

To Deal with sessions in express, we need to install the package `express-session`

1. Setting up the session :

To setup the session on server we can use the middleware `app.use(session({...}))`, this `session()` function takes an object as a parameter.

This object takes values such as `resave`, `saveUninitialized` and a `secret`.

```js
const express = require("express");
const app = express();
const session = require("express-session");

app.use(
  session({
    // avoid saving the value of session if its not changed
    resave: false,

    // avoid saving uninitialized data on server
    saveUninitialized: false,

    // a secret key to encrypt the data
    secret: "literallyAnythingYouCanType",
  })
);

app.listen(3000);
```

2. Creating a session :

To create a session and store some value in it, we can use the `req.session.sessionName` method inside any of our route.

As session is stored on our server, it is always requested from the browser.

```js
// ...

app.get("/", (req, res) => {
  req.session.mySession = "this is my session";
  res.send("Hello World");
});

app.get("/newpage", (req, res) => {
  // can access the session on any route.
  console.log(req.session);
});

// ...
```

Hence, whenever you visit the '/' route, **for your browser** "`mySession = this is my session`" is saved on the server. But the repetiton of saving this data on server is avoided as we've marked `resave` to `false`.

**Once a session is created on the server, then it can be accessed thorugh any route of your app.**

`console.log(req.session);` will log out an session object which looks like :

```js
Session {
    cookie: {
        path: '/', _expires: null, originalMaxAge: null, httpOnly: true
    }
    mySession: "this is my session", // our saved value
}
```

**During Development, restarting / reloading the server makes the session loose the value we've saved. So revisit the same route to create that session again.**

3. Deleting a session :

To delete a session, we can us the `req.session.destroy(() => {})` method which takes an optional callback function as an argument.

```js
// ...

app.get("/deleteSession", (req, res) => {
  req.session.destroy((err) => {
    err && throw err;
    res.send("Session Removed");
  });
});

// ...
```

---

Now to Deal with cookies in express, we need to install the package `cookie-parser`

1. Setting up the cookies :

To setup the cookie on browser, require the package and we can use the `cookieParser()` middleware to parse cookies.

```js
const express = require("express");
const app = express();
const cookieParser = require("cookie-parser");

app.use(cookieParser());

app.listen(3000);
```

2. Creating a cookie :

To create a cookie, we can use the `res.cookie("name", value)` method which takes the cookie name and it's value as an argument.

As cookies are stored on the browser, they are always sent as a response by our server.

```js
// ...

app.get("/", (req, res) => {
  res.cookie("myCookie", "this is my cookie");
  res.send("Hello World");
});

// to read the cookie, we need to find it inside the request body.
app.get("/read", (req, res) => {
  console.log(req.cookies);
});

// ...
```

`console.log(req.cookies);` will log out an cookie object which looks like :

```js
{
    "connect.sid": "s:blablablablablablablabla",
    myCookie: "this is my cookie", // our saved value
}
```

3. Deleting a cookie :

To delete a cookie, we can us the `res.clearCookie("cookieName")` method which takes the cookie name to be deleted. The `clearCookie()` method can also be used to clear all cookies.

```js
// ...

app.get("/delete", (req, res) => {
  res.clearCookie("myCookie");
});

// ...
```
