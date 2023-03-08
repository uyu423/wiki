---
title: 055: Integrating TensorFlow.js with MongoDB in Node.js
description: 
published: true
date: 2023-02-02T19:43:46.330Z
tags: 
editor: markdown
dateCreated: 2023-02-02T19:43:44.595Z
---

- [055: Integrando TensorFlow.js con MongoDB en Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/055-integrating-tensorflow-js-with-mongodb-in-node-js)
{.links-list}
- [055：在 Node.js 中集成 TensorFlow.js 和 MongoDB***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/055-integrating-tensorflow-js-with-mongodb-in-node-js)
{.links-list}
- [055: TensorFlow.js와 Node.js의 MongoDB 통합***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/055-integrating-tensorflow-js-with-mongodb-in-node-js)
{.links-list}


# 05: Integrating TensorFlow.js with MongoDB in Node.js

In this post, we'll learn how to integrate TensorFlow.js with MongoDB in Node.js. We'll cover the following topics:

- What is TensorFlow.js?
- What is MongoDB?
- How to install TensorFlow.js and MongoDB
- How to integrate TensorFlow.js with MongoDB

## What is TensorFlow.js?

TensorFlow.js is a JavaScript library for training and deploying machine learning models. It's developed by Google and released under the Apache 2.0 open source license.

TensorFlow.js can be used in a variety of ways, including:

- In the browser, using JavaScript
- In Node.js, using JavaScript
- In a React Native app
- In a Docker container

## What is MongoDB?

MongoDB is a powerful document-oriented database system. It's developed by MongoDB, Inc. and released under the GNU Affero General Public License.

MongoDB can be used in a variety of ways, including:

- As a traditional database system
- As a NoSQL database
- As a document-oriented database
- As a graph database

## How to install TensorFlow.js and MongoDB

Before we can integrate TensorFlow.js with MongoDB, we need to install both TensorFlow.js and MongoDB.

### Installing TensorFlow.js

There are two ways to install TensorFlow.js:

- Using a script tag
- Using a package manager

#### Using a script tag

You can use a script tag to include the TensorFlow.js library in your HTML file.

```html
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.3/dist/tf.min.js"></script>
```

#### Using a package manager

If you're using a package manager like npm or yarn, you can install TensorFlow.js with the following command:

```
npm install @tensorflow/tfjs
```

### Installing MongoDB

There are two ways to install MongoDB:

- Using a script
- Using a package manager

#### Using a script

You can use a script to install MongoDB. The script will download and install MongoDB for you.

```
curl -O https://fastdl.mongodb.org/osx/mongodb-osx-x86_64-4.2.2.tgz
tar -zxvf mongodb-osx-x86_64-4.2.2.tgz
mkdir -p mongodb
cp -R -n mongodb-osx-x86_64-4.2.2/ mongodb
```

#### Using a package manager

If you're using a package manager like Homebrew, you can install MongoDB with the following command:

```
brew install mongodb
```

## How to integrate TensorFlow.js with MongoDB

Now that we have TensorFlow.js and MongoDB installed, we can start integrating them.

To do this, we'll need to do the following:

- Install the MongoDB Node.js driver
- Connect to the MongoDB database
- Create a schema
- Train a model
- Deploy the model

### Install the MongoDB Node.js driver

The first thing we need to do is install the MongoDB Node.js driver. We can do this with the following command:

```
npm install mongodb
```

### Connect to the MongoDB database

Next, we need to connect to the MongoDB database. We can do this with the following code:

```javascript
const MongoClient = require('mongodb').MongoClient;

const url = 'mongodb://localhost:27017';

MongoClient.connect(url, { useNewUrlParser: true }, (err, client) => {
  if (err) throw err;

  const db = client.db('test');

  console.log('Connected to MongoDB');
});
```

### Create a schema

Now that we're connected to the MongoDB database, we need to create a schema. We can do this with the following code:

```javascript
const schema = new mongoose.Schema({
  name: String,
  age: Number,
  gender: String
});
```

### Train a model

Now that we have a schema, we can train a model. We can do this with the following code:

```javascript
const model = tf.sequential();

model.add(tf.layers.dense({ units: 1, inputShape: [1] }));

model.compile({ loss: 'meanSquaredError', optimizer: 'sgd' });

const xs = tf.tensor2d([1, 2, 3, 4], [4, 1]);
const ys = tf.tensor2d([1, 3, 5, 7], [4, 1]);

model.fit(xs, ys, { epochs: 10 }).then(() => {
  model.predict(tf.tensor2d([5], [1, 1])).print();
});
```

### Deploy the model

Finally, we need to deploy the model. We can do this with the following code:

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.use(express.static('public'));

app.get('/', (req, res) => {
  res.sendFile(__dirname + '/index.html');
});

app.listen(port, () => console.log(`Listening on port ${port}`));
```

## Conclusion

In this post, we've learned how to integrate TensorFlow.js with MongoDB in Node.js. We've covered the following topics:

- What is TensorFlow.js?
- What is MongoDB?
- How to install TensorFlow.js and MongoDB
- How to integrate TensorFlow.js with MongoDB

If you have any questions or comments, please feel free to leave them below.