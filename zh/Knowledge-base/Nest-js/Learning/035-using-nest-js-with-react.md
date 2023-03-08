---
title: 035: 将 Nest.js 与 React 结合使用
description: 
published: true
date: 2023-02-02T00:18:31.587Z
tags: 
editor: markdown
dateCreated: 2023-02-02T00:18:29.881Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [035: Using Nest.js with React***English** document is available*](/en/Knowledge-base/Nest-js/Learning/035-using-nest-js-with-react)
{.links-list}


# 介绍

Nest.js 是一个用于构建可扩展的服务器端应用程序的 Node.js 框架。它使用 TypeScript（JavaScript 的超集），并结合了函数式编程和面向对象编程的元素。

React 是一个用于构建用户界面的 JavaScript 库。它是声明性的、高效的和灵活的。

在这篇文章中，我们将看到如何将 Nest.js 与 React 结合使用。

# 设置项目

我们将使用 create-react-app CLI 生成 React 项目。

```
npx create-react-app nestjs-react-app
```

这将创建一个名为“nestjs-react-app”的目录，其结构如下：

```
nestjs-react-app/
├── README.md
├── node_modules/
├── package.json
├── .gitignore
├── public/
│   ├── favicon.ico
│   ├── index.html
│   └── manifest.json
└── src/
    ├── App.css
    ├── App.js
    ├── App.test.js
    ├── index.css
    ├── index.js
    ├── logo.svg
    └── serviceWorker.js
```

我们将在项目的 React 和 Nest.js 部分使用 TypeScript。

首先，我们需要安装 TypeScript 编译器以及 React 和 React-DOM 的类型定义：

```
npm install --save-dev typescript @types/react @types/react-dom
```

接下来，我们需要修改 tsconfig.json 文件以包含 React 和 React-DOM 定义：

```
{
  "compilerOptions": {
    ...
  },
  "include": [
    "src/**/*"
  ],
  "exclude": [
    "node_modules",
    "**/*.spec.ts"
  ]
}
```

我们还需要修改 `jsconfig.json` 文件以包含 React 和 React-DOM 定义：

```
{
  "compilerOptions": {
    "target": "es6",
    "jsx": "react"
  },
  "include": [
    "src/**/*"
  ]
}
```

现在我们已经设置了 TypeScript，我们可以使用以下命令安装 Nest.js：

```
npm install --save @nestjs/core @nestjs/common rxjs reflect-metadata
```

# 创建 Nest.js 服务器

我们将从在 `src` 目录中创建一个名为 `server.ts` 的文件开始。该文件将包含我们的 Nest.js 服务器的代码。

```
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

在 server.ts 文件中，我们首先从 @nestjs/core 导入 NestFactory 和 AppModule。

`NestFactory` 用于创建 Nest.js 应用程序实例。 `AppModule` 是一个包含我们应用程序代码的模块。

然后我们定义一个名为 bootstrap 的 async 函数，它将用于启动我们的 Nest.js 服务器。

在 `bootstrap` 函数中，我们使用 `NestFactory` 创建了 `AppModule` 的实例，然后我们调用 `listen` 方法来启动服务器。

# 创建 React 前端

我们将从在 `src` 目录中创建一个名为 `App.tsx` 的文件开始。该文件将包含我们的 React 前端的代码。

```
import React from 'react';
import './App.css';

function App() {
  return (
    <div className="App">
      <h1>Hello, world!</h1>
    </div>
  );
}

export default App;
```

在 App.tsx 文件中，我们首先导入 React 和 App.css 文件。

然后我们定义一个名为“App”的函数，它返回一个“div”元素。在 `div` 元素内，我们有一个 `h1` 元素，其中包含文本“Hello, world!”。

最后，我们导出 App 函数，以便在程序的其他部分使用。

# 连接 React 和 Nest.js

我们将首先修改 `server.ts` 文件以包含以下代码：

```
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { NestExpressApplication } from '@nestjs/platform-express';
import { join } from 'path';

async function bootstrap() {
  const app = await NestFactory.create<NestExpressApplication>(
    AppModule,
  );
  app.useStaticAssets(join(__dirname, '..', 'public'));
  app.setBaseViewsDir(join(__dirname, '..', 'views'));
  app.setViewEngine('hbs');
  await app.listen(3000);
}
bootstrap();
```

在 server.ts 文件中，我们首先从 @nestjs/core 导入 NestFactory、AppModule 和 NestExpressApplication。

我们还从 path 模块中导入 join 函数。

`NestFactory` 用于创建 Nest.js 应用程序实例。 `AppModule` 是一个包含我们应用程序代码的模块。 `NestExpressApplication` 用于配置 Express 服务器。

然后我们定义一个名为 bootstrap 的 async 函数，它将用于启动我们的 Nest.js 服务器。

在 `bootstrap` 函数中，我们使用 `NestFactory` 创建了 `AppModule` 的实例，然后我们调用 `useStaticAssets` 和 `setBaseViewsDir` 方法来配置 Express 服务器。

最后，我们调用 `listen` 方法来启动服务器。

# 在 Nest.js 中渲染 React

我们将首先修改 `server.ts` 文件以包含以下代码：

```
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { NestExpressApplication } from '@nestjs/platform-express';
import { join } from 'path';
import { renderFile } from 'pug';

