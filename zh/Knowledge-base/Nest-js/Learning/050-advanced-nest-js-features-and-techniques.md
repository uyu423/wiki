---
title: 050：高级 Nest.js 特性和技术
description: 
published: true
date: 2023-02-15T18:33:02.464Z
tags: 
editor: markdown
dateCreated: 2023-02-15T18:33:00.847Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [050: Advanced Nest.js features and techniques***English** document is available*](/en/Knowledge-base/Nest-js/Learning/050-advanced-nest-js-features-and-techniques)
{.links-list}


050：高级 Nest.js 特性和技术

Nest.js 是一个强大的 Node.js Web 框架。它建立在 Express.js 之上并使用 TypeScript，这使得开发和部署企业级应用程序变得容易。

在本文中，我们将了解 Nest.js 提供的一些高级功能和技术。

我们将涵盖以下主题：

- 路由
- 身份验证和授权
- 数据库访问
- 测试

## 路由

在 Nest.js 中，路由是使用 @Controller() 装饰器定义的。例如：

```typescript
@Controller('/users')
export class UserController {

  @Get('/')
  index() {
    // ...
  }

  @Get('/:id')
  show() {
    // ...
  }

  @Post('/')
  store() {
    // ...
  }

  @Put('/:id')
  update() {
    // ...
  }

  @Delete('/:id')
  destroy() {
    // ...
  }

}
```

如您所见，@Controller() 装饰器为控制器中定义的所有路由定义了基本路径。 @Get()、@Post()、@Put() 和@Delete() 装饰器用于为每个路由定义 HTTP 方法。

## 认证与授权

Nest.js 为身份验证和授权提供开箱即用的支持。

为了对用户进行身份验证，Nest.js 提供了 @Authenticate() 装饰器。此装饰器可用于控制器或方法级别。

例如，要验证 UserController 中定义的所有路由，我们可以在控制器上使用 @Authenticate() 装饰器：

```typescript
@Controller('/users')
@Authenticate()
export class UserController {
  // ...
}
```

要仅验证某些路由，我们可以在方法上使用 @Authenticate() 装饰器：

```typescript
@Controller('/users')
export class UserController {

  @Get('/')
  @Authenticate()
  index() {
    // ...
  }

  @Get('/:id')
  show() {
    // ...
  }

  @Post('/')
  store() {
    // ...
  }

  @Put('/:id')
  update() {
    // ...
  }

  @Delete('/:id')
  destroy() {
    // ...
  }

}
```

Nest.js 还提供了用于授权的@Authorize() 装饰器。此装饰器可用于控制器或方法级别。

例如，要授权 UserController 中定义的所有路由，我们可以在控制器上使用 @Authorize() 装饰器：

```typescript
@Controller('/users')
@Authorize()
export class UserController {
  // ...
}
```

要仅授权某些路由，我们可以在方法上使用 @Authorize() 装饰器：

```typescript
@Controller('/users')
export class UserController {

  @Get('/')
  @Authorize()
  index() {
    // ...
  }

  @Get('/:id')
  show() {
    // ...
  }

  @Post('/')
  store() {
    // ...
  }

  @Put('/:id')
  update() {
    // ...
  }

  @Delete('/:id')
  destroy() {
    // ...
  }

}
```

## 数据库访问

Nest.js 提供了几种访问数据库的方法。

最常见的方法是使用 @Inject() 装饰器将数据库客户端注入到您的控制器或服务中。

例如，要将 MongoDB 客户端注入到您的控制器中，您可以使用以下代码：

```typescript
@Controller('/users')
export class UserController {

  constructor(
    @Inject('MONGODB_CLIENT') private mongodb: MongoClient,
  ) {}

  // ...

}
```

访问数据库的另一种方法是使用 @UseDatabases() 装饰器。此装饰器可用于控制器或服务级别。

例如，要在您的控制器中使用 MongoDB 和 PostgreSQL，您可以使用以下代码：

```typescript
@Controller('/users')
@UseDatabases(['MONGODB', 'POSTGRESQL'])
export class UserController {

  // ...

}
```

## 测试

Nest.js 提供了几种测试应用程序的方法。

最常见的方法是使用 @Test() 装饰器。此装饰器可用于控制器或服务级别。

例如，要测试 UserController，可以使用以下代码：

```typescript
@Test()
export class UserController {

  @Get('/')
  index() {
    // ...
  }

  @Get('/:id')
  show() {
    // ...
  }

  @Post('/')
  store() {
    // ...
  }

  @Put('/:id')
  update() {
    // ...
  }

  @Delete('/:id')
  destroy() {
    // ...
  }

}
```

测试应用程序的另一种方法是使用 @TestModule() 装饰器。这个装饰器可以在模块级别使用。

例如，要测试 UserModule，您可以使用以下代码：

```typescript
@TestModule()
export class UserModule {}
```

## 结论

在这篇文章中，我们介绍了 Nest.js 提供的一些高级功能和技术。

我们已经了解了如何定义路由、如何对用户进行身份验证和授权、如何访问数据库以及如何测试 Nest.js 应用程序。

如果您想了解有关 Nest.js 的更多信息，我建议您查看官方文档。