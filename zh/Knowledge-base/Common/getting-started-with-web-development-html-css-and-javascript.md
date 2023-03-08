---
title: Web 开发入门：HTML、CSS 和 JavaScript
description: 
published: true
date: 2023-02-15T19:56:07.821Z
tags: 
editor: markdown
dateCreated: 2023-02-15T19:55:59.770Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Getting Started with Web Development: HTML, CSS, and JavaScript***English** document is available*](/en/Knowledge-base/Common/getting-started-with-web-development-html-css-and-javascript)
{.links-list}


# Web 开发入门：HTML、CSS 和 JavaScript

互联网已经成为我们生活中不可或缺的一部分。我们用它来做任何事，从与朋友和家人保持联系到支付账单和购买杂货。自 1989 年首次发明以来，万维网已经取得了长足的进步，现在几乎可以在网上做任何事情。

如果您曾经想创建自己的网站或 Web 应用程序，那么您很幸运。只需一点点专业知识，您就可以立即启动并运行。在本文中，我们将带您了解 Web 开发的基础知识，从选择开发环境到编写第一行代码。到最后，您将拥有开始自己的项目所需的所有信息。

## 什么是网络开发？

Web 开发是创建和维护网站的过程。它涵盖了从从头开始构建网站到向现有网站添加新功能的所有内容。

Web 开发是一个广义术语，可用于描述各种不同的角色，例如 Web 设计、Web 工程和 Web 内容管理。一般来说，Web 开发人员负责网站的编码、设计和布局。他们还可能参与 Web 应用程序的开发，这些应用程序是在 Web 服务器上运行并由用户通过 Web 浏览器访问的程序。

## 选择开发环境

Web开发入门的第一步是选择开发环境。这是您将用来编写代码和管理项目的软件。

有几个不同的选项可用，但我们建议使用 [Visual Studio Code](https://code.visualstudio.com/)。它是来自 Microsoft 的免费开源代码编辑器，适用于 Windows、macOS 和 Linux。它对多种编程语言具有出色的支持，包括 HTML、CSS 和 JavaScript。

下载并安装 Visual Studio Code 后，您就可以开始编码了。

## 编写你的第一行代码

下一步是编写您的第一行代码。为此，我们将使用简单的文本编辑器，如记事本或 TextEdit。

打开文本编辑器并输入以下内容：

```html
<!DOCTYPE html>
<html>
<head>
    <title>My first web page</title>
</head>
<body>
    <h1>Hello, world!</h1>
</body>
</html>
```

此代码创建一个带有标题和单个标头元素的基本网页。 `<!DOCTYPE html>` 声明告诉网络浏览器这是一个 HTML 文档。 `<html>`、`<head>` 和 `<body>` 元素是 HTML 页面的基本构建块。 `<head>` 元素包含有关页面的信息，例如标题，`<body>` 元素包含页面的内容。

`<h1>` 元素是标题元素，用于在页面上创建标题。在本例中，我们使用它来创建一个标题为“Hello, world!”的标题。

要保存文件，请从菜单中选择文件 > 另存为，然后从文件类型下拉菜单中选择 HTML。将文件命名为“index.html”并将其保存到您的计算机。

## 查看您的网页

现在您已经编写了第一行代码，是时候在网络浏览器中查看您的网页了。

为此，请在 Web 浏览器中打开您刚刚创建的 index.html 文件。如果您使用的是 Chrome，则可以通过从菜单中选择“文件”>“打开文件”来执行此操作。

你应该看到一个看起来像这样的页面：

![](https://i.imgur.com/JD7iK7I.png)

恭喜！您刚刚创建了第一个网页。

## 使用 CSS 添加样式

现在您已经创建了一个基本网页，是时候添加一些样式了。 CSS（层叠样式表）是一种用于设置 HTML 文档样式的语言。使用 CSS，您可以控制网页的颜色、字体和布局。

让我们从为我们的页面添加一点颜色开始。我们可以通过向页面添加 CSS 规则来做到这一点。

将以下代码添加到 HTML 文档的“<head>”元素中：

```css
<style>
    body {
        background-color: lightblue;
    }
</style>
```

此代码添加了一个 CSS 规则，将 `<body>` 元素的背景色设置为浅蓝色。

保存文件并在 Web 浏览器中刷新页面。您应该会看到如下所示的页面：

![](https://i.imgur.com/eAoR3zJ.png)

正如您所看到的，页面的背景现在是淡蓝色的。

## 使用 JavaScript 添加行为

CSS 用于设置 HTML 文档的样式，但它不会向页面添加任何行为。为此，我们需要使用 JavaScript。

JavaScript 是一种用于向网页添加交互性的编程语言。使用 JavaScript，您可以创建下拉菜单、表单验证和动画效果等内容。

让我们向页面添加一个简单的 JavaScript 函数。将以下代码添加到 HTML 文档的“<body>”元素中：

```javascript
<script>
    function sayHello() {
        alert("Hello, world!");
    }
</script>
```

这段代码定义了一个名为 sayHello() 的函数，它显示一个警告框，上面写着“Hello, world!”。

现在，我们需要向我们的页面添加一个元素，该元素将在单击时调用此函数。将以下代码添加到 HTML 文档的“<body>”元素中：

```html
<button onclick="sayHello()">Click me!</button>
```

此代码向页面添加一个按钮，单击该按钮将调用 `sayHello()` 函数。

保存文件并在 Web 浏览器中刷新页面。您应该会看到一个如下所示的按钮：

![](https://i.imgur.com/B6iU4TJ.png)

单击该按钮，您应该会看到一个如下所示的警告框：

![](https://i.imgur.com/cCk4Afe.png)

恭喜！您刚刚向网页添加了第一点交互性。

## 从这往哪儿走

现在您已经学习了 HTML、CSS 和 JavaScript 的基础知识，您可以开始创建自己的网页和 Web 应用程序了。如果您想了解更多信息，我们建议您查看下面的一些资源。

- [W3Schools](https://www.w3schools.com/) - 一个提供网络开发技术教程和参考的网站
- [Mozilla Developer Network](https://developer.mozilla.org/) - 一个提供 Web 开发技术教程和参考的网站
- [Code Academy](https://www.codecademy.com/) - 学习编码的在线互动平台