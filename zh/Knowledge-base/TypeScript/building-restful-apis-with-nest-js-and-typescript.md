---
title: 使用 Nest.js 和 TypeScript 构建 RESTful API
description: 
published: true
date: 2023-02-15T14:55:40.863Z
tags: 
editor: markdown
dateCreated: 2023-02-15T14:55:39.208Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Building RESTful APIs with Nest.js and TypeScript***English** document is available*](/en/Knowledge-base/TypeScript/building-restful-apis-with-nest-js-and-typescript)
{.links-list}


# 使用 Nest.js 和 TypeScript 构建 RESTful API

Nest.js 是一个用于构建服务器端应用程序的 Node.js 框架。它使用 TypeScript，它是 JavaScript 的超集，添加了静态类型检查和其他功能，并为构建 RESTful API 提供了一个良好的平台。

在本文中，我们将了解如何使用 Nest.js 和 TypeScript 构建 RESTful API。我们将从查看项目结构开始，然后继续创建 API 端点。我们还将了解如何将 TypeScript 与 Nest.js 结合使用。

## 项目结构

Nest.js 项目的项目结构类似于 Node.js 项目。源代码有一个 src 目录，测试有一个 test 目录。 src 目录包含一个 main.ts 文件，它是应用程序的入口点。 tests 目录包含一个 main.spec.ts 文件，它是测试的入口点。

该项目还有一个 tsconfig.json 文件，用于配置 TypeScript 编译器。该文件包含编译器的选项，例如目标 JavaScript 版本和模块类型。

该项目还有一个 package.json 文件，其中包含项目的元数据，例如依赖项和脚本。

## 创建 API 端点

我们需要做的第一件事是创建 API 端点。我们将在 src/main.ts 文件中执行此操作。

我们将从导入 express 模块并创建一个 Express 应用程序开始。我们还将导入 body-parser 模块和 cors 模块。

```javascript
import * as express from 'express';
import * as bodyParser from 'body-parser';
import * as cors from 'cors';

const app = express();
```

接下来，我们将配置 Express 应用程序。我们将端口设置为 3000 并启用正文解析器和 cors 中间件。

```javascript
app.set('port', 3000);
app.use(bodyParser.json());
app.use(cors());
```

现在，我们将创建 API 端点。我们将从用于检索用户列表的 GET 端点开始。

```javascript
app.get('/users', (req, res) => {
  // ...
});
```

接下来，我们将创建一个用于创建新用户的 POST 端点。

```javascript
app.post('/users', (req, res) => {
  // ...
});
```

最后，我们将创建一个用于更新现有用户的 PUT 端点。

```javascript
app.put('/users/:id', (req, res) => {
  // ...
});
```

## 在 Nest.js 中使用 TypeScript

Nest.js 和 TypeScript 可以很好地协同工作。 Nest.js 提供了装饰器，可以轻松地将 TypeScript 与 Nest.js 一起使用。

例如，@Controller 装饰器可用于创建控制器。 @Get 装饰器可用于创建 GET 端点。 @Post 装饰器可用于创建 POST 端点。

```typescript
import { Controller, Get, Post, Put } from '@nestjs/common';

@Controller('/users')
export class UserController {

  @Get()
  getUsers() {
    // ...
  }

  @Post()
  createUser() {
    // ...
  }

  @Put(':id')
  updateUser() {
    // ...
  }

}
```