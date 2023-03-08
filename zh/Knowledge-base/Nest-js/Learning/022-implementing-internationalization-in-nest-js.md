---
title: 022: 在 Nest.js 中实现国际化
description: 
published: true
date: 2023-02-15T03:32:43.672Z
tags: 
editor: markdown
dateCreated: 2023-02-15T03:32:36.016Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [022: Implementing internationalization in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/022-implementing-internationalization-in-nest-js)
{.links-list}


# 在 Nest.js 中实现国际化

Nest.js 是一个用于构建可扩展的服务器端应用程序的 Node.js 框架。它使用 TypeScript（JavaScript 的超集），并结合了面向对象编程、函数式编程和函数式响应式编程的元素。

在这篇文章中，我们将研究如何在 Nest.js 中实现国际化。国际化是为多个市场设计和开发产品、应用程序或网站的过程。 Nest.js 为 i18n 提供了一个内置模块，可以轻松地向 Nest.js 应用程序添加国际化。

## 入门

在我们开始之前，让我们确保我们拥有我们需要的一切。首先，我们需要安装@nestjs/i18n 模块。我们可以使用以下命令执行此操作：

```
npm install @nestjs/i18n
```

安装模块后，我们需要为 i18n 创建一个配置文件。我们将这个文件命名为 i18n.options.ts ，它将位于我们的 Nest.js 项目的 src 目录中。该文件应如下所示：

```typescript
import {
  I18nModuleOptions,
  I18nCoreModule,
} from '@nestjs/i18n';

const i18nModuleOptions: I18nModuleOptions = {
  fallbacks: {
    'en-US': 'en',
  },
  defaultLocale: 'en',
  path: __dirname,
};

export { i18nModuleOptions };
```

在这个文件中，我们将 i18n 模块配置为使用英语作为默认语言。我们还告诉模块在 src 目录中查找语言文件。

## 创建语言文件

现在我们已经设置了 i18n 配置文件，我们需要创建我们的语言文件。对于此示例，我们将创建两个语言文件：一个用于英语，一个用于西班牙语。我们将分别调用这些文件 en.json 和 es.json。

en.json 文件应如下所示：

```json
{
  "hello": "Hello, world!"
}
```

es.json 文件应该如下所示：

```json
{
  "hello": "¡Hola, mundo!"
}
```

这些文件包含我们对“hello”键的翻译。请注意，无论使用何种语言，文件的结构都是相同的。这是因为 i18n 模块使用 CommonJS 模块格式。

## 在我们的 Nest.js 应用程序中使用语言文件

现在我们已经设置了语言文件，我们可以开始在我们的 Nest.js 应用程序中使用它们。

首先，我们需要在应用程序模块中导入 I18nModule。我们可以使用以下代码来做到这一点：

```typescript
import { Module } from '@nestjs/common';
import { I18nModule } from '@nestjs/i18n';

@Module({
  imports: [
    I18nModule.forRoot(),
  ],
})
export class ApplicationModule {}
```

接下来，我们需要创建一个服务来负责处理我们的翻译。我们将此服务称为 I18nService。该服务应如下所示：

```typescript
import { Injectable } from '@nestjs/common';
import { I18nService as I18n } from '@nestjs/i18n';

@Injectable()
export class I18nService {
  constructor(private readonly i18n: I18n) {}

  translate(key: string, params?: any) {
    return this.i18n.translate(key, params);
  }
}
```

在此服务中，我们从 @nestjs/i18n 模块注入 I18nService。我们还创建了一个 translate() 方法来负责处理我们的翻译。

现在我们已经设置了我们的服务，我们可以在我们的控制器中使用它。对于此示例，我们将创建一个简单的控制器，它以用户的首选语言返回问候语。控制器应如下所示：

```typescript
import { Controller, Get, Res } from '@nestjs/common';
import { Response } from 'express';
import { I18nService } from './i18n.service';

@Controller()
export class AppController {
  constructor(private readonly i18nService: I18nService) {}

  @Get()
  getHello(@Res() res: Response) {
    const message = this.i18nService.translate('hello');
    res.send(message);
  }
}
```

在这个控制器中，我们注入了 I18nService。我们还创建了一个 getHello() 方法，它以用户的首选语言返回问候语。

## 测试我们的 Nest.js 应用程序

现在我们已经设置了 Nest.js 应用程序，让我们测试它以确保一切都按预期工作。我们可以使用以下命令执行此操作：

```
npm test
```

如果一切都按预期工作，您应该会看到以下输出：

```
> nestjs-i18n@0.0.1 test /Users/username/projects/nestjs-i18n
> jest

 PASS  src/app.controller.spec.ts
  AppController
    GET /
      ✓ should return "Hello, world!" (5ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.548s
Ran all test suites.
```

## 结论

在这篇文章中，我们研究了如何在 Nest.js 中实现国际化。我们已经创建了语言文件和一项服务来处理我们的翻译。我们还创建了一个控制器，它以用户的首选语言返回问候语。