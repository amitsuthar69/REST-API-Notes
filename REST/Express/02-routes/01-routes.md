## Routes in Express

1. What is a Route :

A route is a path that a server will listen for. When a client makes a request to a specific path, the server will execute the corresponding route handler for that specific endpoint.

---

2. Route Defination :

The following route would define an endpoint for the /products path:

```js
app.get("/products", (req, res) => {
  res.send("Products Page");
});
```

When a client makes a **GET** request to the `/products` path, the server will execute the `(req, res) => { ... }` function.

The route handler can then be used to **send a response to the client**, **perform database queries**, or any other task that is necessary to fulfill the request.

---

3. Route Pramaters :

Route parameters are **placeholders** in a route that can be used to capture values from the URL.

The URLs holding some parameters which contains some values that are generated at runtime are called as **Dynamic URLs**

The following route would capture the product ID from the URL:

```js
app.get("/products/:username", (req, res) => {
  const name = req.params.username;
});
```

As soon as we use a ":" after a "/", the express comes to know that it's a parameter (a variable endpoint).

The `req.params` object contains the values of any route parameters that were captured from the URL.

For example, when the client makes a request to the following URL: `/amit`

The `req.params` object would contain the following property:

```json
{
  "params": {
    "username": "amit"
  }
}
```

---

4. Nested Routes :

Nested routes are routes that are defined within other routes. For example, the following route is a nested route:

```js
app.get("/users/:userId/products", (req, res) => {
  // ...
});
```
