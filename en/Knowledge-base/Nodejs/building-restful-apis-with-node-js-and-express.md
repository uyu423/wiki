---
title: Building RESTful APIs with Node.js and Express
description: 
published: true
date: 2023-02-07T02:19:14.965Z
tags: 
editor: markdown
dateCreated: 2023-02-07T02:19:09.192Z
---

- [Creación de API RESTful con Node.js y Express***Spanish** document is available*](/es/Knowledge-base/Nodejs/building-restful-apis-with-node-js-and-express)
{.links-list}
- [使用 Node.js 和 Express 构建 RESTful API***Chinese Simplified** document is available*](/zh/Knowledge-base/Nodejs/building-restful-apis-with-node-js-and-express)
{.links-list}
- [Node.js 및 Express로 RESTful API 구축***Korean** document is available*](/ko/Knowledge-base/Nodejs/building-restful-apis-with-node-js-and-express)
{.links-list}


# Building RESTful APIs with Node.js and Express

Node.js is a powerful platform for building server-side applications. In this article, we'll show you how to build a RESTful API using Node.js and Express.

## What is a REST API?

A REST API is an application programming interface that uses HTTP requests to GET, PUT, POST, and DELETE data. A REST API can be used to access resources from a server, making it a perfect tool for building a back-end for your web or mobile application.

## Why Use Express?

Express is a popular framework for building web applications on Node.js. It is lightweight and easy to use, making it a great choice for building RESTful APIs.

##Creating a REST API with Node.js and Express

Now that we know what a REST API is and why we would use Express to create one, let's get started!

We'll be creating a simple REST API that allows users to manage a to-do list. Our API will have the following endpoints:

- `GET /todos`: Get a list of all to-dos
- `POST /todos`: Create a new to-do
- `PUT /todos/:id`: Update a to-do
- `DELETE /todos/:id`: Delete a to-do

### Setting up a Node.js project

