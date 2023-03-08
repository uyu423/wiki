---
title: 013: 在 Nest.js 中实现授权
description: 
published: true
date: 2023-02-14T23:32:20.822Z
tags: 
editor: markdown
dateCreated: 2023-02-14T23:32:18.981Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [013: Implementing authorization in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/013-implementing-authorization-in-nest-js)
{.links-list}


# 在 Nest.js 中实现授权

Nest.js 是一个用于构建可扩展的服务器端应用程序的 Node.js 框架。它使用渐进式 JavaScript，使用 TypeScript 构建（保留与纯 JavaScript 的兼容性）并结合了面向对象编程、函数式编程和函数式响应式编程的元素。

在这篇文章中，我们将重点关注如何在 Nest.js 应用程序中实现授权。在继续讨论如何在 Nest.js 中实现它之前，我们将了解什么是授权及其重要性。

## 什么是授权？

授权是确定是否允许用户执行操作或访问资源的过程。它通常涉及检查用户是否具有执行操作所需的权限。

在 Web 应用程序中，授权通常通过检查用户身份然后将其与授权用户列表进行比较来完成。如果用户获得授权，则允许他们访问该资源。如果他们未被授权，则不允许他们访问该资源。

有两种主要类型的授权：

- **身份验证**：这是验证用户是他们所说的人的过程。在 Web 应用程序中，这通常是通过根据用户数据库检查用户的凭据（例如用户名和密码）来完成的。

- **授权**：这是验证用户是否具有访问资源的必要权限的过程。在 Web 应用程序中，这通常是通过根据授权用户列表检查用户身份来完成的。如果用户获得授权，则允许他们访问该资源。如果他们未被授权，则不允许他们访问该资源。

## 为什么授权很重要？

授权很重要，因为它有助于确保您的应用程序安全。通过仅允许授权用户访问资源，您可以帮助防止未经授权访问敏感数据。

## 在 Nest.js 中实现授权

Nest.js 提供了多种方式来实现授权。在本节中，我们将介绍两种最常见的方法：使用“@Authorized()”装饰器和“CanActivate”守卫。

### 使用 `@Authorized()` 装饰器

`@Authorized()` 装饰器可用于限制对控制器或操作的访问。它有一个参数，即允许访问控制器或操作的角色列表。

例如，以下控制器只能由具有“ADMIN”角色的用户访问：

```typescript
@Controller('/users')
@Authorized(['ADMIN'])
export class UserController {

}
```

如果没有 `ADMIN` 角色的用户试图访问 `/users` 端点，他们将收到 `unauthorized` 错误。

### 使用 `CanActivate` 守卫

`CanActivate` 守卫可用于限制对路由的访问。它们采用单个参数，即允许访问路由的角色列表。

例如，只有具有“ADMIN”角色的用户才能访问以下路由：

```typescript
@Get('/users')
@CanActivate(['ADMIN'])
export class UserController {

}
```

如果没有 `ADMIN` 角色的用户试图访问 `/users` 端点，他们将收到 `unauthorized` 错误。

## 附加信息

- Nest.js 文档：https://docs.nestjs.com/
- TypeScript 文档：https://www.typescriptlang.org/docs/handbook/basic-types.html