---
title: 011: 在 Nest.js 中实现身份验证
description: 
published: true
date: 2023-02-14T21:32:53.955Z
tags: 
editor: markdown
dateCreated: 2023-02-14T21:32:46.276Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [011: Implementing authentication in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/011-implementing-authentication-in-nest-js)
{.links-list}


# 在 Nest.js 中实现身份验证

Nest.js 是用于构建 Node.js 应用程序的框架。它使用 TypeScript 并受到 Angular 的影响。 Nest.js 提供了一种构建易于使用和维护的代码的方法。

身份验证是验证用户身份的过程。 Nest.js 提供了一种在应用程序中实现身份验证的方法。在这篇文章中，我们将学习如何在 Nest.js 应用程序中实现身份验证。

## 什么是认证？

身份验证是验证用户身份的过程。它用于保护资源免受未经授权的访问。身份验证通常通过要求用户提供用户名和密码来完成。然后根据授权用户的数据库验证用户名和密码。

## 什么是 Nest.js？

Nest.js 是用于构建 Node.js 应用程序的框架。它使用 TypeScript 并受到 Angular 的影响。 Nest.js 提供了一种构建易于使用和维护的代码的方法。

## 使用 Nest.js 有什么好处？

使用 Nest.js 有很多好处，其中一些是：

- Nest.js 提供了一种构建易于使用和维护的代码的方法。
- Nest.js 易于学习和使用。
- Nest.js 基于 TypeScript，它是 JavaScript 的超集。这意味着 Nest.js 代码更易于阅读和理解。
- Nest.js 受 Angular 的影响。这意味着对于熟悉 Angular 的人来说，Nest.js 代码很容易阅读和理解。

## 什么是打字稿？

TypeScript 是 JavaScript 的超集。这意味着 TypeScript 代码更易于阅读和理解。 TypeScript 也是类型化的，这意味着它可以在编译时捕获错误。这使得 TypeScript 代码更加可靠。

## JavaScript 和 TypeScript 有什么区别？

JavaScript 和 TypeScript 的区别在于 TypeScript 是类型化的，而 JavaScript 不是。这意味着 TypeScript 可以在编译时捕获错误。这使得 TypeScript 代码更加可靠。

## Node.js 和 Nest.js 有什么区别？

Node.js 和 Nest.js 之间的区别在于 Nest.js 构建在 Node.js 之上。 Nest.js 提供了一种构建易于使用和维护的代码的方法。

## 如何安装 Nest.js？

Nest.js 可以使用 Node.js 包管理器 (npm) 安装。要安装 Nest.js，请打开终端并运行以下命令：

```
npm install -g @nestjs/cli
```

## 如何创建 Nest.js 项目？

要创建 Nest.js 项目，请打开终端并运行以下命令：

```
nest new project-name
```

将 project-name 替换为您的项目名称。这将创建一个名为 project-name 的新 Nest.js 项目。

## 如何运行 Nest.js 项目？

要运行 Nest.js 项目，请打开终端并导航到项目目录。然后，运行以下命令：

```
nest start
```

这将启动 Nest.js 服务器。该服务器可通过 http://localhost:3000 访问。

## 在Nest.js 中实现身份验证的步骤是什么？

在 Nest.js 中有很多方法可以实现身份验证。在这篇文章中，我们将使用 Passport.js 库来实现身份验证。 Passport.js 是一个流行的 Node.js 身份验证库。

在 Nest.js 中实现身份验证的步骤是：

1. 安装 Passport.js 库。
2. 配置 Passport.js。
3. 创建登录页面。
4. 创建注销页面。
5. 通过身份验证保护资源。

## 第 1 步：安装 Passport.js 库

第一步是安装 Passport.js 库。 Passport.js 是一个流行的 Node.js 身份验证库。要安装 Passport.js 库，请打开终端并运行以下命令：

```
npm install passport
```

## 第 2 步：配置 Passport.js

下一步是配置 Passport.js。 Passport.js 需要知道如何验证用户的身份。这是通过提供策略来完成的。有许多策略可用于 Passport.js。在这篇文章中，我们将使用 LocalStrategy。

LocalStrategy 是一种使用用户名和密码来验证用户身份的策略。要使用 LocalStrategy，我们需要提供一个回调函数。当 Passport.js 需要验证用户身份时，将调用此回调函数。

LocalStrategy 回调函数具有以下签名：

```
function(username, password, done) {

}
```

用户名和密码参数是用户提供的用户名和密码。 done 回调是一个用于返回验证结果的函数。 done 回调具有以下签名：

```
function(error, user, info) {

}
```

如果验证成功，用户参数将包含用户对象。如果验证不成功，error 和 info 参数将包含有关错误的信息。

要配置 LocalStrategy，我们需要在项目根目录中创建一个名为 passport.js 的文件。 passport.js 文件应如下所示：

```javascript
const passport = require('passport');
const LocalStrategy = require('passport-local').Strategy;

passport.use(new LocalStrategy(
  function(username, password, done) {
    //Verify the username and password here
  }
));
```

将 //Verify the username and password here 注释替换为验证用户名和密码的代码。

## 第三步：创建登录页面

下一步是创建登录页面。登录页面将是一个包含表单的 HTML 页面。该表单将包含用户名和密码字段。表单将提交到 /login 路由。

要创建登录页面，请在项目根目录中创建一个名为 login.html 的文件。 login.html 文件应如下所示：

```html
<html>
<body>
  <form action="/login" method="post">
    <label>Username:</label>
    <input type="text" name="username">
    <label>Password:</label>
    <input type="password" name="password">
    <input type="submit" value="Login">
  </form>
</body>
</html>
```

## 第 4 步：创建注销页面

下一步是创建注销页面。注销页面将是一个包含表单的 HTML 页面。该表单将有一个用户名字段。表单将提交到 /logout 路由。

要创建注销页面，请在项目根目录中创建一个名为 logout.html 的文件。 logout.html 文件应如下所示：

```html
<html>
<body>
  <form action="/logout" method="post">
    <label>Username:</label>
    <input type="text" name="username">
    <input type="submit" value="Logout">
  </form>
</body>
</html>
```

## 第 5 步：使用身份验证保护资源

最后一步是通过身份验证保护资源。为此，我们需要创建一个中间件函数来检查用户是否已通过身份验证。如果用户未通过身份验证，中间件功能会将用户重定向到登录页面。

要创建中间件功能，请在项目根目录中创建一个名为 auth.js 的文件。 auth.js 文件应如下所示：

```javascript
const passport = require('passport');

function isAuthenticated(req, res, next) {
  if (req.isAuthenticated()) {
    return next();
  }
  res.redirect('/login');
}

module.exports = {
  isAuthenticated: isAuthenticated
};
```

isAuthenticated() 函数是中间件函数。该函数检查用户是否已通过身份验证。如果用户未通过身份验证，该函数会将用户重定向到 /login 页面。

中间件功能可用于保护任何路由。例如，要保护 /admin 路由，我们可以使用以下代码：

```javascript
app.get('/admin', auth.isAuthenticated, (req, res) => {
  // The authenticated user can access this route
});
```

## 结论

在这篇文章中，我们学习了如何在 Nest.js 应用程序中实现身份验证。我们安装了 Passport.js 库并将其配置为使用 LocalStrategy。我们还创建了一个登录页面和一个注销页面。最后，我们通过身份验证保护资源。