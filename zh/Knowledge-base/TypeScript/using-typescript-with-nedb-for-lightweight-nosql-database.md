---
title: 将 TypeScript 与 NeDB 一起用于轻量级 NoSQL 数据库
description: 
published: true
date: 2023-02-09T18:56:28.221Z
tags: 
editor: markdown
dateCreated: 2023-02-09T18:56:26.565Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Using TypeScript with NeDB for Lightweight NoSQL Database***English** document is available*](/en/Knowledge-base/TypeScript/using-typescript-with-nedb-for-lightweight-nosql-database)
{.links-list}


# 将 TypeScript 与 NeDB 一起用于轻量级 NoSQL 数据库

## 介绍

TypeScript 是 JavaScript 的类型化超集，可编译为纯 JavaScript。它提供类、模块和接口来帮助您构建健壮的组件。 TypeScript 是可用于 Node.js 运行时环境的众多语言之一。

NeDB 是一个轻量级的 NoSQL 数据库，可以在 Node.js 和浏览器中使用。它支持 MongoDB API，使其易于与现有的 MongoDB 库和工具一起使用。

在本文中，我们将向您展示如何将 TypeScript 与 NeDB 结合使用。我们将创建一个简单的待办事项应用程序，将数据存储在 NeDB 数据库中。

## 设置 TypeScript 项目

