---
title: 021: Creating custom pipes in Nest.js
description: 
published: true
date: 2023-02-15T02:32:24.853Z
tags: 
editor: markdown
dateCreated: 2023-02-15T02:32:17.108Z
---

- [021: Creación de tuberías personalizadas en Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/021-creating-custom-pipes-in-nest-js)
{.links-list}
- [021: 在 Nest.js 中创建自定义管道***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/021-creating-custom-pipes-in-nest-js)
{.links-list}
- [021: Nest.js에서 커스텀 파이프 만들기***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/021-creating-custom-pipes-in-nest-js)
{.links-list}


# Creating custom pipes in Nest.js

Pipes are a great way to transform data in Nest.js. In this post, we'll learn how to create custom pipes.

## What are pipes?

Pipes are a feature of Nest.js that allow for transforming data as it flows through the application. For example, a pipe could be used to convert a string to uppercase, or to format a date.

Pipes can be used in many different places in Nest.js, including:

- In controllers, to transform data before it is used in a route
- In services, to transform data before it is persisted to a database
- In pipes, to transform data before it is returned to the client

## How to create a custom pipe

Creating a custom pipe is simple. First, we need to create a new file in the `pipes` directory. The file name should end in `.pipe.ts`.

Next, we need to import the ` PipeTransform` interface from `@nestjs/common`:

```typescript
import { PipeTransform } from '@nestjs/common';
```

The `PipeTransform` interface defines a single method, `transform`. This method is used to transform the data. The method accepts two arguments:

- `value`: The data to be transformed. This can be any data type.
- `metadata`: metadata about the value. This is an object with the following properties:
  - `type`: The data type of the value. This is useful for ensuring that the data is of the correct type.
  - `data`: Any other data that is associated with the value. This is useful for providing context to the transformation.

The `transform` method should return the transformed data.

Let's look at an example. Suppose we have a list of strings, and we want to convert them to uppercase. We could do this with the following pipe:

```typescript
import { PipeTransform } from '@nestjs/common';

export class StringToUppercasePipe implements PipeTransform {
  transform(value: string, metadata: PipeTransformMetadata) {
    return value.toUpperCase();
  }
}
```

## How to use a custom pipe

Once we have created a custom pipe, we can use it in our application by decorating the controller or service method with the `@UsePipes` decorator:

```typescript
import { Controller, Get, UsePipes } from '@nestjs/common';
import { StringToUppercasePipe } from './string-to-uppercase.pipe';

@Controller('/')
export class AppController {
  @Get('/')
  @UsePipes(StringToUppercasePipe)
  getHello(): string {
    return 'Hello, world!';
  }
}
```

In the example above, the `@UsePipes` decorator is used to apply the `StringToUppercasePipe` to the `getHello` method. This means that any strings returned by the method will be converted to uppercase.

## Summary

In this post, we've learned how to create custom pipes in Nest.js. Pipes are a great way to transform data as it flows through the application.