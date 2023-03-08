---
title: MongoDB and Node.js: Building a Modern Web Application Stack
description: 
published: true
date: 2023-03-04T13:32:51.607Z
tags: 
editor: markdown
dateCreated: 2023-03-04T13:32:44.340Z
---

- [MongoDB 및 Node.js: 최신 웹 애플리케이션 스택 구축***Korean** document is available*](/ko/Knowledge-base/NoSQL/mongodb-and-node-js-building-a-modern-web-application-stack)
{.links-list}


MongoDB and Node.js: Building a Modern Web Application Stack

Modern web applications are built using different technologies, such as databases, front-end frameworks, and backend languages. In this article, we will explore how to build a modern web application stack using MongoDB and Node.js. 

## What is MongoDB?

MongoDB is an open-source NoSQL document-based database that stores data in a flexible, semi-structured document format called BSON (Binary JSON). MongoDB is designed to scale horizontally, providing high availability and automatic sharding. It is widely used in modern web applications due to its flexibility, scalability, and ease of use.

## What is Node.js?

Node.js is an open-source, cross-platform JavaScript runtime environment that executes JavaScript code outside a browser. Node.js is built on Chrome's V8 JavaScript engine and provides an event-driven, non-blocking I/O model that makes it lightweight, efficient, and ideal for building scalable web applications. 

## Why MongoDB and Node.js?

MongoDB and Node.js are a popular combination for building modern web applications due to their flexibility and scalability. They can handle high volumes of data and provide fast, real-time data access. Additionally, both technologies share the same programming language, JavaScript, which makes it easy to write code that can be executed on both the client and server sides. 

## Building a Modern Web Application Stack with MongoDB and Node.js

To build a modern web application stack with MongoDB and Node.js, we need to create an architecture that separates the concerns of the application. We will create a backend API using Node.js and MongoDB, and a frontend using a modern JavaScript framework such as React or Angular.

### Setting up MongoDB

To set up MongoDB, we need to install the MongoDB server and the MongoDB Node.js driver. The driver enables Node.js to connect and interact with the MongoDB server.

First, we need to install the MongoDB server on our local machine or on a cloud-based service such as MongoDB Atlas. After installing the server, we can install the MongoDB Node.js driver using npm (Node Package Manager). 

```javascript
npm install mongodb
```

Once we have installed the driver, we can connect to the MongoDB server using the MongoClient object provided by the driver. 

```javascript
const { MongoClient } = require('mongodb');

const uri = 'mongodb+srv://<username>:<password>@<cluster-address>/test?retryWrites=true&w=majority';

const client = new MongoClient(uri, {
  useNewUrlParser: true,
  useUnifiedTopology: true,
});

client.connect((err) => {
  if (err) throw err;

  const collection = client.db('test').collection('devices');

  // perform actions on the collection object
  client.close();
});
```

We can now perform CRUD (Create, Read, Update, and Delete) operations on the MongoDB server using the collection object.

### Building the Backend API with Node.js

To build the backend API, we need to create a Node.js application that exposes RESTful endpoints for the frontend to consume. We will use the Express framework to create the API and the MongoDB Node.js driver to interact with the database.

First, we need to create a project folder and initialize it with npm.

```javascript
mkdir myapp
cd myapp
npm init
```

Next, we need to install the required dependencies.

```javascript
npm install express mongodb body-parser
```

We can now create a server.js file that will define our API endpoints and connect to the MongoDB server.

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const { MongoClient } = require('mongodb');

const app = express();
const port = process.env.PORT || 3000;

const uri = 'mongodb+srv://<username>:<password>@<cluster-address>/test?retryWrites=true&w=majority';

const client = new MongoClient(uri, {
  useNewUrlParser: true,
  useUnifiedTopology: true,
});

app.use(bodyParser.json());

app.get('/devices', (req, res) => {
  client.connect((err) => {
    if (err) throw err;

    const collection = client.db('test').collection('devices');

    collection.find().toArray((err, result) => {
      if (err) throw err;

      res.send(result);
    });
  });
});

app.post('/devices', (req, res) => {
  client.connect((err) => {
    if (err) throw err;

    const collection = client.db('test').collection('devices');

    collection.insertOne(req.body, (err, result) => {
      if (err) throw err;

      res.send(result.ops);
    });
  });
});

app.put('/devices/:id', (req, res) => {
  client.connect((err) => {
    if (err) throw err;

    const collection = client.db('test').collection('devices');
    const id = req.params.id;

    collection.updateOne({ _id: id }, { $set: req.body }, (err, result) => {
      if (err) throw err;

      res.send(result);
    });
  });
});

app.delete('/devices/:id', (req, res) => {
  client.connect((err) => {
    if (err) throw err;

    const collection = client.db('test').collection('devices');
    const id = req.params.id;

    collection.deleteOne({ _id: id }, (err, result) => {
      if (err) throw err;

      res.send(result);
    });
  });
});

app.listen(port, () => {
  console.log(`Server listening on port ${port}`);
});
```

We can now start the server and test the API endpoints using a tool such as Postman.

```javascript
npm start
```

### Building the Frontend with React

To build the frontend, we will use React, a popular JavaScript library for building user interfaces. React allows us to create reusable UI components and manage the state of the application in a predictable way.

First, we need to create a React project using the create-react-app tool.

```javascript
npx create-react-app my-app
cd my-app
npm start
```

Next, we can create a Devices component that will display a list of devices fetched from the backend API.

```javascript
import React, { useState, useEffect } from 'react';

function Devices() {
  const [devices, setDevices] = useState([]);

  useEffect(() => {
    fetch('/devices')
      .then(response => response.json())
      .then(data => setDevices(data));
  }, []);

  return (
    <ul>
      {devices.map(device => (
        <li key={device._id}>{device.name}</li>
      ))}
    </ul>
  );
}

export default Devices;
```

We can now use the Devices component in our App component.

```javascript
import React from 'react';
import Devices from './Devices';

function App() {
  return (
    <div>
      <h1>Devices</h1>
      <Devices />
    </div>
  );
}

export default App;
```

We can now start the frontend and test the application in the browser.

```javascript
npm start
```

## Conclusion

In this article, we explored how to build a modern web application stack using MongoDB and Node.js. We learned how to set up MongoDB and connect to it using the MongoDB Node.js driver. We also built a backend API using Node.js and Express and a frontend using React. 

This stack offers flexibility, scalability, and ease of use, making it an excellent choice for building modern web applications. 

## External Resources

- [MongoDB Documentation](https://docs.mongodb.com/)
- [Node.js Documentation](https://nodejs.org/en/docs/)
- [Express Documentation](https://expressjs.com/en/api.html)
- [React Documentation](https://reactjs.org/docs/)