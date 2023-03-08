---
title: 033：将 Nest.js 与 JavaScript 结合使用
description: 
published: true
date: 2023-02-15T11:32:41.979Z
tags: 
editor: markdown
dateCreated: 2023-02-15T11:32:40.167Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [033: Using Nest.js with JavaScript***English** document is available*](/en/Knowledge-base/Nest-js/Learning/033-using-nest-js-with-javascript)
{.links-list}


# 在 JavaScript 中使用 Nest.js

Nest.js 是一个用于构建高效、可扩展的 Node.js 服务器端应用程序的框架。它使用现代 JavaScript，使用 TypeScript（可选）构建，并结合了面向对象编程、函数式编程和响应式编程的元素。

Nest.js 对于具有 JavaScript 背景的开发人员来说是一个很棒的框架。它易于使用并且具有熟悉的语法。在这篇文章中，我们将看看如何将 Nest.js 与 JavaScript 一起使用。

## 安装

要安装 Nest.js，您需要在计算机上安装 Node.js 和 npm。然后，您可以使用以下命令安装 Nest.js：

```
npm install -g @nestjs/cli
```

## 创建一个 Nest.js 项目

安装 Nest.js 后，您可以使用 Nest.js CLI 创建一个新项目。为此，请运行以下命令：

```
nest new project-name
```

这将使用您指定的名称创建一个新的 Nest.js 项目。

## 项目名称/src/app.controller.js

我们要看的第一个文件是 app.controller.js 文件。这是我们将定义控制器的文件。控制器是包含一个或多个方法的类。每个方法负责处理一个请求。

让我们看一个简单的控制器：

```javascript
import { Controller, Get, Post, Body } from '@nestjs/common';

@Controller('/api/v1/todos')
export class TodosController {
  @Get()
  findAll() {
    return [];
  }

  @Post()
  create(@Body() createTodoDto) {
    return [];
  }
}
```

在上面的代码中，我们用两个方法定义了一个控制器：findAll 和 create。 findAll 方法负责处理 GET 请求。 create 方法负责处理 POST 请求。

## 项目名称/src/app.service.js

我们要看的下一个文件是 app.service.js 文件。这是我们将定义服务的文件。服务是包含业务逻辑的类。

我们来看一个简单的服务：

```javascript
import { Injectable } from '@nestjs/common';

@Injectable()
export class TodosService {
  getAll() {
    return [];
  }

  create(createTodoDto) {
    return [];
  }
}
```

在上面的代码中，我们用两个方法定义了一个服务：getAll 和 create。 getAll 方法返回所有待办事项。 create 方法创建一个新的待办事项。

## 项目名称/src/app.module.js

我们要看的下一个文件是 app.module.js 文件。这是我们将定义模块的文件。模块是包含控制器和服务的类。

让我们看一个简单的模块：

```javascript
import { Module } from '@nestjs/common';
import { TodosController } from './app.controller';
import { TodosService } from './app.service';

@Module({
  controllers: [TodosController],
  providers: [TodosService],
})
export class TodosModule {}
```

在上面的代码中，我们定义了一个带有控制器和服务的模块。控制器负责处理请求。该服务负责业务逻辑。

## 项目名称/src/main.js

我们要看的下一个文件是 main.js 文件。这是我们将启动 Nest.js 应用程序的文件。

让我们看一下代码：

```javascript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

在上面的代码中，我们导入了 NestFactory 和 AppModule。然后我们创建了一个新的 Nest.js 应用程序并在端口 3000 上启动它。

## 结论

在这篇文章中，我们了解了如何将 Nest.js 与 JavaScript 结合使用。我们已经看到了如何安装 Nest.js 和创建一个新项目。我们还看到了如何定义控制器、服务和模块。