---
title: 使用 Express.js 和 TypeScript 开发 CRUD 应用程序
description: 
published: true
date: 2023-01-31T02:57:44.935Z
tags: 
editor: markdown
dateCreated: 2023-01-31T02:57:43.309Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Developing CRUD Applications with Express.js and TypeScript***English** version of this document is available*](/en/Knowledge-base/TypeScript/developing-crud-applications-with-express-js-and-typescript)
{.links-list}


# 使用 Express.js 和 TypeScript 开发 CRUD 应用程序

最常见的 Web 应用程序类型是 CRUD 应用程序。 CRUD 代表创建、读取、更新、删除。 CRUD 应用程序用于管理数据。在本文中，我们将讨论如何使用 Express.js 和 TypeScript 开发 CRUD 应用程序。

## 什么是 Express.js？

Express.js 是 Node.js 的 Web 应用程序框架。它用于后端开发。 Express.js 提供了一组特性和功能，使开发过程更加容易。

## 什么是打字稿？

TypeScript 是一种编程语言，是 JavaScript 的超集。它主要用于开发大型应用程序。 TypeScript 是一种类型化语言，这意味着它允许您声明具有特定数据类型的变量。这有助于避免在为变量分配不同数据类型的值时可能发生的错误。

## 开发 CRUD 应用程序

在本节中，我们将使用 Express.js 和 TypeScript 开发一个 CRUD 应用程序。我们将为我们的应用程序使用 MongoDB 数据库。

### 设置项目

首先，我们需要为我们的项目创建一个新目录。我们将把我们的项目命名为“crud-app”。

```
mkdir crud-app
```

接下来，我们需要使用 npm 初始化我们的项目。我们将使用“--typescript”标志将我们的项目初始化为 TypeScript 项目。

```
npm init --typescript
```

这将在我们的项目目录中创建一个“package.json”文件。该文件包含有关我们项目的信息，例如我们项目所需的依赖项。

现在，我们需要为我们的项目安装依赖项。我们将使用“express”和“mongodb”包。

```
npm install express mongodb
```

我们还需要安装 TypeScript 编译器。我们将为此使用“打字稿”包。

```
npm install typescript
```

最后，我们需要创建一个“tsconfig.json”文件。该文件包含 TypeScript 编译器的配置。我们将在此文件中设置“target”和“outDir”属性。 “目标”属性指定 JavaScript 目标版本。 “outDir”属性指定编译后的 JavaScript 文件将输出到的目录。

```json
{
    "compilerOptions": {
        "target": "es6",
        "outDir": "dist"
    }
}
```

### 创建数据库

首先，我们需要为我们的应用程序创建一个数据库。我们将我们的数据库命名为“crud_db”。

接下来，我们需要在我们的数据库中创建一个集合。我们将把我们的集合命名为“users”。

最后，我们需要将一些数据插入到我们的集合中。我们将插入两个文档，每个用户一个。

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

### 创建 Express.js 服务器

现在，我们需要为我们的服务器创建一个 TypeScript 文件。我们将这个文件命名为“server.ts”。

在这个文件中，我们将首先导入“express”模块。

```javascript
import * as express from 'express';
```

接下来，我们将创建“express”类的一个实例。

```javascript
const app = express();
```

现在，我们需要设置我们的路线。我们将创建两条路线，一条用于每个 CRUD 操作。

对于“创建”路由，我们将使用“POST”方法。

对于“读取”路由，我们将使用“GET”方法。

对于“更新”路由，我们将使用“PUT”方法。

对于“删除”路由，我们将使用“DELETE”方法。

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

最后，我们需要启动我们的服务器。我们将使用“listen”方法来启动我们的服务器。我们将“端口”属性设置为“3000”。

```javascript
app.listen(3000, () => {
    console.log('Server is listening on port 3000');
});
```

### 实现 CRUD 操作

在本节中，我们将为我们的应用程序实施 CRUD 操作。

#### 创建用户

对于“创建”路由，我们需要从请求正文中获取新用户的数据。

接下来，我们将数据插入到“users”集合中。

最后，我们将向客户端发送响应。

```javascript
app.post('/create', async (req, res) => {
    const user = req.body;
    const result = await users.insertOne(user);
    res.send(result);
});
```

#### 读取用户

对于“读取”路由，我们需要从请求中获取“id”参数。

接下来，我们将查询具有匹配“id”的文档的“users”集合。

最后，我们将向客户端发送响应。

```javascript
app.get('/read/:id', async (req, res) => {
    const id = req.params.id;
    const result = await users.findOne({ "_id": ObjectId(id) });
    res.send(result);
});
```

####更新用户

对于“更新”路由，我们需要从请求中获取“id”参数。

接下来，我们将从请求正文中获取更新用户的数据。

然后，我们将查询具有匹配“id”的文档的“users”集合。

最后，我们将更新文档并向客户端发送响应。

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

#### 删除用户

对于“删除”路由，我们需要从请求中获取“id”参数。

接下来，我们将查询具有匹配“id”的文档的“users”集合。

然后，我们将删除文档并向客户端发送响应。

```javascript
app.delete('/delete/:id', async (req, res) => {
    const id = req.params.id;
    const result = await users.findOneAndDelete({ "_id": ObjectId(id) });
    res.send(result);
});
```

## 测试应用程序

现在我们已经实现了 CRUD 操作，我们需要测试我们的应用程序。

我们将从编译我们的 TypeScript 代码开始。

```
tsc
```

这将在“dist”目录中为我们的服务器生成 JavaScript 文件。

接下来，我们需要启动我们的服务器。

```
node dist/server.js
```

现在，我们可以向我们的服务器发送请求来测试 CRUD 操作。

#### 创建用户

为了测试“创建”路由，我们将使用“curl”命令。

```
curl -X POST http://localhost:3000/create -d '{"name":"John Doe","age":30,"email":"john.doe@example.com"}' -H "Content-Type: application/json"
```

这将使用新用户的数据向“创建”路由发送“POST”请求。

#### 读取用户

为了测试“读取”路由，我们将使用“curl”命令。

```
curl http://localhost:3000/read/5f3f6a8ea864fa22a0b1d9f1
```

这将向“read”路由发送“GET”请求，并将“id”参数设置为我们要读取的用户的“id”。

####更新用户

为了测试“更新”路由，我们将使用“curl”命令。

```
curl -X PUT http://localhost:3000/update/5f3f6a8ea864fa22a0b1d9f1 -d '{"name":"John Doe","age":31,"email":"john.doe@example.com"}' -H "Content-Type: application/json"
```

这将向“更新”路由发送一个“PUT”请求，并将“id”参数设置为我们要更新的用户的“id”。

#### 删除用户

为了测试“删除”路由，我们将使用“curl”命令。

```
curl -X DELETE http://localhost:3000/delete/5f3f6a8ea864fa22a0b1d9f1
```

这将向“delete”路由发送“DELETE”请求，并将“id”参数设置为我们要删除的用户的“id”。