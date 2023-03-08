---
title: 使用 Node.js 和 Express 构建 RESTful API
description: 
published: true
date: 2023-02-07T02:19:10.902Z
tags: 
editor: markdown
dateCreated: 2023-02-07T02:19:09.189Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Building RESTful APIs with Node.js and Express***English** document is available*](/en/Knowledge-base/Nodejs/building-restful-apis-with-node-js-and-express)
{.links-list}


# 使用 Node.js 和 Express 构建 RESTful API

Node.js 是用于构建服务器端应用程序的强大平台。在本文中，我们将向您展示如何使用 Node.js 和 Express 构建 RESTful API。

## 什么是 REST API？

REST API 是一种应用程序编程接口，它使用 HTTP 请求来获取、放置、发布和删除数据。 REST API 可用于从服务器访问资源，使其成为为 Web 或移动应用程序构建后端的完美工具。

## 为什么使用快递？

Express 是一个流行的框架，用于在 Node.js 上构建 Web 应用程序。它轻巧易用，是构建 RESTful API 的绝佳选择。

## 使用 Node.js 和 Express 创建 REST API

现在我们知道什么是 REST API 以及为什么要使用 Express 创建一个，让我们开始吧！

我们将创建一个简单的 REST API，允许用户管理待办事项列表。我们的 API 将具有以下端点：

- `GET /todos`：获取所有待办事项列表
- `POST /todos`: 创建一个新的待办事项
- `PUT /todos/:id`: 更新待办事项
- `DELETE /todos/:id`: 删除待办事项

### 设置 Node.js 项目

让我们从设置一个新的 Node.js 项目开始。我们将使用 [Express 生成器](https://expressjs.com/en/starter/generator.html) 来创建我们的项目。

首先，全局安装 Express 生成器：

```
npm install -g express-generator
```

接下来，使用 Express 生成器创建一个新项目：

```
express todo-api
```

这将创建一个名为“todo-api”的新目录，其中包含您入门所需的基本文件和目录。

接下来，切换到您的新项目目录并安装依赖项：

```
cd todo-api
npm install
```

现在已经安装了依赖项，您可以启动开发服务器：

```
npm start
```

您应该看到以下输出：

```
> todo-api@0.0.0 start /Users/<user>/<path>/todo-api
> node ./bin/www

```

您现在可以通过 http://localhost:3000 访问该应用程序。

### 定义待办事项模型

我们的 API 会将待办事项存储在数据库中。我们将使用 [MongoDB](https://www.mongodb.com/) 作为我们的数据库，使用 [Mongoose](https://mongoosejs.com/) 作为我们的数据库库。

首先，安装猫鼬：

```
npm install mongoose --save
```

接下来，在 ./models/Todo.js 中创建一个新文件并添加以下代码：

```javascript
const mongoose = require('mongoose');

const todoSchema = new mongoose.Schema({
  name: String,
  completed: Boolean
});

const Todo = mongoose.model('Todo', todoSchema);

module.exports = Todo;
```

此代码定义了一个包含两个字段的“Todo”模型：“name”和“completed”。

### 连接数据库

现在我们已经定义了我们的模型，我们需要连接到数据库。我们将在 ./bin/www 文件中执行此操作。

打开 ./bin/www 并添加以下代码：

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

此代码执行以下操作：

- 使用 Mongoose 连接到 MongoDB 数据库
- 在指定端口启动 Express 服务器

### 定义 API 路由

现在我们已经设置好模型和数据库，可以开始定义 API 路由了。

我们将从定义“GET /todos”路由开始。此路由将返回数据库中所有待办事项的列表。

打开 ./routes/index.js 并添加以下代码：

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

此代码定义了一个“GET /todos”路由，该路由使用“Todo.find()”方法从数据库中获取所有待办事项。

如果查询成功，将在 JSON 响应中返回 `todos` 数组。如果出现错误，则会返回“500 Internal Server Error”和错误消息。

接下来，让我们定义 `POST /todos` 路由。此路线将用于创建新的待办事项。

将以下代码添加到 ./routes/index.js 中：

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

此代码定义了一个 POST /todos 路由，该路由从 `req.body` 对象创建一个新的 `Todo`。 `save()` 方法用于将待办事项保存到数据库中。

如果保存成功，新的待办事项将在 JSON 响应中返回。如果出现错误，则会返回“500 Internal Server Error”和错误消息。

接下来，让我们定义 PUT /todos/:id 路由。该路线将用于更新现有的待办事项。

将以下代码添加到 ./routes/index.js 中：

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

此代码定义了一个 `PUT /todos/:id` 路由，该路由使用 `findByIdAndUpdate()` 方法使用 URL 中指定的 `id` 更新待办事项。 `todo` 对象使用来自 `req.body` 的数据更新。

如果更新成功，更新后的待办事项将在 JSON 响应中返回。如果出现错误，则会返回“500 Internal Server Error”和错误消息。

最后，让我们定义 `DELETE /todos/:id` 路由。此路线将用于删除现有的待办事项。

将以下代码添加到 ./routes/index.js 中：

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

此代码定义了一个 DELETE /todos/:id 路由，该路由使用 `findByIdAndRemove()` 方法删除具有 URL 中指定的 `id` 的待办事项。

如果删除成功，则在 JSON 响应中返回删除的待办事项。如果出现错误，则会返回“500 Internal Server Error”和错误消息。

### 测试 API

现在我们已经定义了 API 路由，让我们测试一下吧！我们将使用 [Postman](https://www.getpostman.com/) 来测试我们的 API。

首先，启动开发服务器：

```
npm start
```

接下来，打开 Postman 并创建一个新请求。

对于 GET /todos 路由，我们将使用以下设置：

- 方法：获取
- 网址：http://localhost:3000/todos

![获取待办事项](https://i.imgur.com/wLwvWxH.png)

对于 POST /todos 路由，我们将使用以下设置：

- 方法：POST
- 网址：http://localhost:3000/todos
- 身体：
  - 类型：JSON（应用程序/json）
  - 生的：
    ```json
    {
      "name": "测试任务",
      “完成”：假
    }
    ```

![创建待办事项](https://i.imgur.com/VkzMxK0.png)

对于 PUT /todos/:id 路由，我们将使用以下设置：

- 方法：放置
- 网址：http://localhost:3000/todos/{id}
- 身体：
  - 类型：JSON（应用程序/json）
  - 生的：
    ```json
    {
      "name": "更新待办事项",
      “完成”：真实
    }
    ```

![更新待办事项](https://i.imgur.com/pBKgVnS.png)

对于 DELETE /todos/:id 路由，我们将使用以下设置：

- 方法：删除
- 网址：http://localhost:3000/todos/{id}

![删除待办事项](https://i.imgur.com/wEwJWdl.png)

## 包起来

在本文中，我们向您展示了如何使用 Node.js 和 Express 构建 RESTful API。我们已经定义了一个“Todo”模型并为“GET”、“POST”、“PUT”和“DELETE”请求创建了路由。我们还使用 Postman 测试了我们的 API。

现在您已经了解了如何使用 Node.js 和 Express 构建 REST API，您可以使用这些知识来构建您自己的 API。

## 资源

- [什么是 REST API？](https://www.mulesoft.com/resources/api/what-rest-api)
- [快递](https://expressjs.com/)
- [Node.js](https://nodejs.org/en/)
- [MongoDB](https://www.mongodb.com/)
- [猫鼬](https://mongoosejs.com/)
- [邮递员](https://www.getpostman.com/)