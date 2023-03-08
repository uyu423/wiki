---
title: 048：编写 Nest.js 代码的最佳实践
description: 
published: true
date: 2023-02-03T07:23:45.121Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:23:43.462Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [048: Best practices for writing Nest.js code***English** document is available*](/en/Knowledge-base/Nest-js/Learning/048-best-practices-for-writing-nest-js-code)
{.links-list}


# 048：编写 Nest.js 代码的最佳实践

Nest.js 是用于构建 Node.js 应用程序的强大框架。它建立在 Express.js 之上并使用 TypeScript，这使得编写组织良好且可维护的代码变得容易。

在这篇文章中，我们将看看编写 Nest.js 代码的一些最佳实践。

## 使用正确的编码风格

编写代码时，使用正确的编码风格很重要。这将帮助您编写易于阅读和维护的代码。

您可以为 Nest.js 代码使用几种不同的编码风格。最受欢迎的是 Airbnb 风格指南。该风格指南被 Node.js 社区广泛使用，并已被许多公司采用。

另一个流行的风格指南是 StandardJS 风格指南。与 Airbnb 风格指南相比，这份风格指南没有那么固执己见，如果您不确定要使用哪种风格，它是一个不错的选择。

## 使用打字稿

Nest.js 是用 TypeScript 编写的，建议您在编写 Nest.js 代码时使用 TypeScript。 TypeScript 是 JavaScript 的类型化超集，可编译为纯 JavaScript。

TypeScript 是编写易于阅读和维护的代码的好方法。它还有助于防止代码中出现错误。

## 使用正确的依赖项

在编写 Nest.js 代码时，使用正确的依赖项很重要。您可以使用几种不同类型的依赖项。

第一种依赖类型是 Node.js 模块。这些是在 npm 上发布的模块，可以使用 npm install 命令安装。

第二种类型的依赖是 TypeScript 定义文件。这些文件为 TypeScript 提供类型信息。它们未在 npm 上发布，必须手动安装。

第三种依赖是 JavaScript 文件。这些文件未在 npm 上发布，必须手动安装。

## 使用正确的项目结构

在编写 Nest.js 代码时，使用正确的项目结构很重要。 Nest.js 的推荐项目结构如下：

```
- src
  - controllers
  - services
  - pipes
  - filters
  - interceptors
  - modules
  - middlewares
  - entities
  - dtos
  - providers
  - guards
  - exceptions
  - interceptors
  - main.ts
  - app.module.ts
```

## 使用正确的命名约定

在编写 Nest.js 代码时，使用正确的命名约定很重要。 Nest.js 的推荐命名约定如下：

- 控制器应命名为 *Controller.ts
- 服务应命名为 *Service.ts
- 管道应命名为 *Pipe.ts
- 过滤器应命名为 *Filter.ts
- 拦截器应命名为 *Interceptor.ts
- 模块应命名为 *Module.ts
- 中间件应命名为 *Middleware.ts
- 实体应命名为 *Entity.ts
- Dtos 应该命名为 *Dto.ts
- 供应商应命名为 *Provider.ts
- 守卫应命名为 *Guard.ts
- 异常应命名为 *Exception.ts

## 使用正确的编码模式

编写 Nest.js 代码时，使用正确的编码模式很重要。 Nest.js 的推荐编码模式如下：

- 控制器应该很薄
- 服务要厚
- 应该使用管道进行数据转换
- 过滤器应用于数据验证
- 拦截器应该用于日志记录
- 模块应该用于组织
- 应使用中间件进行身份验证
- 实体应用于数据建模
- Dtos应该用于数据传输
- 供应商应该用于依赖注入
- 应该使用警卫进行授权
- 异常应该用于错误处理

## 使用正确的测试方法

在编写 Nest.js 代码时，使用正确的测试方法很重要。 Nest.js 的推荐测试方法如下：

- 对小功能使用单元测试
- 对更大的功能使用集成测试
- 对整个应用程序使用端到端测试

## 使用正确的工具

编写 Nest.js 代码时，使用正确的工具很重要。 Nest.js 的推荐工具如下：

- 使用像 Visual Studio Code 这样的代码编辑器
- 使用像 Gulp 这样的构建工具
- 使用像 Jest 这样的测试框架
- 使用像 TSLint 这样的 linter

## 使用正确的文档

编写 Nest.js 代码时，使用正确的文档很重要。 Nest.js 的推荐文档如下：

- 使用 JSDoc 获取 JavaScript 文档
- 将 TypeDoc 用于 TypeScript 文档

## 结论

在这篇文章中，我们研究了一些编写 Nest.js 代码的最佳实践。我们已经看到，使用正确的编码风格、使用 TypeScript、使用正确的依赖项、使用正确的项目结构、使用正确的命名约定、使用正确的编码模式、使用正确的测试方法、使用正确的工具非常重要，并使用正确的文档。