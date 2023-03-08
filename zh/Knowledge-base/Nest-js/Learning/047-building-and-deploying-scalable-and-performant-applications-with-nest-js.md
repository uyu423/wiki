---
title: 047：使用 Nest.js 构建和部署可扩展的高性能应用程序
description: 
published: true
date: 2023-02-15T17:32:53.924Z
tags: 
editor: markdown
dateCreated: 2023-02-15T17:32:52.147Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [047: Building and deploying scalable and performant applications with Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/047-building-and-deploying-scalable-and-performant-applications-with-nest-js)
{.links-list}


# Nest.js

Nest.js 是一个用于使用 Node.js 构建可扩展和高性能应用程序的框架。它受到 Angular 的启发，并提供了一组强大的工具来创建服务器端应用程序。在这篇文章中，我们将了解如何开始使用 Nest.js 以及如何使用它构建和部署可扩展的高性能应用程序。

## 入门

要开始使用 Nest.js，您需要安装 Nest.js CLI。你可以用 npm 做到这一点：

```
npm install -g @nestjs/cli
```

安装 Nest.js CLI 后，您可以使用以下命令创建一个新的 Nest.js 项目：

```
nest new my-project
```

这将创建一个名为 ```my-project``` 的新目录，其中包含基本的 Nest.js 项目结构。

## 项目结构

Nest.js 项目具有以下基本结构：

```
my-project
├── src
│   ├── app.controller.ts
│   ├── app.module.ts
│   ├── app.service.ts
│   ├── main.ts
│   └── ...
├── test
│   ├── app.controller.spec.ts
│   ├── app.service.spec.ts
│   └── ...
├── .gitignore
├── nest-cli.json
├── package-lock.json
└── package.json
```

```javascript
@Controller('hello')
export class HelloController {

  @Get()
  hello() {
    return 'Hello, world!';
  }

}
```test``` 目录包含应用程序的单元测试。 ```app.controller.spec.ts``` 文件包含控制器的单元测试。 ```app.service.spec.ts``` 文件包含服务的单元测试。

```javascript
@Injectable()
export class HelloService {

  generateGreeting(name: string) {
    return `Hello, ${name}!`;
  }

}
```nest-cli.json``` 文件包含 Nest.js CLI 的配置。

```javascript
@Module({
  controllers: [HelloController],
  providers: [HelloService],
})
export class HelloModule {}
```package.json``` 文件包含项目的元数据。

## 编写代码

现在你对项目结构有了基本的了解，让我们来看看如何在 Nest.js 中编写代码。

### 控制器

控制器负责处理传入的 HTTP 请求和返回响应。在 Nest.js 中，控制器是使用 ```@Controller()``` 装饰器定义的。

下面是一个处理 GET 请求到 ```/hello``` 路由的示例控制器：

```
nest build
```

在这个例子中，```@Controller('hello')``` 装饰器定义了名为```hello``` 的控制器。 ```@Get()``` 装饰器定义了 GET 请求的处理程序。 ```hello()``` 方法是返回字符串```Hello, world!``` 的处理函数。

### 服务

服务是负责封装业务逻辑的单例。在 Nest.js 中，服务是使用 ```@Injectable()``` 装饰器定义的。

下面是一个示例服务，它具有生成问候语的方法：

```
web: nest start
```

在此示例中，```@Injectable()``` 装饰器将服务定义为可注入的。 ```generateGreeting()``` 方法接受一个 ```name``` 参数并返回一个问候字符串。

### 模块

模块用于组织 Nest.js 中的相关功能。在 Nest.js 中，模块是使用 ```@Module()``` 装饰器定义的。

这是一个定义控制器和服务的示例模块：

```
git push heroku master
```

在此示例中，```@Module()``` 装饰器使用```HelloController``` 和```HelloService``` 定义模块。

## 构建和部署

现在您已经了解了如何在 Nest.js 中编写代码，让我们来看看如何构建和部署 Nest.js 应用程序。

### 建筑

要构建 Nest.js 应用程序，您需要使用 Nest.js CLI。 Nest.js CLI 提供了一个 ```build``` 命令，可用于构建 Nest.js 应用程序。

要构建 Nest.js 应用程序，您需要运行以下命令：

```
筑巢
```

这将构建 Nest.js 应用程序并将编译后的文件输出到 ```dist``` 目录。

### 部署

要部署 Nest.js 应用程序，您需要使用 Node.js 托管提供商。有许多 Node.js 托管提供商可供选择，但我们建议使用 [Heroku](https://www.heroku.com/)。

Heroku 提供了一个免费层，您可以使用它来部署 Nest.js 应用程序。要将您的应用程序部署到 Heroku，您需要在项目的根目录中创建一个“Procfile”。 ```Procfile``` 用于告诉 Heroku 如何运行您的应用程序。

下面是一个 Nest.js 应用程序的例子```Procfile```：

```
网络：嵌套开始
```

在此示例中，```web``` 进程类型用于告诉 Heroku 这是一个 Web 应用程序。 ```nest start``` 命令用于启动 Nest.js 应用程序。

创建“Procfile”后，您可以使用以下命令将 Nest.js 应用程序部署到 Heroku：

```
git push heroku 大师
```

这会将您的代码推送到 Heroku 并触发新的部署。

## 结论

在这篇文章中，我们了解了如何开始使用 Nest.js 以及如何使用它构建和部署可扩展的高性能应用程序。 Nest.js 是一个用于构建服务器端应用程序的强大框架，我们希望这篇文章能给您一个很好的介绍。