Let's start by setting up a new Node.js project. We'll be using the [Express generator](https://expressjs.com/en/starter/generator.html) to create our project.

First, install the Express generator globally:

```
npm install -g express-generator
```

Next, create a new project using the Express generator:

```
express todo-api
```

This will create a new directory called `todo-api` with the basic files and directories you need to get started.

Next, change into your new project directory and install the dependencies:

```
cd todo-api
npm install
```

Now that the dependencies are installed, you can start the development server:

```
npm start
```

You should see the following output:

```
> todo-api@0.0.0 start /Users/<user>/<path>/todo-api
> node ./bin/www

```

You can now access the application at http://localhost:3000.

### Defining the To-Do model

Our API will store to-dos in a database. We'll use [MongoDB](https://www.mongodb.com/) for our database and [Mongoose](https://mongoosejs.com/) for our database library.

First, install Mongoose:

```
npm install mongoose --save
```

Next, create a new file at `./models/Todo.js` and add the following code:

```javascript
const mongoose = require('mongoose');

const todoSchema = new mongoose.Schema({
  name: String,
  completed: Boolean
});

const Todo = mongoose.model('Todo', todoSchema);

module.exports = Todo;
```

This code defines a `Todo` model with two fields: `name` and `completed`.

### Connecting to the database

Now that we have defined our model, we need to connect to the database. We'll do this in the `./bin/www` file.

Open `./bin/www` and add the following code:

```javascript
#!/usr/bin/env node

/**
 * Module dependencies.
 */

const app = require('../app');
const debug = require('debug')('todo-api:server');
const http = require('http');

/**
 * Get port from environment and store in Express.
 */

const port = normalizePort(process.env.PORT || '3000');
app.set('port', port);

/**
 * Create HTTP server.
 */

const server = http.createServer(app);

/**
 * Connect to MongoDB
 */

const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/todo-api');

/**
 * Listen on provided port, on all network interfaces.
 */

server.listen(port);
server.on('error', onError);
server.on('listening', onListening);

/**
 * Normalize a port into a number, string, or false.
 */

function normalizePort(val) {
  const port = parseInt(val, 10);

  if (isNaN(port)) {
    // named pipe
    return val;
  }

  if (port >= 0) {
    // port number
    return port;
  }

  return false;
}

/**
 * Event listener for HTTP server "error" event.
 */

function onError(error) {
  if (error.syscall !== 'listen') {
    throw error;
  }

  const bind = typeof port === 'string'
    ? 'Pipe ' + port
    : 'Port ' + port;

  // handle specific listen errors with friendly messages
  switch (error.code) {
    case 'EACCES':
      console.error(bind + ' requires elevated privileges');
      process.exit(1);
      break;
    case 'EADDRINUSE':
      console.error(bind + ' is already in use');
      process.exit(1);
      break;
    default:
      throw error;
  }
}

/**
 * Event listener for HTTP server "listening" event.
 */

function onListening() {
  const addr = server.address();
  const bind = typeof addr === 'string'
    ? 'pipe ' + addr
    : 'port ' + addr.port;
  debug('Listening on ' + bind);
}
```

This code does the following:

- Connects to the MongoDB database using Mongoose
- Starts the Express server on the specified port

### Defining the API routes

Now that we have our model and database set up, we can start defining our API routes.

We'll start by defining the `GET /todos` route. This route will return a list of all to-dos in the database.

Open `./routes/index.js` and add the following code:

```javascript
const express = require('express');
const router = express.Router();

const Todo = require('../models/Todo');

/* GET home page. */
router.get('/', function(req, res, next) {
  res.render('index', { title: 'Express' });
});

/* GET all todos. */
router.get('/todos', function(req, res, next) {
  Todo.find({}, function(err, todos) {
    if (err) {
      res.status(500).json({ error: err.message });
    } else {
      res.json(todos);
    }
  });
});

module.exports = router;
```

This code defines a `GET /todos` route that uses the `Todo.find()` method to get all to-dos from the database.

If the query is successful, the `todos` array is returned in the JSON response. If there is an error, a `500 Internal Server Error` is returned with the error message.

Next, let's define the `POST /todos` route. This route will be used to create new to-dos.

Add the following code to `./routes/index.js`:

```javascript
/* POST new todo. */
router.post('/todos', function(req, res, next) {
  const todo = new Todo(req.body);
  todo.save(function(err, todo) {
    if (err) {
      res.status(500).json({ error: err.message });
    } else {
      res.json(todo);
    }
  });
});
```

This code defines a `POST /todos` route that creates a new `Todo` from the `req.body` object. The `save()` method is used to save the to-do to the database.

If the save is successful, the new to-do is returned in the JSON response. If there is an error, a `500 Internal Server Error` is returned with the error message.

Next, let's define the `PUT /todos/:id` route. This route will be used to update existing to-dos.

Add the following code to `./routes/index.js`:

```javascript
/* PUT update todo. */
router.put('/todos/:id', function(req, res, next) {
  const id = req.params.id;
  const todo = req.body;
  Todo.findByIdAndUpdate(id, todo, function(err, todo) {
    if (err) {
      res.status(500).json({ error: err.message });
    } else {
      res.json(todo);
    }
  });
});
```

This code defines a `PUT /todos/:id` route that uses the `findByIdAndUpdate()` method to update a to-do with the `id` specified in the URL. The `todo` object is updated with the data from `req.body`.

If the update is successful, the updated to-do is returned in the JSON response. If there is an error, a `500 Internal Server Error` is returned with the error message.

Finally, let's define the `DELETE /todos/:id` route. This route will be used to delete existing to-dos.

Add the following code to `./routes/index.js`:

```javascript
/* DELETE todo. */
router.delete('/todos/:id', function(req, res, next) {
  const id = req.params.id;
  Todo.findByIdAndRemove(id, function(err, todo) {
    if (err) {
      res.status(500).json({ error: err.message });
    } else {
      res.json(todo);
    }
  });
});
```

This code defines a `DELETE /todos/:id` route that uses the `findByIdAndRemove()` method to delete a to-do with the `id` specified in the URL.

If the deletion is successful, the deleted to-do is returned in the JSON response. If there is an error, a `500 Internal Server Error` is returned with the error message.

### Testing the API

Now that we have defined our API routes, let's test them out! We'll use [Postman](https://www.getpostman.com/) to test our API.

First, start the development server:

```
npm start
```

Next, open Postman and create a new request.

For the `GET /todos` route, we'll use the following settings:

- Method: GET
- URL: http://localhost:3000/todos

![Get To-Dos](https://i.imgur.com/wLwvWxH.png)

For the `POST /todos` route, we'll use the following settings:

- Method: POST
- URL: http://localhost:3000/todos
- Body:
  - Type: JSON (application/json)
  - Raw:
    ```json
    {
      "name": "Test To-Do",
      "completed": false
    }
    ```

![Create To-Do](https://i.imgur.com/VkzMxK0.png)

For the `PUT /todos/:id` route, we'll use the following settings:

- Method: PUT
- URL: http://localhost:3000/todos/{id}
- Body:
  - Type: JSON (application/json)
  - Raw:
    ```json
    {
      "name": "Updated To-Do",
      "completed": true
    }
    ```

![Update To-Do](https://i.imgur.com/pBKgVnS.png)

For the `DELETE /todos/:id` route, we'll use the following settings:

- Method: DELETE
- URL: http://localhost:3000/todos/{id}

![Delete To-Do](https://i.imgur.com/wEwJWdl.png)

## Wrapping Up

In this article, we've shown you how to build a RESTful API using Node.js and Express. We've defined a `Todo` model and created routes for `GET`, `POST`, `PUT`, and `DELETE` requests. We've also tested our API using Postman.

Now that you've seen how to build a REST API with Node.js and Express, you can use this knowledge to build your own APIs.

## Resources

- [What is a REST API?](https://www.mulesoft.com/resources/api/what-rest-api)
- [Express](https://expressjs.com/)
- [Node.js](https://nodejs.org/en/)
- [MongoDB](https://www.mongodb.com/)
- [Mongoose](https://mongoosejs.com/)
- [Postman](https://www.getpostman.com/)