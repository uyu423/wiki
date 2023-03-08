---
title: 024：在 Nest.js 中创建和使用 REST API
description: 
published: true
date: 2023-02-09T06:55:56.621Z
tags: 
editor: markdown
dateCreated: 2023-02-09T06:55:54.959Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [024: Creating and consuming REST APIs in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/024-creating-and-consuming-rest-apis-in-nest-js)
{.links-list}


# 介绍

Nest.js 是一个用于构建服务器端应用程序的 Node.js 框架。它基于 Express.js 并使用 TypeScript。

该框架提供了一组用于创建和使用 REST API 的工具和库。

在本文中，我们将学习如何在 Nest.js 中创建和使用 REST API。

# 在 Nest.js 中创建 REST API

Nest.js 提供了一组用于创建 REST API 的注释和装饰器。

## 基于注解的 API

Nest.js 注释基于 reflect-metadata 库中的装饰器。

要使用注解，我们需要安装 reflect-metadata 库：

```
npm install reflect-metadata --save
```

然后我们可以使用@Controller 和@Get 注释来创建一个简单的 REST API：

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('/api')
export class MyController {
  @Get('/hello')
  public hello(): string {
    return 'Hello World!';
  }
}
```

@Controller 注释定义了控制器的路径。 @Get 注释定义了控制器的方法和路径。

在上面的例子中，控制器可以在 ```/api/hello``` 访问。

我们还可以使用@Post、@Put、@Delete 和@Patch 注释来创建用于创建、更新和删除资源的REST API。

## 基于装饰器的 API

Nest.js 还提供了一组用于创建 REST API 的装饰器。

要使用装饰器，我们需要安装@nestjs/common 库：

```
npm install @nestjs/common --save
```

然后我们可以使用 @Controller 和 @Get 装饰器来创建一个简单的 REST API：

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('/api')
export class MyController {
  @Get('/hello')
  public hello(): string {
    return 'Hello World!';
  }
}
```

@Controller 装饰器定义了控制器的路径。 @Get 装饰器定义了控制器的方法和路径。

在上面的例子中，控制器可以在 ```/api/hello``` 访问。

我们还可以使用@Post、@Put、@Delete 和@Patch 装饰器来创建用于创建、更新和删除资源的 REST API。

# 在 Nest.js 中使用 REST API

Nest.js 提供了一组用于使用 REST API 的库。

## HTTP 客户端

Nest.js 包含一个基于 XMLHttpRequest API 的内置 HTTP 客户端。

要使用 HTTP 客户端，我们需要安装 @nestjs/common 库：

```
npm install @nestjs/common --save
```

然后我们可以将 HTTP 客户端注入我们的控制器并使用它来发出 HTTP 请求：

```typescript
import { Controller, Get, Inject } from '@nestjs/common';
import { HttpClient } from '@nestjs/common';

@Controller('/api')
export class MyController {
  constructor(private readonly httpClient: HttpClient) {}

  @Get('/hello')
  public async hello(): Promise<string> {
    const response = await this.httpClient.get('https://example.com/api/hello');
    return response.data;
  }
}
```

在上面的示例中，我们将 HTTP 客户端注入到我们的控制器中，并使用它向 https://example.com/api/hello 发出 GET 请求。

我们还可以使用 HTTP 客户端发出 POST、PUT、PATCH 和 DELETE 请求。

## 公理

Nest.js 还支持 Axios HTTP 客户端。

要使用 axios，我们需要安装 axios 和 @nestjs/common 库：

```
npm install axios @nestjs/common --save
```

然后我们可以将 Axios HTTP 客户端注入我们的控制器并使用它来发出 HTTP 请求：

```typescript
import { Controller, Get, Inject } from '@nestjs/common';
import axios from 'axios';

@Controller('/api')
export class MyController {
  constructor(@Inject('AxiosInstance') private readonly axiosInstance: typeof axios) {}

  @Get('/hello')
  public async hello(): Promise<string> {
    const response = await this.axiosInstance.get('https://example.com/api/hello');
    return response.data;
  }
}
```

在上面的示例中，我们将 Axios HTTP 客户端注入到我们的控制器中，并使用它向 https://example.com/api/hello 发出 GET 请求。

我们还可以使用 Axios HTTP 客户端发出 POST、PUT、PATCH 和 DELETE 请求。

# 结论

在本文中，我们学习了如何在 Nest.js 中创建和使用 REST API。