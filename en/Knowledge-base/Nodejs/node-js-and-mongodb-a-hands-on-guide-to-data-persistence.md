---
title: Node.js and MongoDB: A Hands-On Guide to Data Persistence
description: 
published: true
date: 2023-01-31T06:43:47.484Z
tags: 
editor: markdown
dateCreated: 2023-01-31T06:43:45.845Z
---

- [Node.js 및 MongoDB: 데이터 지속성에 대한 실습 가이드***Korean** version of this document is available*](/ko/Knowledge-base/Nodejs/node-js-and-mongodb-a-hands-on-guide-to-data-persistence)
{.links-list}
- [Node.js と MongoDB: データ永続化のハンズオン ガイド***Japanese** version of this document is available*](/ja/Knowledge-base/Nodejs/node-js-and-mongodb-a-hands-on-guide-to-data-persistence)
{.links-list}
- [Node.js 和 MongoDB：数据持久化实践指南***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Nodejs/node-js-and-mongodb-a-hands-on-guide-to-data-persistence)
{.links-list}



# Node.js and MongoDB: A Hands-On Guide to Data Persistence

In this article, we'll explore how to use Node.js and MongoDB to persist data. We'll cover the basics of setting up a MongoDB database, creating a Node.js application to interact with the database, and using CRUD operations to manipulate data. By the end of this article, you'll have a firm understanding of how to use Node.js and MongoDB to create a scalable and data-driven application.

## Setting up MongoDB

MongoDB is a powerful document-oriented database system. It has a rich query language and indexing capabilities that make it easy to work with data of any size and complexity. 

To get started with MongoDB, you'll first need to [install the MongoDB Community Server](https://www.mongodb.com/download-center/community). MongoDB is available for Windows, macOS, and Linux. 

Once MongoDB is installed, you can launch the MongoDB daemon with the `mongod` command. This will start the MongoDB server and create a `data` directory to store the database files. 

Next, you'll need to create a configuration file for the MongoDB server. This file is typically named `mongod.conf` and is located in the `bin` directory where MongoDB is installed. The following is a basic configuration file that you can use to get started:

```
storage:
  dbPath: /data/db
  journal:
    enabled: true
```

This file tells MongoDB where to store the database files (in this case, the `/data/db` directory) and enables journaling, which is a feature that provides crash recovery for the database. 

Now that the MongoDB server is up and running, you can connect to it using the `mongo` shell. This will give you a JavaScript interface for interacting with the database. 

## Creating a Node.js Application

Now that we have MongoDB up and running, let's create a Node.js application that can interact with the database. We'll start by creating a basic directory structure for our project:

```
node-mongo
├── config
│   └── mongodb.js
├── controllers
│   └── books.js
├── models
│   └── book.js
├── routes
│   └── books.js
└── app.js
```

We'll place our configuration files in the `config` directory, our controller files in the `controllers` directory, our model files in the `models` directory, and our route files in the `routes` directory. 

The `app.js` file will be the entry point for our application. This is where we'll configure our application and set up the middleware. 

First, let's create the `config/mongodb.js` file. This file will contain our MongoDB configuration:

```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost/node-mongo', {
  useNewUrlParser: true,
  useUnifiedTopology: true
});

const db = mongoose.connection;

db.on('error', console.error.bind(console, 'connection error:'));
db.once('open', function() {
  console.log('Connected to MongoDB');
});

module.exports = db;
```

In this file, we're using the `mongoose` library to connect to our MongoDB database. We're also setting up a `db` variable to reference our database connection. This `db` variable will be available to any file that requires this module. 

Next, let's create the `models/book.js` file. This file will contain our book model:

```javascript
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

const bookSchema = new Schema({
  title: String,
  author: String,
  year: Number,
  genre: String
});

const Book = mongoose.model('Book', bookSchema);

module.exports = Book;
```

This model defines the structure of a book document in our database. We're using the `mongoose.model()` method to create a model from our schema. This model will be used to create documents in our database. 

