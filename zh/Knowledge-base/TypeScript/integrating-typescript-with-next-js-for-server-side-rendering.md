---
title: 将 TypeScript 与 Next.js 集成以进行服务器端渲染
description: 
published: true
date: 2023-02-01T14:04:51.859Z
tags: 
editor: markdown
dateCreated: 2023-02-01T14:04:50.366Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Integrating TypeScript with Next.js for Server-side Rendering***English** version of this document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-next-js-for-server-side-rendering)
{.links-list}


  注意：此模板适用于特定文章。如果您不是在写这篇文章，请删除这段文字并替换为您自己的内容。

# 将 TypeScript 与 Next.js 集成用于服务器端渲染

如果您希望将 TypeScript 与 [Next.js](https://nextjs.org/) 结合使用，那么您很幸运！ Next.js 具有一流的 TypeScript 支持，在您的 Next.js 项目中使用 TypeScript 很容易启动和运行。在本文中，我们将了解如何使用 Next.js 设置 TypeScript 以及如何将 TypeScript 与 Next.js 的[服务器端渲染](https://nextjs.org/docs/basic-features /pages#server-side-rendering) 特性。

## 在 Next.js 中设置 TypeScript

我们需要做的第一件事是创建一个新的 Next.js 项目。我们可以使用 [`create-next-app`](https://github.com/zeit/next.js/tree/canary/packages/create-next-app) 来做到这一点，这是一个命令行工具，可以设置为你创建一个新的 Next.js 项目。

要安装 `create-next-app`，我们需要运行以下命令：

```
npm init next-app
```

安装 create-next-app 后，我们可以通过运行以下命令创建一个新的 Next.js 项目：

```
create-next-app my-app
```

这将创建一个名为 my-app 的新目录，其中包含 Next.js 项目所需的基本文件。

接下来，我们需要安装 TypeScript。我们可以通过运行以下命令来完成此操作：

```
npm install --save-dev typescript
```

安装 TypeScript 后，我们可以在项目的根目录中创建一个 tsconfig.json 文件。该文件告诉 TypeScript 我们希望如何编译代码。

`tsconfig.json` 文件应该如下所示：

```json
{
  "compilerOptions": {
    "target": "esnext",
    "module": "commonjs",
    "jsx": "preserve",
    "outDir": "./build",
    "strict": true
  },
  "exclude": [
    "node_modules"
  ]
}
```

接下来，我们需要在项目的根目录中创建一个 .babelrc 文件。这个文件告诉 [Babel](https://babeljs.io/) 我们希望如何编译我们的代码。

`.babelrc` 文件应该是这样的：

```json
{
  "presets": [
    "next/babel"
  ]
}
```

现在我们已经设置了 TypeScript 和 Babel，我们可以在 `pages` 目录中创建一个 `.tsx` 文件。该文件将是我们将在服务器端呈现的页面。

`.tsx` 文件应如下所示：

```jsx
import * as React from 'react'

export default function Page() {
  return <div>Hello, world!</div>
}
```

现在我们已经创建了页面，我们可以通过运行以下命令来启动我们的 Next.js 开发服务器：

```
npm run dev
```

如果我们导航到 http://localhost:3000，我们应该看到我们的页面正在服务器端呈现。

## 将 TypeScript 与 Next.js 的服务器端渲染结合使用

现在我们已经设置了项目，让我们来看看如何将 TypeScript 与 Next.js 的服务器端渲染功能结合使用。

首先，我们需要在 `pages` 目录中创建一个名为 `api.ts` 的文件。该文件将包含我们的 [`getInitialProps`](https://nextjs.org/docs/basic-features/pages#getinitialprops) 函数。

`api.ts` 文件应该如下所示：

```js
import { NextPageContext } from 'next'

export default function Page(ctx: NextPageContext) {
  return {
    hello: 'world'
  }
}
```

接下来，我们需要更新我们的 .tsx 文件以调用 api.ts 文件。为此，我们将 [`getInitialProps`](https://nextjs.org/docs/basic-features/pages#getinitialprops) 属性添加到我们的 `Page` 组件。

`.tsx` 文件现在应该如下所示：

```jsx
import * as React from 'react'
import { PageProps } from 'api'

export default function Page(props: PageProps) {
  return <div>Hello, {props.hello}!</div>
}
```

如果我们导航到 http://localhost:3000，我们应该看到我们的页面正在服务器端使用我们的 api.ts 文件中的数据呈现。

## 包起来

在本文中，我们了解了如何使用 Next.js 设置 TypeScript 以及如何将 TypeScript 与 Next.js 的服务器端渲染功能结合使用。使用 TypeScript 和 Next.js，您可以轻松构建类型安全的服务器端呈现的 React 应用程序。