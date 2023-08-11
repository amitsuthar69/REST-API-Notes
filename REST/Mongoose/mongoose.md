# Mongoose - Playing with the Data

- Mongoose is a MongoDB library similar to **Mongo Client**.

- Mongoose is an Object Data Modeling (ODM) library for MongoDB, a popular open-source NoSQL database. MongoDB stores data in a flexible, **schema-less** format, allowing documents to have varying structures within a collection.

- Mongoose provides a way to work with MongoDB using a more structured and organized approach by defining schemas for your data.

- Install mongoose to your project : `npm install mongoose`

- Make a folder, name it `models`, then make a file & name it `Post.js`

```js
// inside Post.js

const mongoose = require("mongoose");

// Defining a Post Schema
const postSchema = mongoose.Schema({

  // json like object
  name: String,

  // adding extra features, like validation or necessity
  title: {
    type: String,
    required: true,
  },

  description: String,

  date: {
    type: Date,
    default: Date.now,
  },
});

module.export = mongoose.model("Posts", postSchema);
// mongoose.model("name", schema to be followed by name)
```

## Sending data to Database:

```js
// inside /routes/post.js

// Submits a Post
router.post("/", (req, res) => {
  // console.log(req.body);
  const post = new Post({
    name: req.body.name,
    title: req.body.title,
    description: req.body.description,
  });

  post
    .save()
    .then((data) => {
      res.json(data); // displaying data on screen
    })
    .catch((err) => {
      res.json({
        message: err,
      });
    });
});
```

## Optmised way to send data (async-await)

```js
router.post("/", async (req, res) => {
  const post = new Post({
    name: req.body.name,
    title: req.body.title,
    description: req.body.description,
  });

  try {
    const savedPost = await post.save();
    res.json(savedPost);
  } catch (err) {
    res.json({ message: err });
  }
});
```

## Fetching data from database:

```js
// inside /router/posts.js

// Get Back All Of The Posts
router.get("/", async (req, res) => {
  try {
    const getPosts = await Post.find();
    // mongoDB find() method to get all data from database
    res.json(getPosts);
  } catch (err) {
    res.json({ message: err });
  }
});
```
## Fetching a Specific Post using params

```js

/* use /:anyValue, so that whatever goes next to posts/... if matches with one given to data in DB, it gets fetched. 

example : 
If a DB stores a document with id "64d659194e70216866728f96"
then in the browser, /posts/64d659194e70216866728f96 will show the document linked to that id.

NOTE: Here we're specifically using .findById() method to access the Document with its "id".
*/

router.get("/:postId", async (req, res) => {
  try {
    const post = await Post.findById(req.params.postId);
    res.json(post);
  } catch (err) {
    res.json({ message: err });
  }
});
```