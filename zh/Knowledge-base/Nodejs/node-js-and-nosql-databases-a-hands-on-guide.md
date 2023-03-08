---
title: Node.js 和 NoSQL 数据库：实践指南
description: 
published: true
date: 2023-02-12T19:56:01.356Z
tags: 
editor: markdown
dateCreated: 2023-02-12T19:55:59.639Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Node.js and NoSQL Databases: A Hands-On Guide***English** document is available*](/en/Knowledge-base/Nodejs/node-js-and-nosql-databases-a-hands-on-guide)
{.links-list}


# Node.js 和 NoSQL 数据库：实践指南

Node.js 是一个基于 Chrome 的 V8 引擎构建的强大的 JavaScript 运行时，可用于构建可扩展的网络应用程序。 NoSQL 数据库因其灵活性和可扩展性而越来越受欢迎，这使它们非常适合与 Node.js 一起使用。

在本文中，我们将采用实践方法来使用 Node.js 和 NoSQL 数据库。我们将介绍每种技术的基础知识，然后构建一个将数据存储在 MongoDB 数据库中的简单 CRUD 应用程序。

## 什么是 Node.js？

Node.js 是用于开发服务器端应用程序的开源跨平台运行时环境。 Node.js 应用程序是用 JavaScript 编写的，可以在 OS X、Microsoft Windows 和 Linux 上的 Node.js 运行时中运行。

 Node.js 提供了一个事件驱动的架构和一个非阻塞的 I/O API，使其轻量级和高效。 Node.js 应用程序可以在单个线程上运行，利用单个 CPU 内核。

## 什么是 NoSQL？

NoSQL 是一个术语，用于描述一类在某些关键方面不同于传统关系数据库的数据库管理系统。

NoSQL 数据库通常比关系数据库更具可扩展性，因为它们旨在处理可以分布在许多商品服务器上的大量数据。 NoSQL 数据库通常也比关系数据库更灵活，因为它们不需要严格的模式。

## Node.js 和 NoSQL

Node.js 和 NoSQL 数据库是天作之合，因为它们都是为处理大量数据而设计的，并且可以水平扩展。此外，NoSQL 数据库的灵活模式意味着数据可以以更适合 JavaScript 对象的格式存储。

与 Node.js 一起使用的最流行的 NoSQL 数据库之一是 MongoDB。 MongoDB 是一个面向文档的数据库，它将数据存储在类似 JSON 的文档中。

## 设置 MongoDB

