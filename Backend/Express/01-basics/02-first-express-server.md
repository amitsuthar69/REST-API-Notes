## First Express Server

```js
// import express module
const express = require("express");

// creating an instance of express function
const app = express();

// creating routes : app.method(path, handler)
app.get("/", (req, res) => {
  res.send("Hello world!");
});

app.listen(3000, () => {
  console.log(`Server running on http://localhost:3000`);
});
```

Run this code using `node server.js`

This will start the server. To test this app,
open your browser and go to http://localhost:3000
and a message will be displayed on the screen.

---

### Let's breakdown this code :

1. **app.get('/')** : This is a route definition. It sets up a route for the HTTP **GET** method and specifies the URL path as '/', which means the **root path** of the website.

   In simple terms, when someone visits the _homepage of your website_, this route will handle the request

---

2. **(req, res) => { ... }** : This is the handler function for the route. When a request matches the specified route (in this case, a GET request to the root path '/'), Express.js will execute this function

---

3. **req** : This is an abbreviation for "request", and it represents the HTTP **request object**.

   It is a Client's request to server.

   It contains information about the incoming request, such as **"headers, URL parameters, query parameters**, and more.

---

4. **res** : This is an abbreviation for "response", and it represents the HTTP **response object**.

   It is Server's response to client.

   It allows server to send back a response to the client who made the request.

---

5. **res.send()** : As the name suggests, this method sends the server's response to the client. The content inside this send method.

   The data passed in `.send` method can be a string, an object, an array, etc.

---

6. **app.listen()** : This is a method to make your server listen on a specific port.

   This method takes a `port`, and a callback function which runs when the server starts listening.
