---
title: 使用 Express.js 构建 REST API
description: 
published: true
date: 2023-02-06T13:55:51.701Z
tags: 
editor: markdown
dateCreated: 2023-02-06T13:55:50.114Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Building REST APIs with Express.js***English** document is available*](/en/Knowledge-base/Backend/building-rest-apis-with-express-js)
{.links-list}


# 使用 Express.js 构建 REST API

如果您希望使用 Node.js 构建 REST API，您可能希望使用流行的 Express.js 框架。在本文中，我们将向您展示如何使用 Express.js 构建基本的 REST API。

## 什么是 REST API？

在我们开始之前，让我们先简要回顾一下什么是 REST API。 REST (Representational State Transfer) 是一种用于构建 Web 服务的架构风格。 REST API 定义了一组可对资源执行的操作，这些资源通常由 URL 标识。

例如，如果您有一个博客，您可能有一个代表所有博客帖子的“/posts”资源，并且每个帖子都有自己的 URL。要创建新帖子，您可以将 POST 发送到 `/posts` 资源。要查看特定帖子，您需要“获取”该帖子的 URL。要更新帖子，您将“PUT”到帖子的 URL，要删除帖子，您将“DELETE”帖子的 URL。

这些只是一些最常见的操作，但还有更多可以对资源执行的操作。

## 设置 Express.js

现在我们知道什么是 REST API，让我们开始设置 Express.js。您需要做的第一件事是安装 Express.js 框架。您可以使用节点包管理器 (NPM) 执行此操作。

```
npm install express
```

安装 Express.js 后，您可以创建一个新的 `app.js` 文件并需要 Express.js 模块。

```javascript
const express = require('express');
const app = express();
```

接下来，我们需要设置几条路线。路由由 HTTP 方法和 URL 模式定义。对于我们的示例，我们将创建一个用于“获取”所有帖子的路由和一个用于“发布”新帖子的路由。

```javascript
app.get('/posts', (req, res) => {
  // Get all posts
});

app.post('/posts', (req, res) => {
  // Create a new post
});
```

我们还可以通过 id 为 `PUT`ting 和 `DELETE`ing 帖子定义路由。

```javascript
app.put('/posts/:id', (req, res) => {
  // Update a post
});

app.delete('/posts/:id', (req, res) => {
  // Delete a post
});
```

在 `PUT` 和 `DELETE` 路由中，我们使用了一个 URL 参数 `:id`，它表示我们要更新或删除的帖子的 ID。我们可以使用 `req.params` 对象在路由处理函数中访问这个 id。

```javascript
app.put('/posts/:id', (req, res) => {
  const id = req.params.id;
  // Update a post
});

app.delete('/posts/:id', (req, res) => {
  const id = req.params.id;
  // Delete a post
});
```

现在我们已经定义了路由，我们需要启动 Express.js 服务器。我们可以通过调用 app.listen 方法并传入端口号来完成此操作。我们还将添加一个 `console.log` 语句，以便我们知道服务器何时运行。

```javascript
app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

## 测试 API

现在我们的服务器已启动并运行，让我们测试我们的 API。我们可以使用像 Postman 这样的工具向我们的 API 发出 HTTP 请求。

首先，让我们“获取”所有帖子。我们应该看到一个空数组作为响应，因为我们还没有添加任何帖子。

![获取所有帖子](https://i.imgur.com/VmYbU7D.png)

接下来，让我们 `POST` 一个新帖子。我们需要将 `Content-Type` 标头设置为 `application/json` 并传入带有帖子的 `title` 和 `body` 的 JSON 正文。

![发布新帖子](https://i.imgur.com/WBY4KdI.png)

如果我们再次“获取”所有帖子，我们应该会在响应中看到我们的新帖子。

![获取所有带有新帖子的帖子](https://i.imgur.com/YB7qAFs.png)

最后，让我们 `PUT` 更新我们的帖子并 `DELETE` 它。我们需要再次将“Content-Type”标头设置为“application/json”，并在 URL 中传入帖子的“id”。对于更新，我们只更改帖子的“标题”。

![发布更新](https://i.imgur.com/YB7qAFs.png)

如果我们再次 `GET` 帖子，我们应该看到更新后的 `title`。

![获取更新标题的帖子](https://i.imgur.com/VmYbU7D.png)

现在，让我们“删除”帖子。

![删除帖子](https://i.imgur.com/VmYbU7D.png)

如果我们再次 `GET` 所有帖子，我们应该看到该帖子已被删除。

![获取所有已删除帖子的帖子](https://i.imgur.com/VmYbU7D.png)

就是这样！您现在已经使用 Express.js 成功构建了一个基本的 REST API。

## 外部资源

- [REST API 教程](https://www.restapitutorial.com/)
- [Express.js](https://expressjs.com/)
- [Node.js](https://nodejs.org/)