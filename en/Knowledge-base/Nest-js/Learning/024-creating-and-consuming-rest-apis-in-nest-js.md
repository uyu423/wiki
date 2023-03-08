---
title: 024: Creating and consuming REST APIs in Nest.js
description: 
published: true
date: 2023-02-09T06:56:01.073Z
tags: 
editor: markdown
dateCreated: 2023-02-09T06:55:54.967Z
---

- [024: Creación y consumo de API REST en Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/024-creating-and-consuming-rest-apis-in-nest-js)
{.links-list}
- [024：在 Nest.js 中创建和使用 REST API***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/024-creating-and-consuming-rest-apis-in-nest-js)
{.links-list}
- [024: Nest.js에서 REST API 생성 및 사용***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/024-creating-and-consuming-rest-apis-in-nest-js)
{.links-list}


# Introduction

Nest.js is a Node.js framework for building server-side applications. It is based on Express.js and uses TypeScript.

The framework provides a set of tools and libraries for creating and consuming REST APIs.

In this post, we will learn how to create and consume REST APIs in Nest.js.

# Creating REST APIs in Nest.js

Nest.js provides a set of annotations and decorators for creating REST APIs.

## Annotation-based APIs

Nest.js annotations are based on the decorators from the reflect-metadata library.

To use annotations, we need to install the reflect-metadata library:

```
npm install reflect-metadata --save
```

We can then use the @Controller and @Get annotations to create a simple REST API:

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

The @Controller annotation defines the controller's path. The @Get annotation defines the controller's method and path.

In the example above, the controller will be accessible at ```/api/hello```.

We can also use the @Post, @Put, @Delete, and @Patch annotations to create REST APIs for creating, updating, and deleting resources.

## Decorator-based APIs

Nest.js also provides a set of decorators for creating REST APIs.

To use decorators, we need to install the @nestjs/common library:

```
npm install @nestjs/common --save
```

We can then use the @Controller and @Get decorators to create a simple REST API:

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

The @Controller decorator defines the controller's path. The @Get decorator defines the controller's method and path.

In the example above, the controller will be accessible at ```/api/hello```.

We can also use the @Post, @Put, @Delete, and @Patch decorators to create REST APIs for creating, updating, and deleting resources.

# Consuming REST APIs in Nest.js

Nest.js provides a set of libraries for consuming REST APIs.

## HTTP Client

Nest.js includes a built-in HTTP client based on the XMLHttpRequest API.

To use the HTTP client, we need to install the @nestjs/common library:

```
npm install @nestjs/common --save
```

We can then inject the HTTP client into our controller and use it to make HTTP requests:

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

In the example above, we injected the HTTP client into our controller and used it to make a GET request to https://example.com/api/hello.

We can also use the HTTP client to make POST, PUT, PATCH, and DELETE requests.

## Axios

Nest.js also supports the Axios HTTP client.

To use Axios, we need to install the axios and @nestjs/common libraries:

```
npm install axios @nestjs/common --save
```

We can then inject the Axios HTTP client into our controller and use it to make HTTP requests:

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

In the example above, we injected the Axios HTTP client into our controller and used it to make a GET request to https://example.com/api/hello.

We can also use the Axios HTTP client to make POST, PUT, PATCH, and DELETE requests.

# Conclusion

In this post, we learned how to create and consume REST APIs in Nest.js.