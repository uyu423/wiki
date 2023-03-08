---
title: 041：将 Nest.js 与 Firebase 函数结合使用
description: 
published: true
date: 2023-02-15T13:33:20.747Z
tags: 
editor: markdown
dateCreated: 2023-02-15T13:33:19.106Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [041: Using Nest.js with Firebase Functions***English** document is available*](/en/Knowledge-base/Nest-js/Learning/041-using-nest-js-with-firebase-functions)
{.links-list}


# 使用带有 Firebase 函数的 Nest.js

Nest.js 是一个用于构建高效、可扩展的 Node.js 服务器端应用程序的框架。它使用现代 JavaScript，使用 TypeScript（提供类型化 JavaScript）构建，并结合了面向对象编程、函数式编程和函数式响应式编程的元素。

Firebase Functions 是一个无服务器平台，可让您在云端运行 JavaScript 代码，而无需配置或管理任何服务器。功能可以由来自 Firebase 产品的事件触发，例如 Firebase 实时数据库中的数据更改、通过 Firebase 身份验证的新用户注册或通过 Firebase 云消息传递的传入消息。

在本文中，我们将学习如何将 Nest.js 与 Firebase 函数结合使用。我们将构建一个简单的 Nest.js 无服务器应用程序，该应用程序在 Firebase Functions 上运行并响应 HTTP 请求。

## 设置项目

首先，让我们创建一个新的 Nest.js 项目。我们将使用 Nest CLI 生成一个新项目。运行以下命令生成一个新项目：

```
$ nest new nest-firebase-functions
```

这将在名为 ```nest-firebase-functions``` 的文件夹中创建一个新的 Nest.js 项目。

接下来，我们需要为 Node.js 安装 Firebase Functions SDK。我们可以通过运行以下命令来完成此操作：

```
$ npm install firebase-functions@latest firebase-admin@latest --save
```

这将安装最新版本的 Firebase Functions SDK 和 Firebase Admin SDK。

## 编写代码

现在我们有了一个 Nest.js 项目并安装了 Firebase SDK，我们可以编写一些代码了。

打开 ```src/main.ts``` 文件并将内容替换为以下内容：

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

import * as functions from 'firebase-functions';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(() => console.log('Nest.js is listening'));
}

export const api = functions.https.onRequest(bootstrap);
```

让我们来看看这里发生了什么。

首先，我们从```@nestjs/core```导入```NestFactory```和```AppModule```。

接下来，我们导入整个 ```firebase-functions``` 命名空间。这使我们能够访问```functions```对象，我们将使用它来配置我们的HTTP功能。

然后，我们定义一个名为 ```bootstrap``` 的 ```async``` 函数。当我们的 HTTP 函数被调用时，这个函数将被调用。 ```await``` 关键字用于等待异步操作完成。

在 ```bootstrap``` 函数中，我们创建一个新的 ```NestFactory``` 实例并传入我们的 ```AppModule```。然后我们通过调用 ```listen``` 方法启动 Nest.js 服务器。

最后，我们导出一个调用我们的 ```bootstrap``` 函数的```functions.https.onRequest``` 函数。这将导致我们的 Nest.js 应用程序在向 ```/api``` 端点发出 HTTP 请求时被调用。

现在我们有了代码，让我们看一下 ```app.module.ts``` 文件。这是定义我们的 Nest.js 模块的文件。

打开 ```app.module.ts``` 文件并将内容替换为以下内容：

```typescript
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';

@Module({
  imports: [],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

这个文件定义了我们的```AppModule```，它是我们 Nest.js 应用程序的根模块。

我们的模块从```@nestjs/common```导入```Module```装饰器。这个装饰器用于定义一个 Nest.js 模块。

我们的模块还从 ```./app``` 文件夹中导入 ```AppController``` 和 ```AppService```。稍后我们将查看这些文件。

```typescript
import { Controller, Get } from '@nestjs/common';
import { AppService } from './app.service';

@Controller()
export class AppController {
  constructor(private readonly appService: AppService) {}

  @Get()
  getHello(): string {
    return this.appService.getHello();
  }
}
```app.module.ts``` 文件，让我们来看看```app.controller.ts``` 文件。这个文件定义了我们的```AppController```。

打开 ```app.controller.ts``` 文件并将内容替换为以下内容：

```typescript
import { Injectable } from '@nestjs/common';

@Injectable()
export class AppService {
  getHello(): string {
    return 'Hello World!';
  }
}
```

我们的控制器从```@nestjs/common```导入```Controller```和```Get```装饰器。这些装饰器分别用于定义一个控制器和一个控制器动作。

我们的控制器还从 ```./app``` 文件夹中导入 ```AppService```。稍后我们将查看此文件。

```
$ firebase init
```@Get()``` 装饰器用于定义控制器操作。 ```@Get('/')``` 语法指定了可以访问我们的控制器操作的路径。在我们的例子中，可以在根路径 (```/```) 访问控制器操作。

```
$ firebase deploy
```app.controller.ts``` 文件，让我们来看看```app.service.ts``` 文件。这个文件定义了我们的```AppService```。

打开 ```app.service.ts``` 文件并将内容替换为以下内容：

```
$ curl https://{your-firebase-project-id}.firebaseio.com/api
```

我们的服务从```@nestjs/common```导入```Injectable```装饰器。该装饰器用于定义服务。

```@Injectable()``` 装饰器用于配置我们的服务。

```getHello``` 方法是一种返回字符串的简单方法。此方法由我们的控制器操作调用。

## 部署代码

现在我们已经编写了代码，我们需要将其部署到 Firebase。

首先，我们需要创建一个 Firebase 项目。我们可以通过运行以下命令来完成此操作：

```
$ 火力基地初始化
```

这将在当前目录中创建一个新的 Firebase 项目。

接下来，我们需要将代码部署到 Firebase。我们可以通过运行以下命令来完成此操作：

```
$ 火力基地部署
```

这会将我们的代码部署到 Firebase。

## 测试代码

现在我们的代码已部署，让我们对其进行测试。

我们可以通过向 ```/api``` 端点发出 HTTP 请求来测试我们的代码。我们可以使用```curl```命令来做到这一点。运行以下命令发出 HTTP 请求：

```
$ curl https://{your-firebase-project-id}.firebaseio.com/api
```

这将向 ```/api``` 端点发出 HTTP 请求，并将响应打印到控制台。

## 结论

在本文中，我们学习了如何将 Nest.js 与 Firebase 函数结合使用。我们构建了一个简单的 Nest.js 无服务器应用程序，它在 Firebase Functions 上运行并响应 HTTP 请求。