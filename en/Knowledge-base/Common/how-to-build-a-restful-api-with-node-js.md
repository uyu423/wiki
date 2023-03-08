---
title: How to Build a RESTful API with Node.js
description: 
published: true
date: 2023-03-02T10:32:20.256Z
tags: 
editor: markdown
dateCreated: 2023-03-02T10:32:18.820Z
---

- [Node.js로 RESTful API를 구축하는 방법***Korean** document is available*](/ko/Knowledge-base/Common/how-to-build-a-restful-api-with-node-js)
{.links-list}


Node.js is one of the most popular technologies among developers due to its versatility and scalability. It simplifies the process of building high-performance server-side applications. RESTful APIs have become the preferred way of building web services because of their simplicity, flexibility, and scalability. In this article, we will guide you through the process of building a RESTful API with Node.js.

## What is a RESTful API?

A RESTful API is an architectural style for building web services using HTTP methods such as GET, POST, PUT, and DELETE. It is a lightweight and flexible architecture that is easy to understand and implement. RESTful APIs use a uniform resource identifier (URI) to represent resources and a resource representation format, such as JSON or XML, to transfer data.

## Prerequisites

Before you start building your RESTful API, you need to have the following installed on your system:

- Node.js (v10.16.3 or higher)
- NPM (v6.9.0 or higher)
- An IDE or text editor such as Visual Studio Code or Sublime Text

## Step 1: Setting up the project

To create a new Node.js project, open your terminal or command prompt, navigate to the directory where you want to create your project, and run the following command:

```bash
mkdir my-rest-api
cd my-rest-api
npm init
```

This will create a new Node.js project and initialize a package.json file in the root directory.

## Step 2: Installing dependencies

To build a RESTful API, we need to install several dependencies. Run the following command in your terminal to install them:

```bash
npm install express body-parser cors --save
```

- **express** - A popular Node.js web framework that provides a set of features for building web applications.
- **body-parser** - A middleware for parsing request bodies, such as JSON or URL-encoded.
- **cors** - A middleware for enabling cross-origin resource sharing (CORS) in our API.

## Step 3: Creating the server

Create a new file called `server.js` in the root directory of your project and add the following code:

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const cors = require('cors');

const app = express();

app.use(cors());
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: false }));

const PORT = process.env.PORT || 3000;

app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});
```

This code creates a new `express` application, enables `CORS`, and adds middleware for parsing request bodies. We also set the port to use for the server to `3000`, or to the one specified in the environment variable `PORT`.

## Step 4: Creating the routes

Routes are used to define the endpoints of our API. In this step, we will create a new route for handling `GET` requests.

Create a new file called `routes.js` in the root directory of your project and add the following code:

```javascript
const express = require('express');
const router = express.Router();

router.get('/', (req, res) => {
  res.send('Hello, World!');
});

module.exports = router;
```

This code creates a new `express` router and defines a route for handling `GET` requests to the root endpoint `/`. When a `GET` request is made to this endpoint, the server sends the response `Hello, World!`.

## Step 5: Mounting the routes

To use the routes we created in `routes.js`, we need to mount them in our server.

Add the following code to the `server.js` file:

```javascript
const routes = require('./routes');

app.use('/', routes);
```

This code imports the `routes.js` file and mounts the routes to the root endpoint `/`. When a request is made to the root endpoint, the server will use the routes defined in `routes.js`.

## Step 6: Testing the API

To test our API, start the server by running the following command in your terminal:

```bash
node server.js
```

Open your web browser and navigate to `http://localhost:3000`. You should see the message `Hello, World!` displayed in the browser.

Congratulations! You have successfully built a RESTful API with Node.js.

## Conclusion

Building a RESTful API with Node.js is simple and straightforward. With the help of the `express` framework and its middleware libraries, we can easily handle HTTP requests, define routes, and send responses. By following the steps outlined in this article, you should now be able to create your own RESTful API with Node.js.

## External Resources

- [Express.js official website](https://expressjs.com/)
- [RESTful API Design - Best Practices](https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/)
- [Building a Simple RESTful API with NodeJS and ExpressJS](https://blog.logrocket.com/building-a-simple-restful-api-with-nodejs-and-expressjs/)