---
title: 使用 Next.js 设置 TypeScript 以进行服务器端渲染
description: 
published: true
date: 2023-02-14T13:55:32.497Z
tags: 
editor: markdown
dateCreated: 2023-02-14T13:55:30.715Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Setting Up TypeScript with Next.js for Server-Side Rendering***English** document is available*](/en/Knowledge-base/TypeScript/setting-up-typescript-with-next-js-for-server-side-rendering)
{.links-list}


# 使用 Next.js 设置 TypeScript 以进行服务器端渲染

TypeScript 是 JavaScript 的类型化超集，可编译为纯 JavaScript。它提供类、模块和接口来帮助您构建健壮的组件。并且它可以与 React 一起用于服务器端渲染 (SSR)。

在本文中，我们将向您展示如何使用 Next.js 设置 TypeScript。我们将介绍将 TypeScript 与 Next.js 结合使用的一些好处，并向您展示如何开始使用。

## 为什么在 Next.js 中使用 TypeScript？

将 TypeScript 与 Next.js 结合使用有几个好处。

TypeScript 可以帮助您尽早发现错误。这是因为 TypeScript 是一种类型化语言，这意味着您可以指定变量、函数等的类型。这可以帮助您避免在运行时之前无法检测到的错误。

TypeScript 还可以使您的代码更具可读性和可维护性。这是因为您可以使用 TypeScript 的类型注释来记录变量、函数等的类型。这使其他开发人员更容易理解您的代码。

将 TypeScript 与 Next.js 结合使用的另一个好处是它可以改进您的开发工作流程。这是因为 TypeScript 编译器可以在您处理代码时检查您的代码是否存在错误。与等待代码编译后再进行测试相比，这可以为您节省大量时间。

## 入门

现在我们已经了解了将 TypeScript 与 Next.js 结合使用的一些好处，让我们开始吧。

首先，确保安装了 Node.js 和 TypeScript。然后，为您的项目创建一个新目录。

接下来，使用 TypeScript 初始化您的项目。您可以通过运行以下命令来执行此操作：

```
$ tsc --init
```

这将在您的项目中创建一个 tsconfig.json 文件。此文件包含项目的 TypeScript 配置。

接下来，在您的项目中创建一个名为 next.config.js 的新文件。此文件包含项目的 Next.js 配置。

接下来，将以下代码添加到您的 next.config.js 文件中：

```js
const withTypeScript = require('@zeit/next-typescript');

module.exports = withTypeScript();
```

这会将 Next.js 配置为使用 TypeScript。

接下来，在您的项目中创建一个名为 pages/index.tsx 的新文件。此文件包含项目的 React 代码。

将以下代码添加到您的 pages/index.tsx 文件中：

```js
import * as React from 'react';

export default class extends React.Component {
  static getInitialProps({ req }) {
    const userAgent = req ? req.headers['user-agent'] : navigator.userAgent;
    return { userAgent };
  }

  render() {
    return (
      <div>
        Hello, world!
      </div>
    );
  }
}
```

此代码将呈现一个简单的“Hello, world!”信息。

最后，通过运行以下命令启动您的开发服务器：

```
$ npm run dev
```

你现在应该看到你的“你好，世界！”消息显示在您的浏览器中。

## 外部资源

- [打字稿](https://www.typescriptlang.org/)
- [反应](https://reactjs.org/)
- [Next.js](https://nextjs.org/)