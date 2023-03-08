---
title: 使用 TypeScript 和 Node.js 构建图像和视频处理应用程序
description: 
published: true
date: 2023-02-08T20:17:42.089Z
tags: 
editor: markdown
dateCreated: 2023-02-08T20:17:40.459Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Building Image and Video Processing Applications with TypeScript and Node.js***English** document is available*](/en/Knowledge-base/TypeScript/building-image-and-video-processing-applications-with-typescript-and-node-js)
{.links-list}


# 使用 TypeScript 和 Node.js 构建图像和视频处理应用程序

想要创建可扩展的图像和视频处理应用程序的开发人员在编程语言方面有很多选择。一个经常被忽视的选项是 TypeScript。 TypeScript 是 JavaScript 的类型化超集，可编译为纯 JavaScript。它是一种既易于初学者学习又具有经验丰富的开发人员可以利用的高级功能的语言。

Node.js 是一个基于 Chrome 的 V8 JavaScript 引擎构建的 JavaScript 运行时。它用于开发服务器端应用程序。 Node.js 应用程序是用 JavaScript 编写的，可以在各种平台上运行，包括 Windows、macOS 和 Linux。

在本文中，我们将展示如何使用 TypeScript 和 Node.js 构建图像处理应用程序。我们将使用 TypeScript 库 gm，它是 GraphicsMagick 库的包装器。 GraphicsMagick 是一个跨平台的图像处理工具包，可用于创建、编辑和转换图像。

gm 库提供了一个简单的 API 来执行常见的图像处理任务，例如调整大小、裁剪和转换图像。它可用于创建命令行和 Web 应用程序。在本文中，我们将创建一个可调整图像大小的命令行应用程序。

## 安装 TypeScript 和 Node.js

在开始编写应用程序之前，我们需要安装 TypeScript 和 Node.js。可以使用 Node.js 包管理器 npm 安装 TypeScript。要安装 TypeScript，请打开终端并运行以下命令：

```
npm install -g typescript
```

这将安装 TypeScript 编译器 tsc 和 TypeScript 语言服务器 tsserver。 TypeScript 编译器用于将 TypeScript 代码编译成 JavaScript 代码。 TypeScript 语言服务器为 TypeScript 代码提供代码补全和类型检查等语言服务。

Node.js 可以从 Node.js 网站下载。安装 Node.js 后，npm 命令行界面将可用。

## 创建一个 TypeScript 项目

现在我们已经安装了 TypeScript 和 Node.js，我们可以创建一个 TypeScript 项目。为此，我们将使用 npm init 命令。此命令将创建一个 package.json 文件，用于管理 Node.js 项目的依赖项。

要创建 TypeScript 项目，请打开终端并导航到要创建项目的目录。然后，运行以下命令：

```
npm init
```

这将提示您输入一些问题，例如项目的名称和版本。对于我们的项目，我们将名称设置为“image-processing-app”，版本设置为“1.0.0”。

创建 package.json 文件后，我们可以为我们的项目安装依赖项。对于我们的项目，我们需要安装 gm TypeScript 定义和 gm 库。为此，请运行以下命令：

```
npm install --save @types/gm gm
```

这会将 gm TypeScript 定义和 gm 库安装到 node_modules 目录中。 gm TypeScript 定义为 gm 库提供了 TypeScript 绑定。

## 调整图像大小

现在我们已经设置好项目，可以开始编写应用程序了。我们需要做的第一件事是导入 gm 库。我们可以通过将以下行添加到我们的 main.ts 文件的顶部来做到这一点：

```typescript
import * as gm from "gm";
```

这会将 gm 命名空间导入到我们的文件中。我们现在可以使用 gm 命名空间来访问 gm 库的功能。

接下来我们需要做的是打开我们的图像。我们可以使用 gm.open() 函数来做到这一点。此函数将图像的路径作为其第一个参数，并将回调函数作为其第二个参数。使用错误对象和 gm 对象调用回调函数。 gm 对象可用于对图像执行操作。

我们可以打开图像并将 gm 对象传递给 resize() 函数，如下所示：

```typescript
gm.open("input.jpg", (err, image) => {
  if (err) {
    console.log(err);
  } else {
    resize(image);
  }
});
```

resize() 函数将获取 gm 对象并调整图像大小。我们可以定义 resize() 函数如下：

```typescript
function resize(image: gm.Image): void {
  image
    .resize(100, 100)
    .write("output.jpg", (err) => {
      if (err) {
        console.log(err);
      }
    });
}
```

此函数会将图像调整为 100x100 像素并将输出写入 output.jpg 文件。

要运行我们的应用程序，我们可以使用 TypeScript 编译器 tsc。我们可以通过运行以下命令来编译我们的代码：

```
tsc main.ts
```

这将在当前目录中生成一个 main.js 文件。我们可以通过运行以下命令来运行我们的应用程序：

```
node main.js
```

这将调整 input.jpg 图像的大小并将输出保存到 output.jpg 文件。

## 结论

在本文中，我们展示了如何使用 TypeScript 和 Node.js 构建图像处理应用程序。我们已经了解了如何使用 gm 库来调整图像的大小。此应用程序可以轻松扩展以执行其他图像处理任务，例如裁剪和转换图像。