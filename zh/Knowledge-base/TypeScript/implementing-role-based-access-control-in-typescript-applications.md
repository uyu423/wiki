---
title: 在 TypeScript 应用程序中实现基于角色的访问控制
description: 
published: true
date: 2023-02-01T08:05:50.332Z
tags: 
editor: markdown
dateCreated: 2023-02-01T08:05:46.879Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Implementing Role-Based Access Control in TypeScript Applications***English** version of this document is available*](/en/Knowledge-base/TypeScript/implementing-role-based-access-control-in-typescript-applications)
{.links-list}


  在 TypeScript 应用程序中实现基于角色的访问控制

基于角色的访问控制 (RBAC) 是应用程序中常用的权限模型。在 RBAC 中，每个用户都被分配了一个或多个角色，每个角色都有一组权限。该模型灵活且可扩展，可用于为不同用户提供对应用程序不同部分的不同级别的访问。

在本文中，我们将展示如何使用 node-acl 包在 TypeScript 应用程序中实现 RBAC。我们将首先创建一个具有两个用户和两个角色的简单应用程序。然后我们将 RBAC 添加到应用程序，并使用它来根据用户的角色限制对应用程序某些部分的访问。

## 应用程序

我们将从创建一个具有两个用户和两个角色的简单 TypeScript 应用程序开始。为简单起见，用户和角色将在应用程序中进行硬编码。在实际应用程序中，您可能会将此信息存储在数据库中。

该应用程序将有两个页面：主页和个人资料页面。所有用户都可以访问主页，但只有登录的用户才能访问个人资料页面。

主页将如下所示：

