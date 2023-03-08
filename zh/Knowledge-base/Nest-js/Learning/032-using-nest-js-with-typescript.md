---
title: 032：将 Nest.js 与 TypeScript 结合使用
description: 
published: true
date: 2023-02-12T09:55:33.962Z
tags: 
editor: markdown
dateCreated: 2023-02-12T09:55:32.033Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [032: Using Nest.js with TypeScript***English** document is available*](/en/Knowledge-base/Nest-js/Learning/032-using-nest-js-with-typescript)
{.links-list}


# 将 Nest.js 与 TypeScript 结合使用

Nest.js 是一个用于构建高效、可扩展的 Node.js 服务器端应用程序的框架。它使用 TypeScript，这是一种类型化的 JavaScript 超集，可编译为纯 JavaScript。

在这篇文章中，我们将向您展示如何将 Nest.js 与 TypeScript 结合使用。我们将完成设置 Nest.js 项目、配置 TypeScript 和编写简单控制器的步骤。

## 设置一个 Nest.js 项目

首先，让我们创建一个新的 Nest.js 项目。我们将使用 Nest CLI 生成项目框架：

```
$ nest new project-name
```

这将创建一个名为“project-name”的新目录，其结构如下：

```
project-name
├── README.md
├── node_modules
├── package-lock.json
├── package.json
├── tsconfig.json
└── tslint.json
```

接下来，让我们为我们的项目安装依赖项：

```
$ cd project-name
$ npm install
```

## 配置打字稿

Nest.js 默认使用 TypeScript，所以我们不需要单独安装。但是，我们确实需要配置它。

打开 tsconfig.json 并添加以下选项：

```js
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "dist",
    "strict": true
  }
}
```

这些选项会将我们的 TypeScript 代码编译为 ES6，并使用 CommonJS 模块格式。 `outDir` 选项指定编译后的 JavaScript 文件的输出目录。而 `strict` 选项启用严格的类型检查。

## 编写控制器

现在我们的项目已经建立，我们可以编写一个控制器。控制器负责处理 HTTP 请求并返回响应。

让我们创建一个名为 src/controllers/hello.controller.ts 的文件：

```ts
import { Controller, Get } from '@nestjs/common';

@Controller('hello')
export class HelloController {
  @Get()
  public async index(): Promise<string> {
    return 'Hello, world!';
  }
}
```

这个控制器有一个“@Get”路由，它返回字符串“Hello, world!”。

要使用 Nest.js 注册这个控制器，我们需要创建一个模块。让我们创建一个名为 `src/modules/hello.module.ts` 的文件：

```ts
import { Module } from '@nestjs/common';
import { HelloController } from '../controllers/hello.controller';

@Module({
  controllers: [HelloController]
})
export class HelloModule {}
```

该模块导入“HelloController”并将其注册到 Nest.js。

最后，我们需要告诉 Nest.js 使用这个模块。我们可以通过将它添加到 `app.module.ts` 文件来做到这一点：

```ts
import { Module } from '@nestjs/common';
import { HelloModule } from './modules/hello.module';

@Module({
  imports: [HelloModule]
})
export class AppModule {}
```

现在我们的控制器已经注册，我们可以启动 Nest.js 服务器：

```
$ npm start
```

然后在浏览器中打开 http://localhost:3000/hello。您应该看到字符串“Hello, world!”。

## 结论

在这篇文章中，我们向您展示了如何将 Nest.js 与 TypeScript 结合使用。我们已经建立了一个 Nest.js 项目，配置了 TypeScript，并编写了一个简单的控制器。