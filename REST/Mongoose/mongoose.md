```js
const mongoose = require("mongoose");

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