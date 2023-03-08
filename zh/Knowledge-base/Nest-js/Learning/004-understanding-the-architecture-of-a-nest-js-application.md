---
title: 004：了解 Nest.js 应用程序的架构
description: 
published: true
date: 2023-02-14T01:56:43.346Z
tags: 
editor: markdown
dateCreated: 2023-02-14T01:56:36.144Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [004: Understanding the architecture of a Nest.js application***English** document is available*](/en/Knowledge-base/Nest-js/Learning/004-understanding-the-architecture-of-a-nest-js-application)
{.links-list}


# 了解 Nest.js 应用程序的架构

Nest.js 是一个用于构建可扩展的服务器端应用程序的 Node.js 框架。它使用现代 JavaScript，使用 TypeScript（编译为 JavaScript）构建，并结合了面向对象编程、函数式编程和响应式编程的元素。

Nest.js 应用程序被组织成一组嵌套模块。 Nest.js 模块等同于 Angular 模块，用于将相关组件、服务、管道和指令组合在一起。

Nest.js 模块的主要目的是提供一个单一的位置（或根），可以在其中找到单个功能或域的所有相关代码。这使得推理和维护 Nest.js 应用程序变得容易。

Nest.js 模块被组织成具有根模块和零个或多个子模块的层次结构。根模块是应用程序的入口点，通常用于配置 Nest.js 应用程序。子模块用于将功能或域的相关代码组合在一起。

下图显示了 Nest.js 应用程序的典型结构。 src 目录包含应用程序的源代码。 app.module.ts 文件是根模块，用于配置 Nest.js 应用程序。子模块用于将功能或域的相关代码组合在一起。

![图 1. Nest.js 应用程序的典型结构](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/img/app-structure.png)

src/app.module.ts 文件是根模块，用于配置 Nest.js 应用程序。 @Nestjs/common 模块被导入并用于提供 CommonModule 类。 CommonModule 类用于提供注入器服务。注入器服务用于解决依赖关系。

@Nestjs/core 模块被导入并用于提供 NestFactory 类。 NestFactory 类用于创建 Nest.js 应用程序实例。

AppModule 类被导入并用于定义 AppModule 类。 AppModule 类用于配置 Nest.js 应用程序。

AppModule 类使用 @Module() 装饰器进行注释。 @Module() 装饰器用于定义 Nest.js 模块。

AppModule 类被导入并用于定义 AppModule 类。 AppModule 类用于配置 Nest.js 应用程序。

AppModule 类使用 @Module() 装饰器进行注释。 @Module() 装饰器用于定义 Nest.js 模块。

AppModule 类包含一个构造函数和一个 configure() 方法。构造函数用于注入依赖项。 configure() 方法用于配置 Nest.js 应用程序。

src/app.controller.ts 文件用于定义 AppController 类。 AppController 类用于处理 HTTP 请求。

AppController 类使用 @Controller() 装饰器进行注释。 @Controller() 装饰器用于定义 Nest.js 控制器。

AppController 类包含一个 root() 方法。 root() 方法用于处理 HTTP GET 请求。

src/app.service.ts 文件用于定义 AppService 类。 AppService 类用于为控制器提供数据。

AppService 类使用 @Injectable() 装饰器进行注释。 @Injectable() 装饰器用于定义 Nest.js 服务。

AppService 类包含一个 getData() 方法。 getData() 方法用于返回控制器的数据。

src/environments/environment.ts 文件用于定义环境变量。环境变量用于配置 Nest.js 应用程序。

使用 environment() 函数将环境变量注入 AppModule 类。

environment() 函数用于将环境变量注入到 Nest.js 应用程序中。

environment() 函数将一个对象作为参数。该对象包含环境变量。

environment() 函数返回一个环境对象。 Environment 对象包含环境变量。

Environment 对象用于配置 Nest.js 应用程序。

src/main.ts 文件是 Nest.js 应用程序的入口点。 src/main.ts 文件用于创建 Nest.js 应用程序的实例。

src/main.ts 文件导入 AppModule 类。 AppModule 类用于配置 Nest.js 应用程序。

src/main.ts 文件使用 NestFactory 类来创建 Nest.js 应用程序的实例。

NestFactory 类是从 @nestjs/core 模块导入的。 NestFactory 类用于创建 Nest.js 应用程序实例。

