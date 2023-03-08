---
title: 002: 为 Nest.js 设置开发环境
description: 
published: true
date: 2023-02-14T14:32:30.774Z
tags: 
editor: markdown
dateCreated: 2023-02-14T14:32:28.916Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [002: Setting up a development environment for Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/002-setting-up-a-development-environment-for-nest-js)
{.links-list}


# 为 Nest.js 设置开发环境

Nest.js 是一个用于构建高效、可扩展的 Node.js 服务器端应用程序的框架。它使用现代 JavaScript，使用 TypeScript (https://www.typescriptlang.org/) 构建，并结合了面向对象编程、函数式编程和响应式编程的元素。

## 先决条件

在开始之前，请确保您的开发机器上安装了以下内容：

* Node.js (https://nodejs.org/en/)
*打字稿（https://www.typescriptlang.org/）
* 像 Visual Studio Code (https://code.visualstudio.com/) 这样的代码编辑器

## 创建一个新的 Nest.js 项目

打开终端并通过运行以下命令创建一个新的 Nest.js 项目：

```
nest new <project name>
```

这将使用项目名称创建一个新目录，并使用基本的 Nest.js 结构初始化项目。

## 启动 Nest.js 服务器

导航到新创建的项目目录并运行以下命令以启动 Nest.js 服务器：

```
npm run start
```

默认情况下，这将在 http://localhost:3000 上启动 Nest.js 服务器。您可以通过设置 `PORT` 环境变量来更改端口号。

## 创建一个新的 Nest.js 控制器

现在 Nest.js 服务器已启动并运行，让我们创建一个新的控制器。在项目根目录中，创建一个名为“controllers”的新目录和一个名为“<controller name>.controller.ts”的新文件。

控制器文件应如下所示：

```typescript
import { Controller } from '@nestjs/common';

@Controller('<controller path>')
export class <Controller Name>Controller {}
```

将 `<controller path>` 替换为您希望控制器可访问的路径，并将 `<Controller Name>` 替换为控制器的名称。

## 创建一个新的 Nest.js 路由

在控制器文件中，通过添加以下内容创建一个新路由：

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('<controller path>')
export class <Controller Name>Controller {

  @Get()
  getHello(): string {
    return 'Hello World!';
  }

}
```

`@Get()` 装饰器将 `getHello()` 方法定义为 GET 路由。您还可以分别使用“@Post()”、“@Put()”和“@Delete()”装饰器定义 POST、PUT 和 DELETE 路由。

## 测试 Nest.js 路由

在 Web 浏览器中打开 http://localhost:3000/<controller path>，您应该会看到“Hello World!”消息。

## 结论

在本教程中，您学习了如何为 Nest.js 设置开发环境并创建一个带有路由的新 Nest.js 控制器。