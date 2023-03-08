---
title: 023: 在 Nest.js 中使用模板
description: 
published: true
date: 2023-02-15T04:32:33.213Z
tags: 
editor: markdown
dateCreated: 2023-02-15T04:32:31.160Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [023: Using templates with Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/023-using-templates-with-nest-js)
{.links-list}


## 介绍

Nest.js 是一个用于构建可扩展的服务器端应用程序的 Node.js 框架。它使用 TypeScript，这是一种为大规模开发提供静态类型检查和强大工具的语言。

Nest.js 应用程序是使用模块化方法构建的，它允许开发人员将他们的代码分解成更小的片段，这些片段可以在整个应用程序中重复使用。 Nest.js 带有一个内置的依赖注入系统，可以很容易地将服务和其他依赖注入到组件中。

Nest.js 最强大的功能之一是它对模板的使用。 Nest.js 模板基于流行的 AngularJS 模板系统，它们提供了一种模块化 HTML 并减少必须编写的代码量的方法。

在这篇文章中，我们将看看如何在 Nest.js 中使用模板。我们将从创建一个简单的 Nest.js 应用程序开始，然后我们将向其添加一个模板。最后，我们将学习如何使用模板呈现数据库中的数据。

## 创建 Nest.js 应用程序

让我们从创建一个新的 Nest.js 应用程序开始。我们将使用 Nest.js CLI 生成一个新的应用程序。首先，确保安装了 Nest.js CLI。如果你没有安装它，你可以使用 npm 安装它：

```
npm install -g @nestjs/cli
```

一旦安装了 Nest.js CLI，我们就可以使用它来生成一个新的应用程序。我们将我们的应用程序称为“模板应用程序”：

```
nest new template-app
```

这将创建一个名为“template-app”的新目录，并生成基本 Nest.js 应用程序所需的文件。

## 添加模板

现在我们有了一个基本的 Nest.js 应用程序，让我们向它添加一个模板。 Nest.js 带有一个名为 Nest.js View 的内置模板引擎。 Nest.js View 基于流行的 AngularJS 模板引擎，它提供了一种模块化 HTML 并减少必须编写的代码量的方法。

要将模板添加到我们的 Nest.js 应用程序，我们需要在“src/views”目录中创建一个名为“template.html”的新文件。 “src/views”目录是 Nest.js 寻找模板的地方。

在我们的“template.html”文件中，我们将添加一个简单的 HTML 模板：

```html
<html>
  <head>
    <title>Template App</title>
  </head>
  <body>
    <h1>Hello, World!</h1>
  </body>
</html>
```

现在我们有了模板，让我们在 Nest.js 应用程序中使用它。

## 使用模板

要使用我们的模板，我们需要告诉 Nest.js 在哪里可以找到它。我们可以通过向“src/main.ts”文件中的“view”对象添加一个“template”属性来做到这一点：

```javascript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  app.setViewEngine({
    type: 'html',
    template: './src/views/template.html',
  });

  await app.listen(3000);
}
bootstrap();
```

“模板”属性告诉 Nest.js 在哪里可以找到我们的模板文件。在这种情况下，我们告诉 Nest.js 在“src/views”目录中查找“template.html”文件。

现在我们已经告诉 Nest.js 在哪里可以找到我们的模板，我们可以使用它来呈现数据。

## 渲染数据

要在我们的模板中呈现数据，我们需要使用“render”函数。 “渲染”函数有两个参数：一个数据对象和一个响应对象。 data 对象包含我们要呈现的数据，response 对象用于将呈现的 HTML 发送给客户端。

让我们看一个例子。在这个例子中，我们将在我们的模板中呈现一个用户列表：

```javascript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  app.setViewEngine({
    type: 'html',
    template: './src/views/template.html',
  });

  app.get('/users', (req, res) => {
    const users = [
      {
        name: 'John Doe',
        age: 30,
      },
      {
        name: 'Jane Doe',
        age: 31,
      },
    ];

    res.render('users', { users });
  });

  await app.listen(3000);
}
bootstrap();
```

在此示例中，我们向 Nest.js 应用程序添加了一条新路由，用于呈现用户列表。我们正在使用“render”函数来呈现“users”模板并传入包含用户列表的数据对象。

现在我们已经了解了如何在 Nest.js 模板中呈现数据，让我们来看看如何访问我们模板中的数据。

## 访问模板中的数据

要访问模板中的数据，我们使用“render”函数的“data”参数。 “数据”参数是一个包含我们要呈现的数据的对象。

在我们的“template.html”文件中，我们可以访问使用“render”函数传入的数据，如下所示：

```html
<html>
  <head>
    <title>Template App</title>
  </head>
  <body>
    <h1>Users</h1>
    <ul>
      <li>
        {{ users[0].name }} - {{ users[0].age }}
      </li>
      <li>
        {{ users[1].name }} - {{ users[1].age }}
      </li>
    </ul>
  </body>
</html>
```

在此示例中，我们使用“render”函数的“data”参数来访问我们传入的用户列表。然后我们遍历用户列表并呈现他们的姓名和年龄。

现在我们已经了解了如何在 Nest.js 中使用模板，让我们看看一些资源以进一步阅读。

## 进一步阅读的资源

- [Nest.js 视图](https://docs.nestjs.com/v/6/view)
- [AngularJS](https://angularjs.org/)
- [把手](https://handlebarsjs.com/)