Now that we have our model defined, let's create our controller. The controller will contain the logic for our CRUD operations. We'll start by creating the `controllers/books.js` file:

```javascript
const Book = require('../models/book');

exports.getBooks = (req, res, next) => {
  Book.find((err, books) => {
    if (err) return next(err);
    res.json(books);
  });
};

exports.getBook = (req, res, next) => {
  Book.findById(req.params.id, (err, book) => {
    if (err) return next(err);
    res.json(book);
  });
};

exports.createBook = (req, res, next) => {
  const book = new Book(req.body);
  book.save((err, book) => {
    if (err) return next(err);
    res.json(book);
  });
};

exports.updateBook = (req, res, next) => {
  Book.findByIdAndUpdate(req.params.id, req.body, (err, book) => {
    if (err) return next(err);
    res.json(book);
  });
};

exports.deleteBook = (req, res, next) => {
  Book.findByIdAndRemove(req.params.id, req.body, (err, book) => {
    if (err) return next(err);
    res.json(book);
  });
};
```

This controller defines the logic for our CRUD operations. We have a `getBooks` method to fetch all books from our database, a `getBook` method to fetch a single book by ID, a `createBook` method to create a new book, an `updateBook` method to update an existing book, and a `deleteBook` method to delete a book. 

Now that we have our controller defined, let's create our routes. We'll start by creating the `routes/books.js` file:

```javascript
const express = require('express');
const router = express.Router();
const booksCtrl = require('../controllers/books');

router.get('/books', booksCtrl.getBooks);
router.get('/books/:id', booksCtrl.getBook);
router.post('/books', booksCtrl.createBook);
router.put('/books/:id', booksCtrl.updateBook);
router.delete('/books/:id', booksCtrl.deleteBook);

module.exports = router;
```

In this file, we're using the `express.Router` class to create a router for our book API. We're then defining the routes for our CRUD operations and mapping them to the appropriate controller methods. 

Finally, we'll define our `app.js` file. This is the entry point for our application:

```javascript
const express = require('express');
const app = express();
const booksRouter = require('./routes/books');
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost/node-mongo');

app.use(express.json());
app.use('/api/v1/books', booksRouter);

app.listen(3000, () => {
  console.log('Server listening on port 3000');
});
```

In this file, we're requiring the dependencies we need for our application. We're then using the `express.json()` middleware to parse JSON requests. 

Next, we're using the `express.Router` class to create a router for our book API. We're then mapping the `booksRouter` to the `/api/v1/books` path. 

Finally, we're telling our application to listen on port 3000. 

## CRUD Operations

Now that we have our application set up, let's look at how to perform CRUD operations. 

### Creating a Book

To create a book, we'll send a POST request to the `/api/v1/books` endpoint with a JSON body containing the book data:

```javascript
{
	"title": "The Great Gatsby",
	"author": "F. Scott Fitzgerald",
	"year": 1925,
	"genre": "Novel"
}
```

### Retrieving a Book

To retrieve a book, we'll send a GET request to the `/api/v1/books/:id` endpoint, where `:id` is the ID of the book we want to retrieve:

```
/api/v1/books/5d908983b3259d1b68e53b4d
```

### Updating a Book

To update a book, we'll send a PUT request to the `/api/v1/books/:id` endpoint with a JSON body containing the updated book data. Only the fields that need to be updated need to be included in the request body:

```javascript
{
	"title": "The Great Gatsby",
	"author": "F. Scott Fitzgerald",
	"year": 1926,
	"genre": "Novel"
}
```

### Deleting a Book

To delete a book, we'll send a DELETE request to the `/api/v1/books/:id` endpoint, where `:id` is the ID of the book we want to delete:

```
/api/v1/books/5d908983b3259d1b68e53b4d
```

## Conclusion

In this article, we've seen how to use Node.js and MongoDB to create a scalable and data-driven application. We've covered the basics of setting up MongoDB, creating a Node.js application to interact with the database, and using CRUD operations to manipulate data.