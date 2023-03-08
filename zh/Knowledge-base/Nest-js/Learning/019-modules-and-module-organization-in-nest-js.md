---
title: 019: Nest.js 中的模块和模块组织
description: 
published: true
date: 2023-02-06T01:17:53.227Z
tags: 
editor: markdown
dateCreated: 2023-02-06T01:17:47.613Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [019: Modules and module organization in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/019-modules-and-module-organization-in-nest-js)
{.links-list}


# Nest.js 中的模块和模块组织

Nest.js 是一个用于构建可扩展的服务器端应用程序的 Node.js 框架。它使用现代 JavaScript，使用 TypeScript（可选）构建，并结合了面向对象编程、函数式编程和响应式编程的元素。

Nest.js 深受 Angular 的启发。事实上，Nest.js 的作者就是创建 Angular 的人。 Nest.js 与 Angular 有许多相同的概念和想法，因此如果您熟悉 Angular，您会觉得 Nest.js 非常熟悉。

Nest.js 中的关键概念之一是模块。模块用于组织代码和构建应用程序。 Nest.js 带有一个内置的模块系统，它基于 CommonJS 模块系统。

模块就像图书馆。它们是一种打包代码的方式，以便它可以在应用程序的其他部分中重用。 Nest.js 模块与 Angular 模块非常相似。

每个 Nest.js 模块都是相关组件、指令、管道和服务的集合。模块可以导入其他模块，这为您提供了一种在模块之间共享代码的方法。

模块还可以导出组件、指令、管道和服务，以便它们可以在其他模块中使用。

Nest.js 模块不同于 Node.js 模块。 Node.js 模块用于构建在 Node.js 上运行的应用程序。 Nest.js 模块用于构建在 Node.js 上运行并使用 Nest.js 的应用程序。

Node.js 模块通常打包为库并发布到 npm。 Nest.js 模块通常打包为库并发布到 npm。

## 创建模块

创建 Nest.js 模块很简单。您只需要一个目录，其中包含一个名为“module.ts”的文件。 `module.ts` 文件是模块的入口点。

```typescript
import { Module } from '@nestjs/common';

@Module({})
export class MyModule {}
```

`@Module` 装饰器用于定义 Nest.js 模块。 `@Module` 装饰器接受一个具有一些属性的对象。最重要的属性是“imports”属性。

`imports` 属性是这个模块所依赖的其他模块的数组。这就是您在模块之间共享代码的方式。

```typescript
import { Module } from '@nestjs/common';

@Module({
  imports: [OtherModule],
})
export class MyModule {}
```

不需要 `imports` 属性。如果不需要在模块之间共享代码，则不需要使用 imports 属性。

## 模块组织

Nest.js 应用程序通常被组织成一组模块。主模块是根模块，其他模块是子模块。

根模块是应用程序启动时引导的模块。其他模块由根模块加载。

子模块可以被其他子模块加载。这允许您创建模块的嵌套结构。

推荐的组织模块的方法是为应用程序中的每个功能设置一个功能模块。功能模块是封装应用程序功能的模块。

例如，如果你有一个博客功能，你就会有一个博客功能模块。博客功能模块将包含博客功能的所有代码。

功能模块通常组织成一个目录结构。例如，博客功能模块可能会组织成以下目录结构。

```
- blog
  - blog.module.ts
  - blog.service.ts
  - blog.controller.ts
  - blog.component.ts
  - blog.pipe.ts
  - blog.directive.ts
```

`blog.module.ts` 文件是博客功能模块的模块文件。目录中的其他文件是模块的组件。

构建应用程序的推荐方法是拥有一个根模块和一组功能模块。这为您提供了清晰的关注点分离和清晰的应用程序结构。

## 概括

模块是 Nest.js 中的一个关键概念。模块用于组织代码和构建应用程序。 Nest.js 带有一个内置的模块系统，它基于 CommonJS 模块系统。

每个 Nest.js 模块都是相关组件、指令、管道和服务的集合。模块可以导入其他模块，这为您提供了一种在模块之间共享代码的方法。

模块还可以导出组件、指令、管道和服务，以便它们可以在其他模块中使用。

Nest.js 模块不同于 Node.js 模块。 Node.js 模块用于构建在 Node.js 上运行的应用程序。 Nest.js 模块用于构建在 Node.js 上运行并使用 Nest.js 的应用程序。

Node.js 模块通常打包为库并发布到 npm。 Nest.js 模块通常打包为库并发布到 npm。

创建 Nest.js 模块很简单。您只需要一个目录，其中包含一个名为“module.ts”的文件。 `module.ts` 文件是模块的入口点。

`@Module` 装饰器用于定义 Nest.js 模块。 `@Module` 装饰器接受一个具有一些属性的对象。最重要的属性是“imports”属性。

`imports` 属性是这个模块所依赖的其他模块的数组。这就是您在模块之间共享代码的方式。

Nest.js 应用程序通常被组织成一组模块。主模块是根模块，其他模块是子模块。

子模块可以被其他子模块加载。这允许您创建模块的嵌套结构。

推荐的组织模块的方法是为应用程序中的每个功能设置一个功能模块。功能模块是封装应用程序功能的模块。

例如，如果你有一个博客功能，你就会有一个博客功能模块。博客功能模块将包含博客功能的所有代码。