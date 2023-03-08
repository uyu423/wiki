---
title: 040：将 Nest.js 与 Google Cloud Functions 结合使用
description: 
published: true
date: 2023-02-15T12:32:37.736Z
tags: 
editor: markdown
dateCreated: 2023-02-15T12:32:36.061Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [040: Using Nest.js with Google Cloud Functions***English** document is available*](/en/Knowledge-base/Nest-js/Learning/040-using-nest-js-with-google-cloud-functions)
{.links-list}


# 将 Nest.js 与 Google Cloud Functions 结合使用

Google Cloud Functions 是一个无服务器平台，可让您运行代码而无需担心配置或管理服务器。您可以使用多种语言编写代码，包括 JavaScript、Python 和 Go。

Nest.js 是一个用于构建高效、可扩展的 Node.js 服务器端应用程序的框架。它使用现代 JavaScript，使用 TypeScript（为 JavaScript 带来静态类型检查）构建，并结合了面向对象和函数式编程的元素。

在这篇文章中，我们将向您展示如何将 Nest.js 与 Google Cloud Functions 结合使用。我们将创建一个从 MongoDB 数据库返回用户列表的简单函数。

## 1.创建一个新项目

首先，我们需要创建一个新项目。我们将使用 Nest.js CLI 生成一个新项目。

```
$ nest new project-name
```

## 2.安装依赖

接下来，我们需要为我们的项目安装依赖项。我们需要 MongoDB Node.js 驱动程序和 Nest.js MongoDB 包。

```
$ npm install mongodb @nestjs/mongoose
```

## 3. 创建一个 Nest.js 模块

接下来，我们需要创建一个 Nest.js 模块。这是一个标准的 JavaScript 模块，将包含我们与 MongoDB 交互的代码。

```javascript
import { Module } from '@nestjs/common';
import { MongooseModule } from '@nestjs/mongoose';

@Module({
  imports: [
    MongooseModule.forFeature([
      { name: 'User', schema: UserSchema }
    ])
  ],
  providers: [UserService],
  exports: [UserService]
})
export class UserModule {}
```

## 4. 创建一个 Nest.js 服务

接下来，我们需要创建一个 Nest.js 服务。这是一个标准的 JavaScript 类，它将包含我们与 MongoDB 交互的代码。

```javascript
import { Injectable } from '@nestjs/common';
import { InjectModel } from '@nestjs/mongoose';
import { Model } from 'mongoose';

@Injectable()
export class UserService {
  constructor(
    @InjectModel('User') private readonly userModel: Model<User>
  ) {}

  async findAll(): Promise<User[]> {
    return await this.userModel.find().exec();
  }
}
```

## 5. 创建谷歌云函数

接下来，我们需要创建一个 Google Cloud Function。这是一个标准的 JavaScript 函数，当有人向我们的 API 端点发出请求时将被触发。

```javascript
import * as functions from 'firebase-functions';
import { NestFactory } from '@nestjs/core';
import { UserModule } from './user.module';

export const userApi = functions.https.onRequest(async (req, res) => {
  const app = await NestFactory.create(UserModule);
  await app.init();
  res.send(await app.get(UserService).findAll());
});
```

## 6. 部署你的函数

最后，我们需要部署我们的功能。我们可以使用 Firebase CLI 执行此操作。

```
$ firebase deploy --only functions
```

## 7. 测试你的 API 端点

您可以通过向端点 URL 发出 GET 请求来测试 API 端点。您应该会看到带有用户列表的 JSON 响应。

```
$ curl https://us-central1-project-name.cloudfunctions.net/userApi
```

## 恭喜！

您已成功创建使用 Google Cloud Functions 的 Nest.js API 端点。