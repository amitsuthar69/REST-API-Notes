# Mongoose JS

- Mongoose is a MongoDB library similar to **Mongo Client**.

- Mongoose is an Object Data Modeling (ODM) library for MongoDB, a popular open-source NoSQL database. MongoDB stores data in a flexible, **schema-less** format, allowing documents to have varying structures within a collection.

- Mongoose provides a way to work with MongoDB using a more structured and organized approach by defining schemas for your data.

- Install mongoose to your project : `npm install mongoose`

---

1. Require Mongoose :

Create a file `users.js` and require the mongoose package.

```js
const mongoose = require("mongoose");
```

2. Create a Schema :

As schema is the internal representation for the document, we can define the values and their types based on our need.

`moongose.Schema({...})` method takes an object for the schema with value and their types as a key-value pair.

```js
const userSchema = mongoose.Schema({
  name: String,
  age: Number,
  gender: String,
});
```

3. Create the model :

Once we've our schema, we can now create our model (Collection) based on our defined schema.

`mongoose.model("ModelName", SchemaToBeFollowed)` methods takes two parameters, The model name and the schema it'll follow.

```js
mongoose.model("Users", userSchema);
```

4. export the model :

Once we've our model ready, we need to export it inorder to make a collection on our db.

we can export it using generic `module.exports` method.

```js
module.exports = mongoose.model("Users", userSchema);
```

---

## CRUD Operations:

1. Create a `index.js` file to write the express code. Require the model from "./users"

```js
const express = require("express");
const app = express();
const userModel = require("./users"); // require the model

app.get("/", (req, res) => {
  res.send("Hello world");
});

app.listen(3000);
```

2. using the model to create a user :

To perform a create operation, we can use the `modelName.create({...})` method. This method takes an object with values to be sent into the db.

```js
// above code...

app.get("/create", async (req, res) => {
  const user = await userModel.create({
    name: "Amit",
    age: 19,
    gender: "Male",
  });
  res.send("User created!");
  console.log(user);
});

// below code...
```

3. Read / find users from the collection :

To read all the users from the collection, we can use `modelName.find()` method which returns an **array** containing each and every document from the collection.

```js
// ...

app.get("/getUsers", async (req, res) => {
  const users = await userModel.find();
  res.send(users);
});

// ...
```

There are other similar methods to `find()`, like `findOne({...})` which finds a specific document based on the value passed inside the object.

eg : `userModel.findOne({ username: "Amit" })`will return me the document where username = Amit. Passing non-existng value inside this method returns `null`.

3. Delete a user form collection :

To delete a document form the colllection, we can use the `modelName.findOneAndDelete({...})` method the delete a specific document based on the value passed inside the object.

```js
// ...

app.get("/delete", async (req, res) => {
  const deletedUser = await userModel,
    findOneAndDelete({
      usrename: "Amit",
    });
    console.log(deletedUser);
});

// ...
```
