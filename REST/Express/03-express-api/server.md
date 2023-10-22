## A basic only ExpressJs API

```js
const express = require("express");
const app = express();

const products = [
  { id: 1, name: "Product 1", price: 100 },
  { id: 2, name: "Product 2", price: 200 },
  { id: 3, name: "Product 3", price: 300 },
];

// GET /api/products
app.get("/api/products", (req, res) => {
  res.json(products);
});

// POST /api/products
app.post("/api/products", (req, res) => {
  const product = req.body;
  products.push(product);
  res.json(product);
});

// PUT /api/products/:id
app.put("/api/products/:id", (req, res) => {
  const id = req.params.id;
  const product = req.body;
  const productIndex = products.findIndex((p) => p.id === id);
  products[productIndex] = product;
  res.json(product);
});

// DELETE /api/products/:id
app.delete("/api/products/:id", (req, res) => {
  const id = req.params.id;
  const productIndex = products.findIndex((p) => p.id === id);
  products.splice(productIndex, 1);
  res.json({ message: "Product deleted" });
});

app.listen(3000, () => {
  console.log("server running at http://localhost:3000");
});
```

### Code Breakdown :

1. configuration :

```js
const express = require("express");
const app = express();

// ...

app.listen(3000, () => {
  console.log("server running at http://localhost:3000");
});
```

---

2. products array :

```js
const products = [
  { id: 1, name: "Product 1", price: 100 },
  { id: 2, name: "Product 2", price: 200 },
  { id: 3, name: "Product 3", price: 300 },
];
```

Here, we've created an array of objects for our products, In real world, this would be a data being received from a database.

---

3. get method :

```js
app.get("/api/products", (req, res) => {
  res.json(products);
});
```

Here, our server sends the array as a response to the client on the `/api/products` endpoint.

---

4. post method :

```js
app.post("/api/products", (req, res) => {
  const product = req.body;
  products.push(product);
  res.json(product);
});
```

The `app.post()` method is used to create a route that handles POST requests.

This POST request takes the data sent in the request body, stores it in the product variable and then pushes it into the existing array.

The `req.body` property contains the body of the HTTP request. The body of the HTTP request is the data that is sent from the client to the server. In this case, the body of the HTTP request is expected to contain a JSON object that represents a product.

---

5. put method

```js
app.put("/api/products/:id", (req, res) => {
  const id = req.params.id;
  const product = req.body;
  const productIndex = products.findIndex((p) => p.id === id);
  products[productIndex] = product;
  res.json(product);
});
```

This PUT method first takes the id param from the URL and stores it in `id` variable. Then we store the request body inside `product` variable.

The `findIndex()` method is used to find the index of the product in the `products` array that has the same ID as the `id` parameter.

The callback function inside `findIndex()` is executed for each element in the array. The method returns the index of the first element in the array for which the callback function returns a true value.

Then we set the `productIndex`'th element of the array with the new updated one sent in the `req.body` and finally we send the updated json data to the client.

---

6. delete method :

```js
app.delete("/api/products/:id", (req, res) => {
  const id = req.params.id;
  const productIndex = products.findIndex((p) => p.id === id);
  products.splice(productIndex, 1);
  res.json({ message: "Product deleted" });
});
```

In this method, we again get the id, and the particular products whose index matches the id param. Then we use `splice()` method to take out that product from our array, resulting in its deletion.

---

While this is an API built wiith just express, we can also involve a database to send real world data by our API. You can try this API at POSTMAN or ThunderClient.
