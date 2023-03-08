---
title: Developing CRUD Applications with Express.js and TypeScript
description: 
published: true
date: 2023-01-31T02:57:46.745Z
tags: 
editor: markdown
dateCreated: 2023-01-31T02:57:43.272Z
---

- [Express.js 및 TypeScript로 CRUD 애플리케이션 개발***Korean** version of this document is available*](/ko/Knowledge-base/TypeScript/developing-crud-applications-with-express-js-and-typescript)
{.links-list}
- [Express.js と TypeScript を使用した CRUD アプリケーションの開発***Japanese** version of this document is available*](/ja/Knowledge-base/TypeScript/developing-crud-applications-with-express-js-and-typescript)
{.links-list}
- [使用 Express.js 和 TypeScript 开发 CRUD 应用程序***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/TypeScript/developing-crud-applications-with-express-js-and-typescript)
{.links-list}


# Developing CRUD Applications with Express.js and TypeScript

The most common type of web applications are CRUD applications. CRUD stands for Create, Read, Update, Delete. CRUD applications are used to manage data. In this article, we will be discussing how to develop CRUD applications using Express.js and TypeScript.

## What is Express.js?

Express.js is a web application framework for Node.js. It is used for backend development. Express.js provides a set of features and functions that make the process of development much easier. 

## What is TypeScript?

TypeScript is a programming language that is a superset of JavaScript. It is primarily used for developing large-scale applications. TypeScript is a typed language, which means that it allows you to declare variables with a specific data type. This helps to avoid errors that can occur when a variable is assigned a value of a different data type. 

## Developing a CRUD Application

In this section, we will be developing a CRUD application using Express.js and TypeScript. We will be using the MongoDB database for our application.

### Setting up the project

First, we need to create a new directory for our project. We will name our project "crud-app".

```
mkdir crud-app
```

Next, we need to initialize our project using npm. We will be using the "--typescript" flag to initialize our project as a TypeScript project.

```
npm init --typescript
```

This will create a "package.json" file in our project directory. This file contains information about our project, such as the dependencies that our project requires. 

Now, we need to install the dependencies for our project. We will be using the "express" and "mongodb" packages.

```
npm install express mongodb
```

We also need to install the TypeScript compiler. We will be using the "typescript" package for this.

```
npm install typescript
```

Finally, we need to create a "tsconfig.json" file. This file contains the configuration for the TypeScript compiler. We will set the "target" and "outDir" properties in this file. The "target" property specifies the JavaScript target version. The "outDir" property specifies the directory where the compiled JavaScript files will be output.

```json
{
    "compilerOptions": {
        "target": "es6",
        "outDir": "dist"
    }
}
```

### Creating the database

First, we need to create a database for our application. We will name our database "crud_db". 

Next, we need to create a collection in our database. We will name our collection "users". 

Finally, we need to insert some data into our collection. We will insert two documents, one for each user. 

```json
{
    "_id": ObjectId("5f3f6a8ea864fa22a0b1d9f1"),
    "name": "John Doe",
    "age": 30,
    "email": "john.doe@example.com"
}
```

```json
{
    "_id": ObjectId("5f3f6a8ea864fa22a0b1d9f2"),
    "name": "Jane Doe",
    "age": 28,
    "email": "jane.doe@example.com"
}
```

### Creating the Express.js server

Now, we need to create a TypeScript file for our server. We will name this file "server.ts".

In this file, we will first import the "express" module. 

```javascript
import * as express from 'express';
```

Next, we will create an instance of the "express" class. 

```javascript
const app = express();
```

Now, we need to set up our routes. We will create two routes, one for each CRUD operation. 

For the "create" route, we will use the "POST" method. 

For the "read" route, we will use the "GET" method. 

For the "update" route, we will use the "PUT" method. 

For the "delete" route, we will use the "DELETE" method. 

```javascript
app.post('/create', (req, res) => {
    // TODO: Implement the create route
});

app.get('/read/:id', (req, res) => {
    // TODO: Implement the read route
});

app.put('/update/:id', (req, res) => {
    // TODO: Implement the update route
});

app.delete('/delete/:id', (req, res) => {
    // TODO: Implement the delete route
});
```

Finally, we need to start our server. We will use the "listen" method to start our server. We will set the "port" property to "3000". 

```javascript
app.listen(3000, () => {
    console.log('Server is listening on port 3000');
});
```

### Implementing the CRUD operations

In this section, we will be implementing the CRUD operations for our application.

#### Creating a user

For the "create" route, we will need to get the data for the new user from the request body. 

Next, we will insert the data into the "users" collection. 

Finally, we will send a response to the client. 

```javascript
app.post('/create', async (req, res) => {
    const user = req.body;
    const result = await users.insertOne(user);
    res.send(result);
});
```

#### Reading a user

For the "read" route, we will need to get the "id" parameter from the request. 

Next, we will query the "users" collection for the document with the matching "id". 

Finally, we will send a response to the client. 

```javascript
app.get('/read/:id', async (req, res) => {
    const id = req.params.id;
    const result = await users.findOne({ "_id": ObjectId(id) });
    res.send(result);
});
```

#### Updating a user

For the "update" route, we will need to get the "id" parameter from the request. 

Next, we will get the data for the updated user from the request body. 

Then, we will query the "users" collection for the document with the matching "id". 

Finally, we will update the document and send a response to the client. 

```javascript
app.put('/update/:id', async (req, res) => {
    const id = req.params.id;
    const user = req.body;
    const result = await users.findOneAndUpdate(
        { "_id": ObjectId(id) },
        { $set: user },
        { returnOriginal: false }
    );
    res.send(result);
});
```

#### Deleting a user

For the "delete" route, we will need to get the "id" parameter from the request. 

Next, we will query the "users" collection for the document with the matching "id". 

Then, we will delete the document and send a response to the client. 

```javascript
app.delete('/delete/:id', async (req, res) => {
    const id = req.params.id;
    const result = await users.findOneAndDelete({ "_id": ObjectId(id) });
    res.send(result);
});
```

## Testing the Application

Now that we have implemented the CRUD operations, we need to test our application. 

We will start by compiling our TypeScript code. 

```
tsc
```

This will generate the JavaScript files for our server in the "dist" directory. 

Next, we need to start our server. 

```
node dist/server.js
```

Now, we can send requests to our server to test the CRUD operations. 

#### Creating a user

To test the "create" route, we will use the "curl" command. 

```
curl -X POST http://localhost:3000/create -d '{"name":"John Doe","age":30,"email":"john.doe@example.com"}' -H "Content-Type: application/json"
```

This will send a "POST" request to the "create" route with the data for the new user. 

#### Reading a user

To test the "read" route, we will use the "curl" command. 

```
curl http://localhost:3000/read/5f3f6a8ea864fa22a0b1d9f1
```

This will send a "GET" request to the "read" route with the "id" parameter set to the "id" of the user that we want to read. 

#### Updating a user

To test the "update" route, we will use the "curl" command. 

```
curl -X PUT http://localhost:3000/update/5f3f6a8ea864fa22a0b1d9f1 -d '{"name":"John Doe","age":31,"email":"john.doe@example.com"}' -H "Content-Type: application/json"
```

This will send a "PUT" request to the "update" route with the "id" parameter set to the "id" of the user that we want to update. 

#### Deleting a user

To test the "delete" route, we will use the "curl" command. 

```
curl -X DELETE http://localhost:3000/delete/5f3f6a8ea864fa22a0b1d9f1
```

This will send a "DELETE" request to the "delete" route with the "id" parameter set to the "id" of the user that we want to delete.