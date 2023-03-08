---
title: Kotlin 和 Express.js：使用 Node.js 框架构建 Web 应用程序
description: 
published: true
date: 2023-02-05T12:55:28.085Z
tags: 
editor: markdown
dateCreated: 2023-02-05T12:55:22.666Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kotlin and Express.js: Building a Web Application with a Node.js Framework***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-express-js-building-a-web-application-with-a-node-js-framework)
{.links-list}


# Kotlin 和 Express.js：使用 Node.js 框架构建 Web 应用程序

Kotlin 是一种 JVM 语言，可用于使用各种框架构建 Web 应用程序。在本文中，我们将重点介绍如何将 Kotlin 与 Express.js 框架结合使用。 Express.js 是一个 Node.js 框架，它提供了一组用于创建 Web 应用程序的工具。也可以将 Kotlin 与其他 Node.js 框架一起使用，例如 Hapi.js 和 Koa.js。

## 设置项目

首先，我们需要使用 Express.js 框架创建一个新的 Kotlin 项目。我们可以使用 express-generator 工具来做到这一点。

首先，我们需要使用 npm 安装该工具：

```
npm install -g express-generator
```

接下来，我们就可以使用该工具生成一个新的工程了：

```
express --view=pug my-app
```

这将在配置 Pug 模板引擎的 my-app 目录中创建一个新项目。

## 运行应用程序

现在我们有了一个新项目，我们可以通过在项目目录中运行以下命令来启动应用程序：

```
npm start
```

这将在 http://localhost:3000 上启动应用程序。我们可以在浏览器中访问该应用程序，我们应该会看到默认的 Express.js 欢迎页面。

## 你好世界

让我们开始创建一个简单的“Hello world”路由。我们可以通过编辑 routes/index.js 文件来做到这一点。

首先，我们需要导入 Express.js 路由器：

```javascript
var express = require('express');
var router = express.Router();
```

接下来，我们可以为“/”路径添加一个新路由：

```javascript
router.get('/', function(req, res, next) {
  res.send('Hello world');
});
```

当我们在浏览器中访问“/”路径时，此路由将呈现“Hello world”字符串。

## 结论

在本文中，我们了解了如何使用 Kotlin 和 Express.js 框架构建 Web 应用程序。我们还看到了如何创建路由和渲染模板。

有关 Kotlin 和 Web 开发的更多信息，请参阅以下资源：

- [用于服务器端开发的 Kotlin](https://kotlinlang.org/docs/reference/server-overview.html)
- [使用 Kotlin、Spring Boot 和 MongoDB 构建 Web 应用程序](https://www.baeldung.com/kotlin-mongodb-spring-boot)
- [全栈 Kotlin：使用 React 和 Spring Boot 开发 Web 应用程序](https://www.baeldung.com/kotlin-react-spring-boot)