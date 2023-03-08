---
title: 使用 TypeScript 和 Next.js 构建渐进式 Web 应用程序
description: 
published: true
date: 2023-02-02T02:43:47.137Z
tags: 
editor: markdown
dateCreated: 2023-02-02T02:43:45.412Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Building Progressive Web Applications with TypeScript and Next.js***English** document is available*](/en/Knowledge-base/TypeScript/building-progressive-web-applications-with-typescript-and-next-js)
{.links-list}


TypeScript 是 JavaScript 的类型化超集，可编译为纯 JavaScript。它提供类、模块和接口来帮助您构建健壮的组件。

Next.js 是一个 React 框架，可以轻松创建生产就绪的服务器呈现应用程序。它包括自动代码拆分、静态文件服务、路由处理和通用渲染等功能。

在本文中，我们将学习如何使用 TypeScript 和 Next.js 构建渐进式 Web 应用程序 (PWA)。我们将从创建一个简单的 PWA 开始，该 PWA 从 JSON 文件加载 List 组件。然后，我们将 TypeScript 添加到我们的项目中，并使用 React typings 对我们的组件进行类型检查。最后，我们将学习如何使用代码拆分和路由预取等 Next.js 功能来提高 PWA 的性能。

## 使用 TypeScript 和 Next.js 创建一个简单的 PWA

我们将从创建一个简单的 Next.js 应用程序开始，该应用程序从 JSON 文件加载 List 组件。 List 组件将由服务器呈现，并将包括代码拆分和路由预取。

首先，让我们创建一个新的 Next.js 项目：

```
npx create-next-app my-app
```

接下来，我们需要安装以下依赖项：

```
npm install --save react react-dom next
```

现在，我们可以创建我们的 List 组件。创建一个名为 List.js 的新文件并添加以下代码：

```js
import React from 'react';

const List = ({ items }) => (
  <ul>
    {items.map(item => (
      <li key={item.id}>{item.text}</li>
    ))}
  </ul>
);

export default List;
```

该组件将采用 `items` 道具并呈现项目列表。每个项目都有一个键和一个文本。

接下来，我们需要创建一个包含列表项的 JSON 文件。创建一个名为 listItems.json 的新文件并添加以下代码：

```json
[
  { "id": 1, "text": "Item 1" },
  { "id": 2, "text": "Item 2" },
  { "id": 3, "text": "Item 3" }
]
```

现在，我们可以在我们的 List.js 组件中导入这个 JSON 文件：

```js
import listItems from './listItems.json';
```

最后，我们需要告诉 Next.js 在服务器上渲染我们的 List 组件。打开 `pages/index.js` 文件并将内容替换为以下代码：

```js
import React from 'react';
import List from '../components/List';

const IndexPage = () => <List items={listItems} />;

export default IndexPage;
```

这将在服务器上呈现我们的 List 组件，并将 `listItems` JSON 数据作为 prop 传递给组件。

现在，如果我们运行我们的应用程序，我们应该会看到我们的 List 组件被呈现在页面上：

```
npm run dev
```

## 将 TypeScript 添加到我们的项目中

接下来，我们将 TypeScript 添加到我们的项目中，并使用 React typings 对我们的组件进行类型检查。

首先，我们需要安装 TypeScript 编译器：

```
npm install --save-dev typescript
```

然后，我们需要在项目的根目录中创建一个 tsconfig.json 文件。该文件将包含我们的 TypeScript 配置。将以下代码添加到 `tsconfig.json` 文件中：

```json
{
  "compilerOptions": {
    "jsx": "react",
    "target": "esnext",
    "module": "commonjs",
    "strict": true
  },
  "include": ["src"]
}
```

此配置将告诉 TypeScript 编译器以最新的 JavaScript 标准 (ESNext) 为目标，并将我们的代码视为 CommonJS 模块。

接下来，我们需要安装 React typings：

```
npm install --save-dev @types/react @types/react-dom
```

现在，我们可以将我们的 `List.js` 组件重命名为 `List.tsx` 并开始使用 TypeScript。首先，我们将为道具添加类型：

```tsx
import React from 'react';

interface ListProps {
  items: {
    id: number;
    text: string;
  }[];
}

const List: React.FC<ListProps> = ({ items }) => (
  <ul>
    {items.map(item => (
      <li key={item.id}>{item.text}</li>
    ))}
  </ul>
);

export default List;
```

我们已经为我们的道具声明了一个名为 ListProps 的接口。这个接口定义了道具的形状。我们还使用“React.FC”泛型向我们的组件添加了类型。这个泛型允许我们指定道具的类型。

现在，如果我们尝试将一个无效的 prop 传递给我们的组件，我们将得到一个类型错误：

```tsx
// TypeError: Type '{ items: number[]; }' is not assignable to type 'IntrinsicAttributes & ListProps'.
//   Property 'items' does not exist on type 'IntrinsicAttributes & ListProps'.ts(2322)
<List items={[1, 2, 3]} />
```

## 使用 Next.js 特性来提高性能

最后，我们将学习如何使用代码拆分和路由预取等 Next.js 功能来提高 PWA 的性能。

### 代码拆分

Next.js 包含一个称为代码拆分的功能，它允许我们将代码拆分为多个包。这样，浏览器就可以只下载和执行当前页面所需的代码。

要在我们的 List 组件中使用代码拆分，我们需要使用“React.lazy”组件。该组件允许我们在运行时动态加载组件。

首先，让我们导入 `React.lazy` 组件：

```tsx
import React, { lazy } from 'react';
```

然后，我们可以使用 `lazy` 组件来动态加载我们的 List 组件：

```tsx
const List = lazy(() => import('./List'));
```

现在，我们的 List 组件只会在需要时加载。

### 路由预取

Next.js 还包括一个称为路由预取的功能。此功能允许 Next.js 在后台预取其他页面的代码。这样，当用户导航到这些页面时，代码已经下载完毕，页面加载速度也会更快。

要使用路由预取，我们需要使用 Next.js 中的 `Link` 组件。该组件将创建指向我们应用程序中另一个页面的链接。

首先，让我们导入 `Link` 组件：

```tsx
import Link from 'next/link';
```

然后，我们可以使用 `Link` 组件创建到另一个页面的链接：

```tsx
<Link href="/page2" prefetch>
  <a>Navigate to page 2</a>
</Link>
```

这将在我们的应用程序中创建一个指向 `/page2` 路由的链接。 `prefetch` 属性将告诉 Next.js 在后台预取此路由的代码。

## 结论

在本文中，我们学习了如何使用 TypeScript 和 Next.js 构建渐进式 Web 应用程序 (PWA)。我们从创建一个简单的 PWA 开始，它从 JSON 文件加载 List 组件。然后，我们将 TypeScript 添加到我们的项目中，并使用 React typings 对我们的组件进行类型检查。最后，我们学习了如何使用代码拆分和路由预取等 Next.js 功能来提高 PWA 的性能。