---
title: Kotlin 和 TypeScript：使用 JavaScript 框架构建 Web 应用程序
description: 
published: true
date: 2023-02-17T18:16:47.297Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:36:33.228Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Kotlin and TypeScript: Building a Web Application with a JavaScript Framework***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-typescript-building-a-web-application-with-a-javascript-framework)
{.links-list}


Kotlin 和 TypeScript 是两种流行的编程语言，可以一起使用来构建 Web 应用程序。在本文中，我们将了解如何使用 Kotlin 和 TypeScript 构建带有 JavaScript 框架的 Web 应用程序。

我们将从了解结合使用 Kotlin 和 TypeScript 的一些好处开始。 Kotlin 是一种在 Java 虚拟机上运行的静态类型语言。它以其安全性、互操作性和工具支持而闻名。 TypeScript 是 JavaScript 的超集，增加了静态类型和其他功能。它以其工具支持和扩展能力而闻名。

结合使用 Kotlin 和 TypeScript 可以让您获得两种语言的优势。您可以获得 Kotlin 的安全和工具支持，以及 TypeScript 的扩展能力。

接下来，我们将了解如何使用 Kotlin 和 TypeScript 设置项目。我们将创建一个简单的“Hello, World!” Web应用程序。

首先，我们需要创建一个项目目录。我们可以使用命令行或 IDE 来完成此操作。

接下来，我们将在我们的项目目录中创建一个名为“Hello.kt”的文件。我们将以下代码添加到我们的文件中：

```kotlin
fun main(args: Array<String>) {
    println("Hello, World!")
}
```

然后我们可以使用命令行编译我们的 Kotlin 代码：

```
kotlinc Hello.kt -d hello.js
```

这将在我们的项目目录中生成一个名为“hello.js”的文件。

现在，我们可以在我们的项目目录中创建一个名为“index.html”的文件。我们将以下代码添加到我们的文件中：

```html
<!doctype html>
<html>

<head>
    <meta charset="utf-8">
    <title>Hello, World!</title>
</head>

<body>
    <script src="hello.js"></script>
</body>

</html>
```

最后，我们可以在浏览器中打开“index.html”，我们应该会看到我们的“Hello, World!”信息。

现在我们已经了解了如何使用 Kotlin 和 TypeScript 设置项目，让我们看看如何将 Kotlin 和 TypeScript 与 JavaScript 框架结合使用。我们将使用 React JavaScript 框架。

首先，我们需要安装 React 和 React-DOM。我们可以使用命令行来做到这一点：

```
npm install react react-dom
```

接下来，我们将在我们的项目目录中创建一个名为“Hello.tsx”的文件。我们将以下代码添加到我们的文件中：

```typescript
import * as React from "react";
import * as ReactDOM from "react-dom";

ReactDOM.render(
    <h1>Hello, World!</h1>,
    document.getElementById("root")
);
```

然后，我们将使用命令行编译我们的 TypeScript 代码：

```
tsc --jsx react Hello.tsx
```

这将在我们的项目目录中生成一个名为“Hello.js”的文件。

最后，我们需要更新我们的“index.html”文件以包含我们的 React 代码。我们将以下代码添加到我们的文件中：

```html
<!doctype html>
<html>

<head>
    <meta charset="utf-8">
    <title>Hello, World!</title>
</head>

<body>
    <div id="root"></div>
    <script src="hello.js"></script>
</body>

</html>
```

然后我们可以在浏览器中打开“index.html”，我们应该会看到我们的“Hello, World!”信息。

Kotlin 和 TypeScript 是两种流行的编程语言，可以一起使用来构建 Web 应用程序。在本文中，我们了解了如何使用 Kotlin 和 TypeScript 构建带有 JavaScript 框架的 Web 应用程序。