MongoDB 可以从 MongoDB 网站 (https://www.mongodb.com/) 下载。安装 MongoDB 后，需要从 npm 安装 mongodb-server 包。

```
$ npm install mongodb-server
```

## 创建一个 MongoDB 数据库

MongoDB 将数据存储在集合中，类似于关系数据库中的表。一个数据库可以包含多个集合。

要创建新数据库，请使用 MongoDB 客户端连接到 mongodb 服务器，然后使用 createDatabase() 方法。

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

## 将数据插入 MongoDB 数据库

使用 insert() 方法将数据插入 MongoDB 数据库。 insert() 方法将一个对象作为参数并将其插入到集合中。

以下示例将文档插入“users”集合。

```javascript
db.collection('users').insert({
   name: 'John Doe',
   age: 40
}, function(err, result) {
   if(err) throw err;
   console.log('Document inserted!');
});
```

## 查询 MongoDB 数据库

使用 find() 方法从 MongoDB 数据库中查询数据。 find() 方法将查询对象作为参数并返回与查询匹配的所有文档。

以下示例查询“users”集合中年龄为 40 的所有文档。

```javascript
db.collection('users').find({
   age: 40
}).toArray(function(err, docs) {
   if(err) throw err;
   console.log(docs);
});
```

## 更新 MongoDB 数据库中的数据

使用 update() 方法在 MongoDB 数据库中更新数据。 update() 方法将查询对象和更新对象作为参数。更新对象包含应更新的字段和新值。

以下示例将 _id 为 1 的用户的名称更新为“Jane Doe”。

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

## 从 MongoDB 数据库中删除数据

使用 remove() 方法从 MongoDB 数据库中删除数据。 remove() 方法将查询对象作为参数并删除所有与查询匹配的文档。

以下示例删除 _id 为 1 的用户。

```javascript
db.collection('users').remove({
   _id: 1
}, function(err, result) {
   if(err) throw err;
   console.log('Document deleted!');
});
```

## 使用 Node.js 和 MongoDB 构建 CRUD 应用程序

现在我们已经了解了 Node.js 和 MongoDB 的基础知识，让我们通过构建一个简单的 CRUD 应用程序将我们学到的知识付诸实践。

该应用程序将允许用户在 MongoDB 数据库中创建、读取、更新和删除文档。

### 设置项目

为项目创建一个新目录并使用 npm 对其进行初始化。

```
$ mkdir nodejs-mongodb-crud
$ cd nodejs-mongodb-crud
$ npm init
```

从 npm 安装以下依赖项。

```
$ npm install express body-parser mongodb
```

### 创建服务器

创建一个名为 server.js 的新文件并添加以下代码。

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

上面的代码创建了一个 Express 服务器并配置了 body-parser 中间件来解析 JSON 和 URL 编码的数据。它还连接到 MongoDB 数据库并将数据库对象保存在 db 变量中。最后，它在端口 3000 上启动服务器。

### 创建路由

创建一个名为 routes.js 的新文件并添加以下代码。

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

上面的代码定义了一个 POST /users 路由，它将一个文档插入到“users”集合中。该文件取自请求正文。如果插入成功，则在响应中返回新文档。

将以下代码添加到 server.js 文件的末尾以加载路由。

```javascript
require('./routes')(app, db);
```

### 测试应用程序

启动 MongoDB 服务器和 Node.js 服务器。

```
$ mongod
$ node server.js
```

通过向 /users 路由发送 POST 请求来测试应用程序。您可以为此使用 curl 或 Postman。

```
$ curl -X POST -H "Content-Type: application/json" -d '{"name": "John Doe", "age": 40}' http://localhost:3000/users
```

您应该会看到以下响应。

```json
{"name": "John Doe", "age": 40, "_id": "58c0eb9e4a6e4a1c9c5e4a82"}
```

您还可以查询数据库以查看文档是否已插入。

```
$ mongo
> use crud
> db.users.find()
{"_id":"58c0eb9e4a6e4a1c9c5e4a82","name":"John Doe","age":40}
```

### 更新路由

使用以下代码更新 routes.js 文件。

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

上面的代码定义了以下路由：

* GET /users - 返回“users”集合中的所有文档
* GET /users/:id - 返回具有指定 ID 的文档
* PUT /users/:id - 使用指定的 id 更新文档
* DELETE /users/:id - 删除具有指定 id 的文档

### 测试路由

通过向服务器发送以下请求来测试路由。

```
$ curl http://localhost:3000/users
$ curl http://localhost:3000/users/58c0eb9e4a6e4a1c9c5e4a82
$ curl -X PUT -H "Content-Type: application/json" -d '{"name": "Jane Doe", "age": 30}' http://localhost:3000/users/58c0eb9e4a6e4a1c9c5e4a82
$ curl -X DELETE http://localhost:3000/users/58c0eb9e4a6e4a1c9c5e4a82
```

您应该会看到以下响应。

```json
[{"_id":"58c0eb9e4a6e4a1c9c5e4a82","name":"John Doe","age":40}]
{"_id":"58c0eb9e4a6e4a1c9c5e4a82","name":"John Doe","age":40}
{"name": "Jane Doe", "age": 30}
{"name": "Jane Doe", "age": 30}
```

## 结论

在本文中，我们采用了一种实践方法来使用 Node.js 和 NoSQL 数据库。我们介绍了每种技术的基础知识，然后构建了一个将数据存储在 MongoDB 数据库中的简单 CRUD 应用程序。

如果您有兴趣了解有关 Node.js、MongoDB 或 NoSQL 数据库的更多信息，请查看以下资源。

* [节点.js](https://nodejs.org/)
* [MongoDB](https://www.mongodb.com/)
* [NoSQL](https://en.wikipedia.org/wiki/NoSQL)