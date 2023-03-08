---
title: 018：在 Nest.js 中创建可重用组件
description: 
published: true
date: 2023-02-07T21:17:22.330Z
tags: 
editor: markdown
dateCreated: 2023-02-07T21:17:16.591Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [018: Creating reusable components in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/018-creating-reusable-components-in-nest-js)
{.links-list}


# 在 Nest.js 中创建可重用组件

Nest.js 是用于构建 Node.js 应用程序的框架。它使用 TypeScript 并构建在 Express.js 之上。

使用 Nest.js 的好处之一是可以轻松创建可重用的组件。在这篇文章中，我们将看看如何在 Nest.js 中创建一个可重用的组件。

## 定义一个组件

创建可重用组件的第一步是定义它。我们可以使用 @Component 装饰器来做到这一点。

例如，假设我们要创建一个记录用户信息的组件。我们会这样定义它：

```typescript
@Component()
export class UserLoggerComponent {
  // ...
}
```

## 使用组件

一旦我们定义了一个组件，我们就可以通过将它注入控制器或服务来在我们的 Nest.js 应用程序中使用它。

例如，假设我们有一个控制器来处理创建用户的请求。我们可以将我们的 UserLoggerComponent 注入到这个控制器中，并用它来记录有关新用户的信息：

```typescript
@Controller('users')
export class UserController {
  constructor(private readonly userLogger: UserLoggerComponent) {}

  @Post()
  async createUser(@Body() userDto: UserDto) {
    // ...

    this.userLogger.log(userDto);

    // ...
  }
}
```

## 结论

在这篇文章中，我们了解了如何在 Nest.js 中创建可重用的组件。我们已经使用 @Component 装饰器定义了一个组件，并将其注入到控制器中以使用它。