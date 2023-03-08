---
title: Node.js and NoSQL Databases: A Hands-On Guide
description: 
published: true
date: 2023-02-12T19:56:06.428Z
tags: 
editor: markdown
dateCreated: 2023-02-12T19:55:59.647Z
---

- [Bases de datos Node.js y NoSQL: una guía práctica***Spanish** document is available*](/es/Knowledge-base/Nodejs/node-js-and-nosql-databases-a-hands-on-guide)
{.links-list}
- [Node.js 和 NoSQL 数据库：实践指南***Chinese Simplified** document is available*](/zh/Knowledge-base/Nodejs/node-js-and-nosql-databases-a-hands-on-guide)
{.links-list}
- [Node.js 및 NoSQL 데이터베이스: 실습 가이드***Korean** document is available*](/ko/Knowledge-base/Nodejs/node-js-and-nosql-databases-a-hands-on-guide)
{.links-list}


# Node.js and NoSQL Databases: A Hands-On Guide

Node.js is a powerful JavaScript runtime built on Chrome's V8 engine that can be used to build scalable network applications. NoSQL databases are increasingly popular for their flexibility and scalability, making them a natural fit for use with Node.js.

In this article, we'll take a hands-on approach to working with Node.js and NoSQL databases. We'll cover the basics of each technology and then build a simple CRUD application that stores data in a MongoDB database.

## What is Node.js?

Node.js is an open-source, cross-platform runtime environment for developing server-side applications. Node.js applications are written in JavaScript and can be run within the Node.js runtime on OS X, Microsoft Windows, and Linux.

 Node.js provides an event-driven architecture and a non-blocking I/O API that makes it lightweight and efficient. Node.js applications can be run on a single thread, making use of a single CPU core.

## What is NoSQL?

NoSQL is a term used to describe a class of database management systems that differ from traditional relational databases in some key ways.

NoSQL databases are often more scalable than relational databases, as they are designed to handle large amounts of data that can be spread across many commodity servers. NoSQL databases are also often more flexible than relational databases, as they do not require a rigid schema.

## Node.js and NoSQL

Node.js and NoSQL databases are a natural fit, as they are both designed to handle large amounts of data and are horizontally scalable. In addition, the flexible schema of NoSQL databases means that data can be stored in a format that is more natural for JavaScript objects.

One of the most popular NoSQL databases for use with Node.js is MongoDB. MongoDB is a document-oriented database that stores data in JSON-like documents.

## Setting up MongoDB

