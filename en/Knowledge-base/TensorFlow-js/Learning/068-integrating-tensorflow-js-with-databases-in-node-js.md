---
title: 068: Integrating TensorFlow.js with Databases in Node.js
description: 
published: true
date: 2023-02-02T22:43:40.502Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:43:38.875Z
---

- [068: Integración de TensorFlow.js con bases de datos en Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/068-integrating-tensorflow-js-with-databases-in-node-js)
{.links-list}
- [068：在 Node.js 中将 TensorFlow.js 与数据库集成***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/068-integrating-tensorflow-js-with-databases-in-node-js)
{.links-list}
- [068: Node.js의 데이터베이스와 TensorFlow.js 통합***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/068-integrating-tensorflow-js-with-databases-in-node-js)
{.links-list}


# 068: Integrating TensorFlow.js with Databases in Node.js

TensorFlow.js is a powerful tool for machine learning in JavaScript. In this post, we'll show you how to use TensorFlow.js with databases in Node.js.

## Setting up your environment

Before we get started, we need to set up our environment. We'll need to install Node.js and the TensorFlow.js Node.js API.

You can install Node.js from the [Node.js website](https://nodejs.org/en/).

Once you have Node.js installed, you can install the TensorFlow.js Node.js API with the following command:

```
npm install @tensorflow/tfjs-node
```

## Connecting to a database

Now that we have our environment set up, we can start working with databases.

We'll use the [sqlite3](https://www.npmjs.com/package/sqlite3) Node.js module to connect to an SQLite database. SQLite is a lightweight database that doesn't require a separate server.

First, we need to install the sqlite3 module:

```
npm install sqlite3
```

Next, we'll create a file called `database.js` with the following contents:

```javascript
const sqlite3 = require('sqlite3').verbose();

const db = new sqlite3.Database('./database.sqlite3');

db.serialize(() => {
  // create a table
  db.run('CREATE TABLE IF NOT EXISTS items (name, value)');

  // insert some data
  const stmt = db.prepare('INSERT INTO items VALUES (?, ?)');
  for (let i = 0; i < 10; i++) {
    stmt.run(`Item ${i}`, i);
  }
  stmt.finalize();

  // query the data
  db.each('SELECT * FROM items', (err, row) => {
    console.log(row.name + ': ' + row.value);
  });
});

db.close();
```

In this file, we're connecting to an SQLite database called `database.sqlite3`. We're then creating a table called `items` and inserting some data into it.

Finally, we're querying the data from the database and printing it to the console.

To run this file, you can use the following command:

```
node database.js
```

## Using TensorFlow.js with databases

Now that we've seen how to connect to a database, let's take a look at how to use TensorFlow.js with databases.

We'll use the same `database.js` file from the previous section. We'll just add a few lines of code to load the data from the database into a TensorFlow.js `tf.data.Dataset`.

```javascript
const sqlite3 = require('sqlite3').verbose();
const tf = require('@tensorflow/tfjs-node');

const db = new sqlite3.Database('./database.sqlite3');

db.serialize(() => {
  // create a table
  db.run('CREATE TABLE IF NOT EXISTS items (name, value)');

  // insert some data
  const stmt = db.prepare('INSERT INTO items VALUES (?, ?)');
  for (let i = 0; i < 10; i++) {
    stmt.run(`Item ${i}`, i);
  }
  stmt.finalize();

  // query the data
  const dataset = tf.data.Dataset.fromSqlQuery('SELECT * FROM items', db, (err, row) => {
    return {
      name: row.name,
      value: row.value
    };
  });

  // print the data
  dataset.forEachAsync(item => {
    console.log(item.name + ': ' + item.value);
  });
});

db.close();
```

In this file, we're using the `tf.data.Dataset.fromSqlQuery()` function to load the data from the database into a `tf.data.Dataset`. We're then printing the data to the console.

To run this file, you can use the following command:

```
node database.js
```

## Summary

In this post, we've seen how to use TensorFlow.js with databases in Node.js. We've seen how to connect to a database and how to use TensorFlow.js to load data from a database.