async function bootstrap() {
  const app = await NestFactory.create<NestExpressApplication>(
    AppModule,
  );
  app.useStaticAssets(join(__dirname, '..', 'public'));
  app.setBaseViewsDir(join(__dirname, '..', 'views'));
  app.setViewEngine('pug');
  app.get('/', (req, res) => {
    res.render('index', {
      message: 'Hello, world!',
    });
  });
  await app.listen(3000);
}
bootstrap();
```

在 `server.ts` 文件中，我们首先从 `pug` 模块导入 `NestFactory`、`AppModule`、`NestExpressApplication`、`join` 函数和 `renderFile` 函数。

`NestFactory` 用于创建 Nest.js 应用程序实例。 `AppModule` 是一个包含我们应用程序代码的模块。 `NestExpressApplication` 用于配置 Express 服务器。

然后我们定义一个名为 bootstrap 的 async 函数，它将用于启动我们的 Nest.js 服务器。

在 `bootstrap` 函数中，我们使用 `NestFactory` 创建了 `AppModule` 的实例，然后我们调用 `useStaticAssets`、`setBaseViewsDir` 和 `setViewEngine` 方法来配置 Express 服务器。

接下来，我们为呈现 index.pug 模板的 `/` 路径定义路由处理程序。

最后，我们调用 `listen` 方法来启动服务器。

# 将数据从 Nest.js 传递到 React

我们将首先修改 `server.ts` 文件以包含以下代码：

```
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { NestExpressApplication } from '@nestjs/platform-express';
import { join } from 'path';
import { renderFile } from 'pug';

async function bootstrap() {
  const app = await NestFactory.create<NestExpressApplication>(
    AppModule,
  );
  app.useStaticAssets(join(__dirname, '..', 'public'));
  app.setBaseViewsDir(join(__dirname, '..', 'views'));
  app.setViewEngine('pug');
  app.get('/', (req, res) => {
    res.render('index', {
      message: 'Hello, world!',
    });
  });
  await app.listen(3000);
}
bootstrap();
```

在 `server.ts` 文件中，我们首先从 `pug` 模块导入 `NestFactory`、`AppModule`、`NestExpressApplication`、`join` 函数和 `renderFile` 函数。

`NestFactory` 用于创建 Nest.js 应用程序实例。 `AppModule` 是一个包含我们应用程序代码的模块。 `NestExpressApplication` 用于配置 Express 服务器。

然后我们定义一个名为 bootstrap 的 async 函数，它将用于启动我们的 Nest.js 服务器。

在 `bootstrap` 函数中，我们使用 `NestFactory` 创建了 `AppModule` 的实例，然后我们调用 `useStaticAssets`、`setBaseViewsDir` 和 `setViewEngine` 方法来配置 Express 服务器。

接下来，我们为呈现 index.pug 模板的 `/` 路径定义路由处理程序。

最后，我们调用 `listen` 方法来启动服务器。

# 将数据从 React 传递到 Nest.js

我们将首先修改 App.tsx 文件以包含以下代码：

```
import React from 'react';
import './App.css';

function App() {
  const [message, setMessage] = React.useState('Hello, world!');
  return (
    <div className="App">
      <h1>{message}</h1>
      <button onClick={() => setMessage('Nest.js is awesome!')}>
        Click me!
      </button>
    </div>
  );
}

export default App;
```

在 App.tsx 文件中，我们首先导入 React 和 App.css 文件。

然后我们定义一个名为“App”的函数，它返回一个“div”元素。在 `div` 元素内，我们有一个 `h1` 元素，其中包含文本“Hello, world!”。

我们还有一个 `button` 元素，当点击它时，会将 `h1` 元素中的文本更改为“Nest.js is awesome!”。

最后，我们导出 App 函数，以便在程序的其他部分使用。

# 结论

在这篇文章中，我们看到了如何将 Nest.js 与 React 结合使用。

我们首先设置项目，然后创建 Nest.js 服务器。

接下来，我们创建了 React 前端并连接了 React 和 Nest.js。

最后，我们看到了如何将数据从 Nest.js 传递到 React 以及从 React 传递到 Nest.js。