MongoDB can be downloaded from the MongoDB website (https://www.mongodb.com/). Once MongoDB is installed, the mongodb-server package needs to be installed from npm.

```
$ npm install mongodb-server
```

## Creating a MongoDB Database

MongoDB stores data in collections, which are similar to tables in a relational database. A database can contain multiple collections.

To create a new database, use the MongoDB client to connect to the mongodb server and then use the createDatabase() method.

```javascript
var MongoClient = require('mongodb').MongoClient;

MongoClient.connect('mongodb://localhost:27017/mydatabase', function(err, db) {
   if(err) throw err;

   db.createDatabase('mydatabase', function(err, result) {
      if(err) throw err;
      console.log('Database created!');
   });
});
```

## Inserting Data into a MongoDB Database

Data is inserted into a MongoDB database using the insert() method. The insert() method takes an object as a parameter and inserts it into the collection.

The following example inserts a document into the "users" collection.

```javascript
db.collection('users').insert({
   name: 'John Doe',
   age: 40
}, function(err, result) {
   if(err) throw err;
   console.log('Document inserted!');
});
```

## Querying a MongoDB Database

Data is queried from a MongoDB database using the find() method. The find() method takes a query object as a parameter and returns all documents that match the query.

The following example queries the "users" collection for all documents with an age of 40.

```javascript
db.collection('users').find({
   age: 40
}).toArray(function(err, docs) {
   if(err) throw err;
   console.log(docs);
});
```

## Updating Data in a MongoDB Database

Data is updated in a MongoDB database using the update() method. The update() method takes a query object and an update object as parameters. The update object contains the fields that should be updated and the new values.

The following example updates the name of the user with an _id of 1 to "Jane Doe".

```javascript
db.collection('users').update({
   _id: 1
}, {
   $set: {
      name: 'Jane Doe'
   }
}, function(err, result) {
   if(err) throw err;
   console.log('Document updated!');
});
```

## Deleting Data from a MongoDB Database

Data is deleted from a MongoDB database using the remove() method. The remove() method takes a query object as a parameter and deletes all documents that match the query.

The following example deletes the user with an _id of 1.

```javascript
db.collection('users').remove({
   _id: 1
}, function(err, result) {
   if(err) throw err;
   console.log('Document deleted!');
});
```

## Building a CRUD Application with Node.js and MongoDB

Now that we've covered the basics of Node.js and MongoDB, let's put what we've learned into practice by building a simple CRUD application.

The application will allow users to create, read, update, and delete documents in a MongoDB database.

### Setting up the Project

Create a new directory for the project and initialize it with npm.

```
$ mkdir nodejs-mongodb-crud
$ cd nodejs-mongodb-crud
$ npm init
```

Install the following dependencies from npm.

```
$ npm install express body-parser mongodb
```

### Creating the Server

Create a new file named server.js and add the following code.

```javascript
var express = require('express');
var bodyParser = require('body-parser');
var MongoClient = require('mongodb').MongoClient;

var app = express();
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

var db;

MongoClient.connect('mongodb://localhost:27017/crud', function(err, database) {
   if(err) throw err;
   db = database;
   app.listen(3000, function() {
      console.log('Listening on port 3000');
   });
});
```

The code above creates an Express server and configures the body-parser middleware to parse JSON and URL-encoded data. It also connects to the MongoDB database and saves the database object in the db variable. Finally, it starts the server on port 3000.

### Creating the Routes

Create a new file named routes.js and add the following code.

```javascript
module.exports = function(app, db) {
   app.post('/users', function(req, res) {
      db.collection('users').insert(req.body, function(err, result) {
         if (err) { 
            res.send({ 'error': 'An error has occurred' }); 
         } else {
            res.send(result.ops[0]);
         }
      });
   });
};
```

The code above defines a POST /users route that inserts a document into the "users" collection. The document is taken from the request body. If the insert is successful, the new document is returned in the response.

Add the following code to the end of the server.js file to load the routes.

```javascript
require('./routes')(app, db);
```

### Testing the Application

Start the MongoDB server and the Node.js server.

```
$ mongod
$ node server.js
```

Test the application by sending a POST request to the /users route. You can use curl or Postman for this.

```
$ curl -X POST -H "Content-Type: application/json" -d '{"name": "John Doe", "age": 40}' http://localhost:3000/users
```

You should see the following response.

```json
{"name": "John Doe", "age": 40, "_id": "58c0eb9e4a6e4a1c9c5e4a82"}
```

You can also query the database to see that the document has been inserted.

```
$ mongo
> use crud
> db.users.find()
{"_id":"58c0eb9e4a6e4a1c9c5e4a82","name":"John Doe","age":40}
```

### Updating the Routes

Update the routes.js file with the following code.

```javascript
app.get('/users', function(req, res) {
   db.collection('users').find().toArray(function(err, docs) {
      if (err) { 
         res.send({ 'error': 'An error has occurred' }); 
      } else {
         res.send(docs);
      }
   });
});

app.get('/users/:id', function(req, res) {
   var id = req.params.id;
   db.collection('users').findOne({ '_id': new ObjectID(id) }, function(err, doc) {
      if (err) { 
         res.send({ 'error': 'An error has occurred' }); 
      } else {
         res.send(doc);
      }
   });
});

app.put('/users/:id', function(req, res) {
   var id = req.params.id;
   var user = req.body;
   db.collection('users').update({ '_id': new ObjectID(id) }, user, function(err, result) {
      if (err) { 
         res.send({ 'error': 'An error has occurred' }); 
      } else {
         res.send(user);
      }
   });
});

app.delete('/users/:id', function(req, res) {
   var id = req.params.id;
   db.collection('users').remove({ '_id': new ObjectID(id) }, function(err, result) {
      if (err) { 
         res.send({ 'error': 'An error has occurred' }); 
      } else {
         res.send(req.body);
      }
   });
});
```

The code above defines the following routes:

* GET /users - Returns all documents in the "users" collection
* GET /users/:id - Returns the document with the specified id
* PUT /users/:id - Updates the document with the specified id
* DELETE /users/:id - Deletes the document with the specified id

### Testing the Routes

Test the routes by sending the following requests to the server.

```
$ curl http://localhost:3000/users
$ curl http://localhost:3000/users/58c0eb9e4a6e4a1c9c5e4a82
$ curl -X PUT -H "Content-Type: application/json" -d '{"name": "Jane Doe", "age": 30}' http://localhost:3000/users/58c0eb9e4a6e4a1c9c5e4a82
$ curl -X DELETE http://localhost:3000/users/58c0eb9e4a6e4a1c9c5e4a82
```

You should see the following responses.

```json
[{"_id":"58c0eb9e4a6e4a1c9c5e4a82","name":"John Doe","age":40}]
{"_id":"58c0eb9e4a6e4a1c9c5e4a82","name":"John Doe","age":40}
{"name": "Jane Doe", "age": 30}
{"name": "Jane Doe", "age": 30}
```

## Conclusion

In this article, we've taken a hands-on approach to working with Node.js and NoSQL databases. We've covered the basics of each technology and then built a simple CRUD application that stores data in a MongoDB database.

If you're interested in learning more about Node.js, MongoDB, or NoSQL databases, check out the following resources.

* [Node.js](https://nodejs.org/)
* [MongoDB](https://www.mongodb.com/)
* [NoSQL](https://en.wikipedia.org/wiki/NoSQL)