NestFactory 类将 AppModule 类作为参数。 AppModule 类用于配置 Nest.js 应用程序。

NestFactory 类返回 Nest.js 应用程序的一个实例。

Nest.js 应用程序的实例用于启动 Nest.js 应用程序。

Nest.js 应用程序的实例是使用 start() 方法启动的。

start() 方法用于启动 Nest.js 应用程序。

start() 方法将端口号作为参数。端口号用于侦听 HTTP 请求。

start() 方法返回一个 Promise。当 Nest.js 应用程序启动时，Promise 被解析。

src/index.ts 文件是 TypeScript 编译器的入口点。 src/index.ts 文件用于编译 TypeScript 代码。

src/index.ts 文件导入 AppModule 类。 AppModule 类用于配置 Nest.js 应用程序。

src/index.ts 文件使用 tsconfig.json 文件来配置 TypeScript 编译器。

tsconfig.json 文件用于配置 TypeScript 编译器。

tsconfig.json 文件包含编译器选项。编译器选项用于配置 TypeScript 编译器。

tsconfig.json 文件用于将 TypeScript 代码编译成 JavaScript 代码。

使用 tsc 命令将 TypeScript 代码编译成 JavaScript 代码。

tsc 命令用于将 TypeScript 代码编译成 JavaScript 代码。

tsc 命令将 tsconfig.json 文件作为参数。 tsconfig.json 文件用于配置 TypeScript 编译器。

tsc 命令将 TypeScript 代码编译成 JavaScript 代码。

编译后的 JavaScript 代码放在 dist 目录中。

dist 目录包含已编译的 JavaScript 代码。

dist 目录是 TypeScript 编译器的输出目录。

Nest.js 应用程序使用 node 命令运行。

node 命令用于运行 Nest.js 应用程序。

node 命令将编译后的 JavaScript 代码作为参数。编译后的 JavaScript 代码放在 dist 目录中。

node 命令运行 Nest.js 应用程序。

Nest.js 应用程序在 Node.js 服务器上运行。

Node.js 服务器用于运行 Nest.js 应用程序。

Node.js 服务器是一个 JavaScript 运行时。

Node.js 服务器用于执行 JavaScript 代码。

使用网络浏览器访问 Nest.js 应用程序。

Web 浏览器用于访问 Nest.js 应用程序。

Web 浏览器用于向 Nest.js 应用程序发送 HTTP 请求。

Nest.js 应用程序可通过 http://localhost:3000 访问。

# 附加信息

Nest.js 是一个用于构建可扩展的服务器端应用程序的 Node.js 框架。它使用现代 JavaScript，使用 TypeScript（编译为 JavaScript）构建，并结合了面向对象编程、函数式编程和响应式编程的元素。

Nest.js 应用程序被组织成一组嵌套模块。 Nest.js 模块等同于 Angular 模块，用于将相关组件、服务、管道和指令组合在一起。

Nest.js 模块的主要目的是提供一个单一的位置（或根），可以在其中找到单个功能或域的所有相关代码。这使得推理和维护 Nest.js 应用程序变得容易。

Nest.js 模块被组织成具有根模块和零个或多个子模块的层次结构。根模块是应用程序的入口点，通常用于配置 Nest.js 应用程序。子模块用于将功能或域的相关代码组合在一起。

下图显示了 Nest.js 应用程序的典型结构。 src 目录包含应用程序的源代码。 app.module.ts 文件是根模块，用于配置 Nest.js 应用程序。子模块用于将功能或域的相关代码组合在一起。

![图 1. Nest.js 应用程序的典型结构](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/img/app-structure.png)

src/app.module.ts 文件是根模块，用于配置 Nest.js 应用程序。 @Nestjs/common 模块被导入并用于提供 CommonModule 类。 CommonModule 类用于提供注入器服务。注入器服务用于解决依赖关系。

@Nestjs/core 模块被导入并用于提供 NestFactory 类。 NestFactory 类用于创建 Nest.js 应用程序实例。

AppModule 类被导入并用于定义 AppModule 类。 AppModule 类用于配置 Nest.js 应用程序。

AppModule 类使用 @Module() 装饰器进行注释。 @Module() 装饰器用于定义 Nest.js 模块。

AppModule 类被导入并用于定义 AppModule 类。 AppModule 类用于配置 Nest.js 应用程序。

