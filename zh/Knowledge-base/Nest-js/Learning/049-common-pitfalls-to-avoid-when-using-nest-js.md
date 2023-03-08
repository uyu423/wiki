---
title: 049：使用 Nest.js 时要避免的常见陷阱
description: 
published: true
date: 2023-02-02T04:17:39.188Z
tags: 
editor: markdown
dateCreated: 2023-02-02T04:17:37.611Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [049: Common pitfalls to avoid when using Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/049-common-pitfalls-to-avoid-when-using-nest-js)
{.links-list}


# 049: 使用 Nest.js 时要避免的常见陷阱

Nest.js 是用于构建 Node.js 应用程序的强大框架。然而，与任何框架一样，有一些常见的陷阱可能会让刚接触 Nest 的开发人员感到困惑。在这篇文章中，我们将看看使用 Nest.js 时最常犯的一些错误，以及如何避免这些错误。

## 1. 没有正确初始化 Nest.js

使用 Nest.js 时最常见的错误之一是未能正确初始化框架。创建新项目时，必须使用 `--init` 标志初始化 Nest.js：

```
nest new my-project --init
```

如果您忘记包含 `--init` 标志，您的项目将无法正确设置，并且您会遇到错误。

## 2. 不使用@Module 装饰器

另一个经常犯的错误是在创建模块时忘记使用 @Module 装饰器。所有 Nest.js 模块都需要 @Module 装饰器：

```javascript
import { Module } from '@nestjs/common';

@Module({})
export class MyModule {}
```

如果您忘记使用 @Module 装饰器，Nest.js 将无法正确识别您的模块，您将遇到错误。

## 3. 不使用@Controller 装饰器

同样，所有 Nest.js 控制器都需要 @Controller 装饰器：

```javascript
import { Controller } from '@nestjs/common';

@Controller('/my-controller')
export class MyController {}
```

如果您忘记使用“@Controller”装饰器，Nest.js 将无法正确识别您的控制器，您将遇到错误。

## 4. 不使用@Injectable 装饰器

另一个经常被遗忘的装饰器是 @Injectable 装饰器。所有 Nest.js 服务都需要 @Injectable 装饰器：

```javascript
import { Injectable } from '@nestjs/common';

@Injectable()
export class MyService {}
```

如果您忘记使用 @Injectable 装饰器，Nest.js 将无法正确识别您的服务，您将遇到错误。

## 5. 不使用@NestModule 装饰器

另一个经常犯的错误是在创建模块时忘记使用 @NestModule 装饰器。所有 Nest.js 模块都需要 @NestModule 装饰器：

```javascript
import { NestModule } from '@nestjs/common';

@NestModule({})
export class MyModule {}
```

如果您忘记使用“@NestModule”装饰器，Nest.js 将无法正确识别您的模块，您将遇到错误。

## 6. 不使用@NestController 装饰器

同样，所有 Nest.js 控制器都需要 @NestController 装饰器：

```javascript
import { NestController } from '@nestjs/common';

@NestController('/my-controller')
export class MyController {}
```

如果您忘记使用“@NestController”装饰器，Nest.js 将无法正确识别您的控制器，您将遇到错误。

## 7. 不使用@NestInjectable 装饰器

另一个经常被遗忘的装饰器是 @NestInjectable 装饰器。所有 Nest.js 服务都需要 @NestInjectable 装饰器：

```javascript
import { NestInjectable } from '@nestjs/common';

@NestInjectable()
export class MyService {}
```

如果您忘记使用 @NestInjectable 装饰器，Nest.js 将无法正确识别您的服务，您将遇到错误。

## 8. 不使用@Component 装饰器

另一个经常犯的错误是在创建模块时忘记使用 @Component 装饰器。所有 Nest.js 模块都需要 @Component 装饰器：

```javascript
import { Component } from '@nestjs/common';

@Component({})
export class MyModule {}
```

如果您忘记使用 @Component 装饰器，Nest.js 将无法正确识别您的模块，您将遇到错误。

## 9. 不使用@Controller 装饰器

同样，所有 Nest.js 控制器都需要 @Controller 装饰器：

```javascript
import { Controller } from '@nestjs/common';

@Controller('/my-controller')
export class MyController {}
```

如果您忘记使用“@Controller”装饰器，Nest.js 将无法正确识别您的控制器，您将遇到错误。

## 10. 不使用@Injectable 装饰器

另一个经常被遗忘的装饰器是 @Injectable 装饰器。所有 Nest.js 服务都需要 @Injectable 装饰器：

```javascript
import { Injectable } from '@nestjs/common';

@Injectable()
export class MyService {}
```

如果您忘记使用 @Injectable 装饰器，Nest.js 将无法正确识别您的服务，您将遇到错误。