![首页](https://i.imgur.com/P0jrQbu.png)

个人资料页面将如下所示：

![简介页面](https://i.imgur.com/TK7gNcu.png)

用户将能够使用主页上的登录表单登录和退出应用程序。当用户登录时，他们的用户名将显示在个人资料页面上。

为了将重点放在 RBAC 上，我们不会在本文中实现完整的身份验证系统。相反，我们将在用户登录时简单地设置一个会话变量。在实际应用程序中，您可能希望使用更安全的身份验证方法，例如 JSON Web Tokens。

此 [GitHub 存储库](https://github.com/auth0-blog/typescript-rbac-app) 中提供了该应用程序的代码。

## 设置项目

在开始实施 RBAC 之前，我们需要设置项目。首先，我们需要创建一个新的 TypeScript 项目。我们可以使用 TypeScript 网站上的 [TypeScript 模板](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes.html) 来完成此操作。

创建项目后，我们需要安装项目所需的依赖项。在这种情况下，我们需要 [Express](https://expressjs.com/) web 框架和 [node-acl](https://www.npmjs.com/package/node-acl) 包来实现 RBAC .我们可以使用 npm 安装这些依赖项：

```
npm install express node-acl --save
```

我们还需要安装 [TypeScript](https://www.typescriptlang.org/) 编译器和 [Webpack](https://webpack.js.org/) 模块打包器。我们也可以使用 npm 安装这些依赖项：

```
npm install typescript webpack webpack-cli --save-dev
```

## 实施 RBAC

现在我们已经设置了项目，我们可以开始实施 RBAC。我们将从在 `src` 目录中创建一个名为 `acl.ts` 的新文件开始。该文件将包含用于设置和使用 node-acl 包的代码。

首先，我们需要导入 node-acl 包和 Express Request 和 Response 接口。我们还将导入 node-acl MemoryBackend，我们将使用它来将 ACL 数据存储在内存中：

```typescript
import * as acl from 'acl';
import { Request, Response } from 'express';
import { MemoryBackend } from 'acl';
```

接下来，我们需要创建一个新的 node-acl MemoryBackend 实例。我们还将创建 node-acl acl 类的新实例，我们将使用它来创建和管理 ACL：

```typescript
const backend = new MemoryBackend();
const acl = new acl(backend);
```

现在我们已经设置了后端和 acl 实例，我们可以开始为我们的应用程序创建角色和权限。

我们将从创建两个角色开始：`user` 和 `admin`。 `user` 角色将拥有 `view` 权限，允许用户查看主页。 `admin` 角色将拥有 `view` 和 `edit` 权限，这将允许管理员查看和编辑个人资料页面：

```typescript
acl.allow([
  {
    roles: ['user'],
    allows: [
      { resources: '/', permissions: 'view' }
    ]
  },
  {
    roles: ['admin'],
    allows: [
      { resources: '/', permissions: 'view' },
      { resources: '/profile', permissions: 'edit' }
    ]
  }
]);
```

我们还需要创建一个“访客”角色。此角色没有任何权限，这将阻止来宾访问应用程序的任何部分：

```typescript
acl.addRoleParents('guest', []);
```

现在我们已经设置了角色和权限，我们需要创建一个中间件函数来检查 ACL 以查看用户是否具有访问特定资源的权限。

首先，我们需要导入 Express Request 和 Response 接口。我们还将导入 node-acl acl 类：

```typescript
import { Request, Response } from 'express';
import { acl } from 'acl';
```

接下来，我们将创建一个名为“checkPermission”的新中间件函数：

```typescript
function checkPermission(resource: string, action: string) {
  return (req: Request, res: Response, next: Function) => {
    acl.isAllowed(req.session.user, resource, action, (err: Error, allowed: boolean) => {
      if (err) {
        next(err);
      } else if (allowed) {
        next();
      } else {
        res.status(403).send('Forbidden');
      }
    });
  };
}
```

这个中间件函数有两个参数：用户试图访问的资源和他们试图对该资源执行的操作。 acl 实例的 isAllowed 方法用于检查用户是否具有访问资源的权限。如果用户没有权限，则返回“403”状态码。

## 将 RBAC 添加到应用程序

现在我们已经设置了中间件功能，我们可以将它添加到我们的应用程序中。

首先，我们需要导入 `express` 和 `body-parser` 包。我们还将导入在上一节中创建的 ./acl 文件：

```typescript
import * as express from 'express';
import * as bodyParser from 'body-parser';
import * as acl from './acl';
```

接下来，我们将创建一个新的 Express 应用程序并将其配置为使用“body-parser”中间件：

```typescript
const app = express();
app.use(bodyParser.json());
```

现在，我们可以开始添加我们的路线了。

我们要添加的第一个路由是 `GET /` 路由。此路由将呈现应用程序的主页：

```typescript
app.get('/', (req: Request, res: Response) => {
  res.send(`
    <html>
      <head>
        <title>Home</title>
      </head>
      <body>
        <h1>Home</h1>
        ${req.session.user ? `<p>Welcome, ${req.session.user}!</p>` : ''}
        <a href="/profile">Profile</a>
      </body>
    </html>
  `);
});
```

接下来，我们将添加 `GET /profile` 路由。此路由将呈现应用程序的配置文件页面：

```typescript
app.get('/profile', checkPermission('/profile', 'view'), (req: Request, res: Response) => {
  res.send(`
    <html>
      <head>
        <title>Profile</title>
      </head>
      <body>
        <h1>Profile</h1>
        <p>Welcome, ${req.session.user}!</p>
        <a href="/">Home</a>
      </body>
    </html>
  `);
});
```

请注意，我们已将 `checkPermission` 中间件功能添加到此路由。这将确保只有具有 `view` 权限的用户才能访问此路由。

最后，我们将添加 `POST /login` 路由。此路由将用于登录和注销应用程序的用户：

```typescript
app.post('/login', (req: Request, res: Response) => {
  const { user } = req.body;
  req.session.user = user;
  res.redirect('/');
});
```

此路由会将会话对象的“用户”属性设置为在请求正文中传递的用户名。

## 测试应用程序

现在我们已经设置了应用程序，我们可以测试它以查看 RBAC 是否按预期工作。

首先，我们需要构建应用程序。我们可以使用 `webpack` 命令来做到这一点：

```
webpack
```

接下来，我们需要启动应用程序。我们可以使用 `node` 命令来做到这一点：

```
node ./dist/bundle.js
```

现在，我们可以在 Web 浏览器中打开应用程序并对其进行测试。

如果我们尝试在不登录的情况下访问 `/profile` 路由，我们应该会看到以下错误消息：

![错误信息](https://i.imgur.com/vALDKd7.png)

这是预期的行为，因为我们没有为 `guest` 角色授予 `/profile` 路由的 `view` 权限。

如果我们以 `user` 角色登录，我们应该能够访问主页，但我们不应该能够访问个人资料页面：

![首页](https://i.imgur.com/P0jrQbu.png)

![简介页面](https://i.imgur.com/TK7gNcu.png)

这是预期的行为，因为我们只为 `user` 角色授予了 `/` 路由的 `view` 权限。

如果我们以“admin”角色登录，我们应该能够访问主页和个人资料页面：

![首页](https://i.imgur.com/P0jrQbu.png)

![简介页面](https://i.imgur.com/TK7gNcu.png)

这是预期的行为，因为我们已经为 admin 角色授予了 `/` 和 `/profile` 路由的 `view` 和 `edit` 权限。

## 结论

在本文中，我们展示了如何使用 node-acl 包在 TypeScript 应用程序中实现 RBAC。我们创建了一个具有两个用户和两个角色的简单应用程序。然后我们将 RBAC 添加到应用程序，并使用它来根据用户的角色限制对应用程序某些部分的访问。

如果您想了解有关 RBAC 的更多信息，我们推荐以下资源：

- [基于角色的访问控制](https://en.wikipedia.org/wiki/Role-based_access_control) 在维基百科上
- [node-acl 文档](https://github.com/OptimalBits/node-acl)
- [Express 文档](https://expressjs.com/en/guide/rbac.html)