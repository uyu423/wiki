---
title: 使用 TypeScript 和 Passport.js 进行用户身份验证
description: 
published: true
date: 2023-02-10T16:17:46.887Z
tags: 
editor: markdown
dateCreated: 2023-02-10T16:17:45.299Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Using TypeScript with Passport.js for User Authentication***English** document is available*](/en/Knowledge-base/TypeScript/using-typescript-with-passport-js-for-user-authentication)
{.links-list}


# 使用 TypeScript 和 Passport.js 进行用户身份验证

Passport.js 是一个灵活的 Node.js 身份验证中间件。它可用于使用各种策略对用户进行身份验证，包括用户名和密码、Facebook、Twitter 等。

TypeScript 是 JavaScript 的超集，增加了静态类型检查和其他功能。 TypeScript 广泛用于大型应用程序，它对模块、类和接口的支持使其成为与 Passport.js 一起工作的不错选择。

在本文中，我们将了解如何将 TypeScript 与 Passport.js 结合使用来构建用户身份验证系统。我们将从使用 TypeScript 和 Express.js 设置一个项目开始。然后我们将安装 Passport.js 并将其配置为与 TypeScript 一起使用。最后，我们将添加一些 TypeScript 代码来实现简单的用户名和密码身份验证策略。

## 设置 TypeScript 项目

首先，我们需要创建一个新的 TypeScript 项目。我们将使用 [Express.js](https://expressjs.com/) 网络框架和 [TypeScript Node Starter](https://github.com/Microsoft/TypeScript-Node-Starter) 项目模板。

首先，安装 TypeScript 编译器和 Express.js 框架。我们还需要一些其他模块：

```
npm install -g typescript
npm install express
npm install @types/express -D
```

接下来，使用 TypeScript Node Starter 模板创建一个新项目：

```
npx tsc --init
```

这将在您的项目中创建一个“tsconfig.json”文件。打开此文件并添加以下设置：

```json
{
    "compilerOptions": {
        "target": "es6",
        "module": "commonjs",
        "outDir": "dist",
        "strict": true
    }
}
```

这些设置会将我们的 TypeScript 代码编译为与 Express.js 兼容的 ES6 JavaScript。编译后的代码将输出到 dist 目录。

## 安装 Passport.js

现在我们已经设置了一个项目，我们可以安装 Passport.js。运行以下命令：

```
npm install passport
```

这将安装 Passport.js 模块并将其添加到 `package.json` 文件中。

## 配置 Passport.js

Passport.js 使用模块化方法，使用不同的“策略”来验证用户。有使用用户名和密码、Facebook、Twitter 等进行身份验证的策略。在本文中，我们将重点关注用户名和密码身份验证策略。

要使用 Passport.js 策略，我们需要安装相应的模块。对于用户名和密码策略，我们将使用 [passport-local](https://github.com/jaredhanson/passport-local) 模块。运行以下命令来安装它：

```
npm install passport-local
```

安装模块后，我们需要配置 Passport.js 以使用它。我们将在 `app.ts` 文件中执行此操作。首先，我们需要导入 `passport-local` 模块：

```javascript
import passportLocal from "passport-local";
```

接下来，我们需要配置 Passport.js 以使用 `passport-local` 策略。我们将在 `configurePassport` 函数中执行此操作：

```javascript
function configurePassport(passport: passport.Passport) {
    passport.use(new passportLocal.Strategy());
}
```

这会将 Passport.js 配置为使用“passport-local”策略。 `passport-local` 策略使用用户名和密码对用户进行身份验证。

## 实现身份验证

现在我们已经配置了 Passport.js，我们可以开始实现身份验证了。我们将在 `app.ts` 文件中执行此操作。

首先，我们需要导入 `passport-local` 模块：

```javascript
import passportLocal from "passport-local";
```

接下来，我们需要配置 Passport.js 以使用 `passport-local` 策略。我们将在 `configurePassport` 函数中执行此操作：

```javascript
function configurePassport(passport: passport.Passport) {
    passport.use(new passportLocal.Strategy());
}
```

这会将 Passport.js 配置为使用“passport-local”策略。 `passport-local` 策略使用用户名和密码对用户进行身份验证。

一旦我们配置了 Passport.js，我们就可以编写代码来验证用户。我们将在 `login` 函数中执行此操作：

```javascript
async function login(req: express.Request, res: express.Response) {
    passport.authenticate("local", (err, user, info) => {
        if (err) {
            // Handle errors
        }

        if (!user) {
            // Redirect to login page
        }

        // Login successful, redirect to home page
    })(req, res);
}
```

此代码使用“passport-local”策略对用户进行身份验证。如果身份验证成功，用户将被重定向到主页。否则，他们将被重定向到登录页面。

## 外部资源

- [Passport.js 文档](http://passportjs.org/docs)
- [护照本地文档](https://github.com/jaredhanson/passport-local)
- [TypeScript 文档](https://www.typescriptlang.org/docs/handbook/basic-types.html)