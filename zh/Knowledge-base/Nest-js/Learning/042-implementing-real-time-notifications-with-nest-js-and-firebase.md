---
title: 042：使用 Nest.js 和 Firebase 实现实时通知
description: 
published: true
date: 2023-02-12T03:17:53.930Z
tags: 
editor: markdown
dateCreated: 2023-02-12T03:17:52.264Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [042: Implementing real-time notifications with Nest.js and Firebase***English** document is available*](/en/Knowledge-base/Nest-js/Learning/042-implementing-real-time-notifications-with-nest-js-and-firebase)
{.links-list}


# 使用 Nest.js 和 Firebase 实现实时通知

在本文中，我们将研究如何使用 Firebase Cloud Messaging (FCM) 服务在 Nest.js 应用程序中设置实时通知。

Nest.js 是一个用于构建可扩展的服务器端应用程序的 Node.js 框架。它使用现代 JavaScript，使用 TypeScript（编译为 JavaScript）构建，并结合了面向对象编程、函数式编程和响应式编程的元素。

Firebase 是由 Google 开发的移动和 Web 应用程序开发平台。它提供了许多服务，其中之一就是 FCM。 FCM 是一种跨平台消息传递解决方案，可让您免费可靠地传递消息。

## 设置一个 Nest.js 项目

我们将从设置一个新的 Nest.js 项目开始。为此，我们将使用 Nest CLI。如果您没有安装它，您可以通过运行以下命令来安装它：

```
$ npm install -g @nestjs/cli
```

安装 Nest CLI 后，我们可以通过运行以下命令来创建一个新项目：

```
$ nest new project-name
```

这将创建一个包含项目文件的新目录。

## 安装依赖

我们需要为我们的项目安装以下依赖项：

- @nestjs/常见
- @nestjs/平台快递
- 火力管理

我们可以通过运行以下命令来安装这些依赖项：

```
$ npm install --save @nestjs/common @nestjs/platform-express firebase-admin
```

## 配置火力地堡

我们需要创建一个新的 Firebase 项目才能使用 FCM。我们可以通过转到 [Firebase 控制台](https://console.firebase.google.com/) 并单击“创建项目”按钮来完成此操作。

为您的项目命名，然后单击“创建项目”按钮。

创建项目后，单击“将 Firebase 添加到您的 Web 应用程序”按钮。

这将打开一个弹出窗口，其中包含您的 Firebase 配置。我们需要复制配置对象并将其添加到项目中的 environment.ts 文件中。该文件应如下所示：

```javascript
export const environment = {
  production: false,
  firebase: {
    apiKey: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    authDomain: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    databaseURL: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    projectId: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    storageBucket: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    messagingSenderId: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
  }
};
```

我们还需要将以下行添加到 environment.prod.ts 文件中：

```javascript
export const environment = {
  production: true,
  firebase: {
    apiKey: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    authDomain: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    databaseURL: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    projectId: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    storageBucket: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    messagingSenderId: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
  }
};
```

## 创建 FCM 服务

我们需要创建一个新服务来处理 FCM 消息的发送。我们可以通过运行以下命令来完成此操作：

```
$ nest generate service fcm
```

这将在 `src/fcm` 目录中创建一个新的服务文件。我们需要导入 `firebase-admin` 模块和 `environment` 文件。我们还需要创建 `admin.messaging.Messaging` 类的新实例。该服务应如下所示：

```javascript
import { Injectable } from '@nestjs/common';
import * as admin from 'firebase-admin';
import { environment } from '../../environments/environment';

@Injectable()
export class FcmService {
  private readonly messaging = admin.messaging();

  constructor() {
    admin.initializeApp({
      credential: admin.credential.applicationDefault(),
      databaseURL: environment.firebase.databaseURL,
      projectId: environment.firebase.projectId
    });
  }

  // ...
}
```

## 发送 FCM 消息

我们需要向将发送 FCM 消息的“FcmService”添加一个新方法。该方法应采用指定消息收件人的“to”参数和包含要发送的数据的“data”参数。

该方法应返回一个在消息发送后解析的“Promise”。

```javascript
  async send(to: string, data: any): Promise<void> {
    const message = {
      to,
      data
    };

    await this.messaging.send(message);
  }
```

## 创建控制器

我们需要创建一个新的控制器，它将调用 `FcmService` 的 `send` 方法。我们可以通过运行以下命令来完成此操作：

```
$ nest generate controller fcm
```

这将在 src/fcm 目录中创建一个新的控制器文件。我们需要导入 `FcmService` 和 `@nestjs/common` 模块。我们还需要将 `FcmService` 注入到控制器中。控制器应如下所示：

```javascript
import { Controller, Post, Body } from '@nestjs/common';
import { FcmService } from './fcm.service';

@Controller('fcm')
export class FcmController {
  constructor(private readonly fcmService: FcmService) {}

  @Post()
  async send(@Body('to') to: string, @Body('data') data: any): Promise<void> {
    await this.fcmService.send(to, data);
  }
}
```

## 测试控制器

我们可以通过使用 `to` 和 `data` 参数向 `/fcm` 端点发送 POST 请求来测试控制器。我们可以使用 [Postman](https://www.getpostman.com/) 工具来完成此操作。

如果消息发送成功，我们应该会在 Postman 控制台中看到一条成功消息。

## 结论

在本文中，我们了解了如何使用 Firebase 云消息传递 (FCM) 服务在 Nest.js 应用程序中设置实时通知。