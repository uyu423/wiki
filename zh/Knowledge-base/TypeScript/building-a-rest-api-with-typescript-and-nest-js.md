---
title: 使用 TypeScript 和 Nest.js 构建 REST API
description: 
published: true
date: 2023-02-17T18:12:56.684Z
tags: 
editor: markdown
dateCreated: 2023-01-30T19:44:00.613Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Building a REST API with TypeScript and Nest.js***English** version of this document is available*](/en/Knowledge-base/TypeScript/building-a-rest-api-with-typescript-and-nest-js)
{.links-list}


# 使用 TypeScript 和 Nest.js 构建 REST API

Nest.js 是一个 Node.js 框架，用于在 TypeScript 和 JavaScript（ES6、7、8）之上构建高效、可扩展的企业级服务器端应用程序。

## 为什么使用 Nest.js？

您可能想要使用 Nest.js 构建 REST API 的原因有很多。

Nest.js 建立在 TypeScript 之上，因此受益于 TypeScript 的所有优势，包括静态类型检查。这与动态类型的 JavaScript 形成对比。

此外，Nest.js 还利用了 JavaScript Express 框架。 Express 是一个快速、独立、极简的 Node.js Web 框架。通过使用 Express，Nest.js 可以利用大量可用的 Express 插件和中间件。

Nest.js 也是非常模块化的。 Nest.js 架构基于 CRNA（通用根名称架构）。这种架构使得 Nest.js 中的每个模块都可以相互独立使用。

## 使用 TypeScript 的好处

由于 Nest.js 是基于 TypeScript 构建的，因此它受益于 TypeScript 的所有功能。 TypeScript 是 JavaScript 的超集，可将可选的静态类型添加到您的代码中。

使用 TypeScript 而不是 JavaScript 的好处包括：

- TypeScript 是 JavaScript 的超集，这意味着任何有效的 JavaScript 代码也是有效的 TypeScript 代码。这使得 JavaScript 开发人员可以轻松开始使用 TypeScript。

- TypeScript 代码被编译为 JavaScript，这意味着它可以在任何 JavaScript 环境中运行。这使得将 TypeScript 代码部署到服务器或 Web 浏览器变得容易。

- TypeScript 是静态类型的。这意味着 TypeScript 编译器可以在执行代码之前检查代码中的错误。这有助于防止将错误引入您的代码中。

- TypeScript 编译器可以生成与旧版 JavaScript 兼容的 JavaScript 代码。这被称为“针对”特定的 JavaScript 版本。当您需要支持较旧的浏览器或服务器时，这会很有帮助。

- TypeScript 带有自己的类型定义文件。这些文件可用于向 TypeScript 提供有关代码中预期的值类型的信息。这在使用用 JavaScript 编写的第三方库时特别有用。

## 安装 TypeScript 和 Nest.js

为了使用 TypeScript 和 Nest.js，您需要安装它们。可以使用 npm 包管理器安装 TypeScript 编译器。

```
npm install -g typescript
```

Nest.js 框架可以使用 npm 包管理器安装。

```
npm install -g @nestjs/cli
```

## 在 Nest.js 中使用 TypeScript

Nest.js 使用 TypeScript 作为其编程语言。这意味着在开发 Nest.js 应用程序时需要使用 TypeScript。

TypeScript 是 JavaScript 的超集。这意味着任何有效的 JavaScript 代码也是有效的 TypeScript 代码。 TypeScript 将可选的静态类型添加到您的代码中。

使用 TypeScript 而不是 JavaScript 的好处包括：

- TypeScript 是静态类型的。这意味着 TypeScript 编译器可以在执行代码之前检查代码中的错误。这有助于防止将错误引入您的代码中。

- TypeScript 编译器可以生成与旧版 JavaScript 兼容的 JavaScript 代码。这被称为“针对”特定的 JavaScript 版本。当您需要支持较旧的浏览器或服务器时，这会很有帮助。

- TypeScript 带有自己的类型定义文件。这些文件可用于向 TypeScript 提供有关代码中预期的值类型的信息。这在使用用 JavaScript 编写的第三方库时特别有用。

Nest.js 在其整个代码库中使用 TypeScript 语言。这意味着您需要熟悉 TypeScript 才能有效地使用 Nest.js。

如果您不熟悉 TypeScript，可以查看 TypeScript 网站上的 TypeScript 教程。

## 创建一个 Nest.js 应用程序

现在您已经安装了 TypeScript 和 Nest.js，您可以创建一个 Nest.js 应用程序。

Nest.js CLI 可用于创建新的 Nest.js 应用程序。

```
nest new my-api
```

这将在名为“my-api”的目录中创建一个新的 Nest.js 应用程序。

## 定义路由

路由在 Nest.js 路由器中定义。路由器是用于定义应用程序路由的模块。

路由由路径和处理函数定义。路径是一个字符串，用于匹配传入请求的 URL。处理函数用于处理传入的请求并生成响应。

在 Nest.js 中，路由在文件 ```app.routing.ts```. 

```打字稿
从'@nestjs/common'导入{ModuleWithProviders，RouterModule，Routes}；
从'./app.controller'导入{AppController}；
从'./app.service'导入{AppService}；

常量路线：路线= [
  { 路径：'/'，控制器：AppController，方法：'get'}，
];

export const AppRoutingModule: ModuleWithProviders = RouterModule.forRoot(routes);
```

In the code above, a route is defined for the path ```/```. This route will match the URL ```/``` and will use the ```AppController``` to handle the request. 

The ```AppController``` is a Nest.js controller. Controllers are responsible for handling requests and generating responses. 

```打字稿
从'@nestjs/common'导入{控制器，获取}；
从'./app.service'导入{AppService}；

@控制器（）
导出类 AppController {
  构造函数（私有只读应用服务：AppService）{}

  @得到（）
  getHello(): 字符串 {
    返回 this.appService.getHello();
  }
}
```

In the code above, the ```AppController``` is annotated with the ```@Controller``` decorator. This decorator tells Nest.js that this class is a controller. 

The ```AppController``` has a single route handler. This handler is annotated with the ```@Get``` decorator. This decorator tells Nest.js that this handler will process GET requests. 

The ```getHello()``` handler is a simple handler that returns the string "Hello World!". 

## Defining Services

Services are used to encapsulate business logic in Nest.js applications. Services are injected into controllers and are used to process requests and generate responses. 

Services are defined in the file ```app.service.ts```. 

```打字稿
从'@nestjs/common'导入{Injectable}；

@Injectable()
导出类 AppService {
  getHello(): 字符串 {
    返回“你好世界！”；
  }
}
```

In the code above, the ```AppService``` is annotated with the ```@Injectable``` decorator. This decorator tells Nest.js that this class is a service. 

The ```AppService``` has a single method, ```getHello()```. This method returns the string "Hello World!". 

## Injecting Services

Services are injected into controllers using the ```打字稿
从'@nestjs/common'导入{Controller，Get，Inject}；
从'./app.service'导入{AppService}；

@控制器（）
导出类 AppController {
  构造函数（
    @Inject('APP_SERVICE')
    私有只读应用服务：应用服务，
  ）{}

  @得到（）
  getHello(): 字符串 {
    返回 this.appService.getHello();
  }
}
``` decorator. 

```AppService```

In the code above, the ```@Inject()``` is injected into the ```AppController``` using the ```@Inject()``` decorator. The ```@Inject()``` decorator takes a service token as a parameter. The service token is used to identify the service that is being injected. 

The ```
嵌套开始
```

这将在端口 3000 上启动 Nest.js 应用程序。