AppModule 类使用 @Module() 装饰器进行注释。 @Module() 装饰器用于定义 Nest.js 模块。

AppModule 类包含一个构造函数和一个 configure() 方法。构造函数用于注入依赖项。 configure() 方法用于配置 Nest.js 应用程序。

src/app.controller.ts 文件用于定义 AppController 类。 AppController 类用于处理 HTTP 请求。

AppController 类使用 @Controller() 装饰器进行注释。 @Controller() 装饰器用于定义 Nest.js 控制器。

AppController 类包含一个 root() 方法。 root() 方法用于处理 HTTP GET 请求。

src/app.service.ts 文件用于定义 AppService 类。 AppService 类用于为控制器提供数据。

AppService 类使用 @Injectable() 装饰器进行注释。 @Injectable() 装饰器用于定义 Nest.js 服务。

AppService 类包含一个 getData() 方法。 getData() 方法用于返回控制器的数据。

src/environments/environment.ts 文件用于定义环境变量。环境变量用于配置 Nest.js 应用程序。

使用 environment() 函数将环境变量注入 AppModule 类。

environment() 函数用于将环境变量注入到 Nest.js 应用程序中。

environment() 函数将一个对象作为参数。该对象包含环境变量。

environment() 函数返回一个环境对象。 Environment 对象包含环境变量。

Environment 对象用于配置 Nest.js 应用程序。

src/main.ts 文件是 Nest.js 应用程序的入口点。 src/main.ts 文件用于创建 Nest.js 应用程序的实例。

src/main.ts 文件导入 AppModule 类。 AppModule 类用于配置 Nest.js 应用程序。

src/main.ts 文件使用 NestFactory 类来创建 Nest.js 应用程序的实例。

NestFactory 类是从 @nestjs/core 模块导入的。 NestFactory 类用于创建 Nest.js 应用程序实例。

NestFactory 类将 AppModule 类作为参数。 AppModule 类用于配置 Nest.js 应用程序。

NestFactory 类返回 Nest.js 应用程序的一个实例。

Nest.js 应用程序的实例用于启动 Nest.js 应用程序。

Nest.js 应用程序的实例是使用 start() 方法启动的。

start() 方法用于启动 Nest.js 应用程序。

start() 方法将端口号作为参数。端口号用于侦听 HTTP 请求。

start() 方法返回一个 Promise。当 Nest.js 应用程序启动时，Promise 被解析。

src/index.ts 文件是 TypeScript 编译器的入口点。 src/index.ts 文件用于编译 TypeScript 代码。

src/index.ts 文件导入 AppModule 类。 AppModule 类用于配置 Nest.js 应用程序。

src/index.ts 文件使用 tsconfig.json 文件来配置 TypeScript 编译器。

tsconfig.json 文件用于配置 TypeScript 编译器。

tsconfig.json 文件包含编译器选项。编译器选项用于配置 TypeScript 编译器。

tsconfig.json 文件用于将 TypeScript 代码编译成 JavaScript 代码。

使用 tsc 命令将 TypeScript 代码编译成 JavaScript 代码。

tsc 命令用于将 TypeScript 代码编译成 JavaScript 代码。

tsc 命令将 tsconfig.json 文件作为参数。 tsconfig.json 文件用于配置 TypeScript 编译器。

tsc 命令将 TypeScript 代码编译成 JavaScript 代码。

编译后的 JavaScript 代码放在 dist 目录中。

dist 目录包含已编译的 JavaScript 代码。

dist 目录是 TypeScript 编译器的输出目录。

Nest.js 应用程序使用 node 命令运行。

node 命令用于运行 Nest.js 应用程序。

node 命令将编译后的 JavaScript 代码作为参数。编译后的 JavaScript 代码放在 dist 目录中。

node 命令运行 Nest.js 应用程序。

Nest.js 应用程序在 Node.js 服务器上运行。

Node.js 服务器用于运行 Nest.js 应用程序。

Node.js 服务器是一个 JavaScript 运行时。

Node.js 服务器用于执行 JavaScript 代码。

使用网络浏览器访问 Nest.js 应用程序。

Web 浏览器用于访问 Nest.js 应用程序。

Web 浏览器用于向 Nest.js 应用程序发送 HTTP 请求。

Nest.js 应用程序可通过 http://localhost:3000 访问。