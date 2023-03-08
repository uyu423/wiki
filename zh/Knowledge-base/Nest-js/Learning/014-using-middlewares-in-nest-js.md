---
title: 014: 在 Nest.js 中使用中间件
description: 
published: true
date: 2023-02-15T00:32:32.946Z
tags: 
editor: markdown
dateCreated: 2023-02-15T00:32:25.390Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [014: Using middlewares in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/014-using-middlewares-in-nest-js)
{.links-list}


# 在 Nest.js 中使用中间件

Nest.js 是 Node.js 的 Web 框架，可帮助您创建可扩展的服务器端应用程序。在这篇文章中，我们将看看如何在 Nest.js 中使用中间件。

中间件是 Nest.js 在收到传入请求时调用的函数。它们可用于执行日志记录、验证和身份验证等任务。

Nest.js 带有一个内置的中间件工厂，可以很容易地创建你自己的中间件。要创建中间件，您需要创建一个实现“NestMiddleware”接口的类。该接口定义了一个将 `req` 和 `res` 对象作为参数的 `use()` 方法。

这是一个记录传入请求的中间件的简单示例：

```typescript
import { Injectable, NestMiddleware } from '@nestjs/common';

@Injectable()
export class LoggerMiddleware implements NestMiddleware {
  use(req: any, res: any, next: () => void) {
    console.log(`Incoming request at ${req.url}`);
    next();
  }
}
```

要使用这个中间件，你需要向 Nest.js 注册它。这可以在 `app.module.ts` 文件中完成：

```typescript
import { Module } from '@nestjs/common';
import { LoggerMiddleware } from './logger.middleware';

@Module({
  providers: [LoggerMiddleware],
})
export class AppModule {}
```

注册中间件后，Nest.js 将在收到传入请求时调用它。

中间件还可用于执行验证和身份验证等任务。例如，您可以创建一个中间件来检查传入请求是否经过身份验证：

```typescript
import { Injectable, NestMiddleware } from '@nestjs/common';

@Injectable()
export class AuthMiddleware implements NestMiddleware {
  use(req: any, res: any, next: () => void) {
    if (!req.isAuthenticated()) {
      res.status(401).send('You are not authenticated');
    } else {
      next();
    }
  }
}
```

该中间件将检查传入请求是否已通过身份验证。如果不是，它将返回“401 Unauthorized”状态代码。否则，它将调用链中的下一个中间件。

中间件可以链接在一起以创建针对每个传入请求执行的操作链。例如，您可以创建一个链来记录请求、验证请求，然后对请求进行身份验证：

```typescript
import { Injectable, NestMiddleware } from '@nestjs/common';
import { LoggerMiddleware } from './logger.middleware';
import { AuthMiddleware } from './auth.middleware';

@Module({
  providers: [
    LoggerMiddleware,
    AuthMiddleware,
  ],
})
export class AppModule {}
```

在此示例中，将首先调用 `LoggerMiddleware`，然后调用 `AuthMiddleware`。

中间件可用于执行各种各样的任务。它们是一个强大的工具，可用于扩展 Nest.js 的功能。