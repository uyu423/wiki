---
title: 021: 在 Nest.js 中创建自定义管道
description: 
published: true
date: 2023-02-15T02:32:18.696Z
tags: 
editor: markdown
dateCreated: 2023-02-15T02:32:17.099Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [021: Creating custom pipes in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/021-creating-custom-pipes-in-nest-js)
{.links-list}


# 在 Nest.js 中创建自定义管道

管道是在 Nest.js 中转换数据的好方法。在本文中，我们将学习如何创建自定义管道。

## 什么是管道？

管道是 Nest.js 的一项功能，允许在数据流经应用程序时对其进行转换。例如，管道可用于将字符串转换为大写，或格式化日期。

管道可以用在 Nest.js 的许多不同地方，包括：

- 在控制器中，在数据用于路由之前转换数据
- 在服务中，在数据持久化到数据库之前转换数据
- 在管道中，在数据返回给客户端之前转换数据

## 如何创建自定义管道

创建自定义管道很简单。首先，我们需要在 `pipes` 目录中创建一个新文件。文件名应以 .pipe.ts 结尾。

接下来，我们需要从 @nestjs/common 导入 PipeTransform 接口：

```typescript
import { PipeTransform } from '@nestjs/common';
```

`PipeTransform` 接口定义了一个方法，`transform`。此方法用于转换数据。该方法接受两个参数：

- `value`：要转换的数据。这可以是任何数据类型。
- `metadata`：关于值的元数据。这是一个具有以下属性的对象：
  - `type`：值的数据类型。这对于确保数据的类型正确很有用。
  - `data`：与该值关联的任何其他数据。这对于为转换提供上下文很有用。

`transform` 方法应该返回转换后的数据。

让我们看一个例子。假设我们有一个字符串列表，我们想将它们转换为大写。我们可以使用以下管道来做到这一点：

```typescript
import { PipeTransform } from '@nestjs/common';

export class StringToUppercasePipe implements PipeTransform {
  transform(value: string, metadata: PipeTransformMetadata) {
    return value.toUpperCase();
  }
}
```

## 如何使用自定义管道

一旦我们创建了自定义管道，我们就可以通过使用 @UsePipes 装饰器装饰控制器或服务方法在我们的应用程序中使用它：

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

在上面的示例中，@UsePipes 装饰器用于将 StringToUppercasePipe 应用于 getHello 方法。这意味着该方法返回的任何字符串都将转换为大写。

## 概括

在本文中，我们学习了如何在 Nest.js 中创建自定义管道。管道是在数据流经应用程序时转换数据的好方法。