首先，我们需要创建一个 TypeScript 项目。我们将使用 [TypeScript Node Starter](https://github.com/Microsoft/TypeScript-Node-Starter) 项目模板。

```
$ git clone https://github.com/Microsoft/TypeScript-Node-Starter.git todo-app
$ cd todo-app
$ npm install
```

接下来，我们需要安装 NeDB 类型。

```
$ npm install --save-dev @types/nedb
```

## 创建待办事项模型

我们将从创建一个待办事项模型开始。使用以下代码在 `src` 目录中创建一个名为 `todo.ts` 的新文件：

```typescript
export class ToDo {
  _id: string;
  title: string;
  completed: boolean;
  date: Date;

  constructor(title: string) {
    this.title = title;
    this.completed = false;
    this.date = new Date();
  }
}
```

该模型有四个字段：`_id`、`title`、`completed` 和 `date`。 _id 字段是主键，由 NeDB 生成。 `title` 字段是待办事项的标题。 `completed` 字段是一个布尔值，指示待办事项是否已完成。 `date` 字段是创建待办事项的日期。

## 创建待办事项服务

接下来，我们将创建一个待办事项服务。该服务将负责 To-Do 项目的 CRUD 操作。使用以下代码在 `src` 目录中创建一个名为 `todoService.ts` 的新文件：

```typescript
import { Datastore } from 'nedb';
import { ToDo } from './todo';

export class ToDoService {
  private db: Datastore;

  constructor(db: Datastore) {
    this.db = db;
  }

  public async getAll(): Promise<ToDo[]> {
    return new Promise<ToDo[]>((resolve, reject) => {
      this.db.find({}, (err, docs: ToDo[]) => {
        if (err) {
          return reject(err);
        }
        resolve(docs);
      });
    });
  }

  public async getById(id: string): Promise<ToDo | null> {
    return new Promise<ToDo | null>((resolve, reject) => {
      this.db.findOne({ _id: id }, (err, doc: ToDo) => {
        if (err) {
          return reject(err);
        }
        resolve(doc);
      });
    });
  }

  public async create(todo: ToDo): Promise<string> {
    return new Promise<string>((resolve, reject) => {
      this.db.insert(todo, (err, doc: ToDo) => {
        if (err) {
          return reject(err);
        }
        resolve(doc._id);
      });
    });
  }

  public async update(todo: ToDo): Promise<number> {
    return new Promise<number>((resolve, reject) => {
      this.db.update({ _id: todo._id }, todo, {}, (err, numUpdated: number) => {
        if (err) {
          return reject(err);
        }
        resolve(numUpdated);
      });
    });
  }

  public async delete(id: string): Promise<number> {
    return new Promise<number>((resolve, reject) => {
      this.db.remove({ _id: id }, {}, (err, numRemoved: number) => {
        if (err) {
          return reject(err);
        }
        resolve(numRemoved);
      });
    });
  }
}
```

该服务有五个方法：`getAll`、`getById`、`create`、`update` 和 `delete`。这些方法映射到待办事项上的 CRUD 操作。

`getAll` 和 `getById` 方法返回一个 `Promise`，分别解析为一组待办事项或单个待办事项。

`create`、`update` 和 `delete` 方法返回一个 `Promise`，它解析为创建的待办事项的 `_id`、更新的待办事项的数量或待办事项的数量项分别删除。

## 创建待办事项控制器

接下来，我们将创建一个 To-Do 控制器。该控制器将负责处理 HTTP 请求。使用以下代码在 `src` 目录中创建一个名为 `todoController.ts` 的新文件：

```typescript
import { Request, Response } from 'express';
import { ToDoService } from './todoService';
import { ToDo } from './todo';

export class ToDoController {
  private todoService: ToDoService;

  constructor(todoService: ToDoService) {
    this.todoService = todoService;
  }

  public async getAll(req: Request, res: Response) {
    try {
      const todos = await this.todoService.getAll();
      res.json(todos);
    } catch (err) {
      res.status(500).send(err);
    }
  }

  public async getById(req: Request, res: Response) {
    const id = req.params.id;
    try {
      const todo = await this.todoService.getById(id);
      if (todo) {
        res.json(todo);
      } else {
        res.sendStatus(404);
      }
    } catch (err) {
      res.status(500).send(err);
    }
  }

  public async create(req: Request, res: Response) {
    const todo = req.body as ToDo;
    try {
      const id = await this.todoService.create(todo);
      res.json({ id: id });
    } catch (err) {
      res.status(500).send(err);
    }
  }

  public async update(req: Request, res: Response) {
    const todo = req.body as ToDo;
    if (!todo._id) {
      return res.status(400).send('To-Do item must have an _id');
    }
    try {
      const numUpdated = await this.todoService.update(todo);
      res.json({ numUpdated: numUpdated });
    } catch (err) {
      res.status(500).send(err);
    }
  }

  public async delete(req: Request, res: Response) {
    const id = req.params.id;
    try {
      const numDeleted = await this.todoService.delete(id);
      res.json({ numDeleted: numDeleted });
    } catch (err) {
      res.status(500).send(err);
    }
  }
}
```

这个控制器有五个方法：`getAll`、`getById`、`create`、`update` 和 `delete`。这些方法分别映射到 HTTP 方法`GET`、`GET`/`:id`、`POST`、`PUT` 和`DELETE`。

`getAll` 和 `getById` 方法分别返回一组待办事项或单个待办事项。

`create`、`update` 和 `delete` 方法分别返回创建的待办事项的 _id、更新的待办事项数或删除的待办事项数。

## 创建一个 Express 服务器

接下来，我们将创建一个 [Express](https://expressjs.com/) 服务器。 Express 是 Node.js 的 Web 应用程序框架。

使用以下代码在 `src` 目录中创建一个名为 `server.ts` 的新文件：

```typescript
import * as express from 'express';
import * as bodyParser from 'body-parser';
import { ToDoController } from './todoController';
import { Datastore } from 'nedb';

const app = express();
const PORT = 3000;

const db = new Datastore('todo.db');
db.loadDatabase();

const todoService = new ToDoService(db);
const todoController = new ToDoController(todoService);

app.use(bodyParser.json());

app.get('/todos', todoController.getAll);
app.get('/todos/:id', todoController.getById);
app.post('/todos', todoController.create);
app.put('/todos', todoController.update);
app.delete('/todos/:id', todoController.delete);

app.listen(PORT, () => {
  console.log(`Server listening on port ${PORT}`);
});
```

该服务器创建一个名为“todo.db”的 NeDB 数据库并加载它。然后它创建一个 To-Do 服务和一个 To-Do 控制器。

服务器将 Express 配置为使用 [body-parser](https://www.npmjs.com/package/body-parser) 中间件来解析 JSON 主体。

服务器为 To-Do 控制器的方法定义路由。 `app.get` 路由映射到 `GET` 方法。 `app.get`/`:id` 路由映射到带有路径参数的 `GET` 方法。 `app.post` 路由映射到 `POST` 方法。 `app.put` 路由映射到 `PUT` 方法。 `app.delete` 路由映射到 `DELETE` 方法。

最后，服务器开始监听端口 3000。

## 测试待办 API

我们可以使用 [cURL](https://curl.haxx.se/) 测试我们的 To-Do API。

首先，我们将启动服务器：

```
$ npm start

> todo-app@1.0.0 start /Users/username/projects/todo-app
> ts-node src/server.ts

Server listening on port 3000
```

接下来，我们将使用 cURL 创建一个待办事项：

```
$ curl -X POST -H "Content-Type: application/json" -d '{"title": "Buy milk"}' http://localhost:3000/todos
```

此 cURL 命令向带有 JSON 主体的“/todos”端点发送“POST”请求。 JSON 正文包含标题为“购买牛奶”的待办事项。

我们应该得到这样的回应：

```json
{"id": "5e1d280b04a7a22a68e0e7cd"}
```

这是我们创建的待办事项的“_id”。我们可以使用这个 _id 来检索待办事项：

```
$ curl http://localhost:3000/todos/5e1d280b04a7a22a68e0e7cd
```

我们应该得到这样的回应：

```json
{"_id":"5e1d280b04a7a22a68e0e7cd","title":"Buy milk","completed":false,"date":"2020-01-08T05:34:51.596Z"}
```

这是我们创建的待办事项。我们可以看到 `completed` 字段为 `false` 而 `date` 字段是我们创建项目的日期。

接下来，我们将更新待办事项：

```
$ curl -X PUT -H "Content-Type: application/json" -d '{"_id": "5e1d280b04a7a22a68e0e7cd", "title": "Buy eggs", "completed": true}' http://localhost:3000/todos
```

此 cURL 命令向带有 JSON 主体的“/todos”端点发送“PUT”请求。 JSON 正文包含更新后的待办事项。我们已将标题更改为“Buy eggs”并将“completed”字段设置为“true”。

我们应该得到这样的回应：

```json
{"numUpdated": 1}
```

这是已更新的待办事项的数量。我们可以检索更新的待办事项以验证它是否已更新：

```
$ curl http://localhost:3000/todos/5e1d280b04a7a22a68e0e7cd
```

我们应该得到这样的回应：

```json
{"_id":"5e1d280b04a7a22a68e0e7cd","title":"Buy eggs","completed":true,"date":"2020-01-08T05:34:51.596Z"}
```

最后，我们将删除待办事项：

```
$ curl -X DELETE http://localhost:3000/todos/5e1d280b04a7a22a68e0e7cd
```

此 cURL 命令向 `/todos/:id` 端点发送 `DELETE` 请求。我们将要删除的待办事项的“_id”作为路径参数传递。

我们应该得到这样的回应：

```json
{"numDeleted": 1}
```

这是已删除的待办事项的数量。我们可以通过检索来验证该项目是否已删除：

```
$ curl http://localhost:3000/todos/5e1d280b04a7a22a68e0e7cd
```

我们应该得到一个“404 Not Found”错误，因为待办事项不再存在。

## 结论

在本文中，我们向您展示了如何将 TypeScript 与 NeDB 结合使用。我们创建了一个简单的 To-Do API，将数据存储在 NeDB 数据库中。我们还向您展示了如何使用 cURL 测试 API。