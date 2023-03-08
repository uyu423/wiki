---
title: 003：创建你的第一个 Nest.js 应用程序
description: 
published: true
date: 2023-02-14T15:34:15.016Z
tags: 
editor: markdown
dateCreated: 2023-02-14T15:34:13.184Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [003: Creating your first Nest.js application***English** document is available*](/en/Knowledge-base/Nest-js/Learning/003-creating-your-first-nest-js-application)
{.links-list}


# 创建你的第一个 Nest.js 应用

本指南将引导您完成创建第一个 Nest.js 应用程序的步骤。 Nest.js 是用于构建 Node.js 应用程序的框架。它基于 Express.js 并使用 TypeScript，它是 JavaScript 的超集。

## 先决条件

在开始之前，您需要在您的机器上安装以下软件：

- 节点.js
- npm
- 打字稿

## 入门

首先，为您的项目创建一个新目录。然后，通过运行以下命令来初始化您的项目：

```
npm init
```

这将在您的项目目录中创建一个 `package.json` 文件。接下来，您需要安装 Nest.js 框架。您可以通过运行以下命令来执行此操作：

```
npm install --save @nestjs/core
```

## 你好世界

现在您已经安装了 Nest.js，您可以创建您的第一个 Nest.js 应用程序。在您的项目目录中创建一个名为“app.ts”的新文件，并向其中添加以下代码：

```typescript
import { NestFactory } from '@nestjs/core';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

此代码从“@nestjs/core”包中导入“NestFactory”类，并使用它创建“AppModule”类的实例。 `AppModule` 类是一个 Nest.js 模块。 Nest.js 模块用于组织您的代码。

接下来，代码调用 app 对象的 listen() 方法。这会告诉 Nest.js 应用程序开始侦听端口 3000 上传入的 HTTP 请求。

## 结论

在本指南中，您已经创建了您的第一个 Nest.js 应用程序。您还了解了 Nest.js 中的一些关键概念，例如模块和 NestFactory 类。