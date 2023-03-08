---
title: 014: Using middlewares in Nest.js
description: 
published: true
date: 2023-02-15T00:32:27.168Z
tags: 
editor: markdown
dateCreated: 2023-02-15T00:32:25.395Z
---

- [014: Uso de middleware en Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/014-using-middlewares-in-nest-js)
{.links-list}
- [014: 在 Nest.js 中使用中间件***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/014-using-middlewares-in-nest-js)
{.links-list}
- [014: Nest.js에서 미들웨어 사용하기***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/014-using-middlewares-in-nest-js)
{.links-list}


# Using middlewares in Nest.js

Nest.js is a web framework for Node.js that helps you create scalable server-side applications. In this post, we'll take a look at how to use middlewares in Nest.js.

Middlewares are functions that are invoked by Nest.js when an incoming request is received. They can be used to perform tasks such as logging, validation, and authentication.

Nest.js comes with a built-in middleware factory that makes it easy to create your own middlewares. To create a middleware, you need to create a class that implements the `NestMiddleware` interface. This interface defines a `use()` method that takes the `req` and `res` objects as parameters.

Here's a simple example of a middleware that logs the incoming request:

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

To use this middleware, you need to register it with Nest.js. This can be done in the `app.module.ts` file:

```typescript
import { Module } from '@nestjs/common';
import { LoggerMiddleware } from './logger.middleware';

@Module({
  providers: [LoggerMiddleware],
})
export class AppModule {}
```

Once the middleware is registered, Nest.js will invoke it whenever an incoming request is received.

Middlewares can also be used to perform tasks such as validation and authentication. For example, you can create a middleware that checks if the incoming request is authenticated:

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

This middleware will check if the incoming request is authenticated. If it is not, it will return a `401 Unauthorized` status code. Otherwise, it will invoke the next middleware in the chain.

Middlewares can be chained together to create a chain of operations that is executed for each incoming request. For example, you can create a chain that logs the request, validates the request, and then authenticates the request:

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

In this example, the `LoggerMiddleware` will be invoked first, followed by the `AuthMiddleware`.

Middlewares can be used to perform a wide variety of tasks. They are a powerful tool that can be used to extend the functionality of Nest.js.