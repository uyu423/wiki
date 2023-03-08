---
title: 066：在 Electron.js 和 Node.js 中使用 TensorFlow.js
description: 
published: true
date: 2023-02-02T21:23:21.062Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:23:19.323Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [066: Using TensorFlow.js in Electron.js with Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/066-using-tensorflow-js-in-electron-js-with-node-js)
{.links-list}


# Electron.js 中的 TensorFlow.js 与 Node.js

## 介绍

在这篇文章中，我们将探索如何在 Electron.js 和 Node.js 中使用 TensorFlow.js。我们将回顾使用 TensorFlow.js 的基础知识，然后展示如何在 Electron.js 中使用它。

## 什么是 TensorFlow.js？

TensorFlow.js 是一个用于训练和部署机器学习模型的 JavaScript 库。它用于各种任务，包括图像分类、对象检测和文本分类。

## 入门

首先，您需要安装 TensorFlow.js。您可以使用以下命令执行此操作：

```
npm install @tensorflow/tfjs
```

安装 TensorFlow.js 后，您可以使用以下行将其导入到您的 JavaScript 代码中：

```javascript
import * as tf from '@tensorflow/tfjs';
```

## 在 Electron.js 中使用 TensorFlow.js

现在我们已经安装了 TensorFlow.js，让我们来看看如何在 Electron.js 中使用它。

我们需要做的第一件事是创建一个新的 Electron.js 项目。我们可以使用以下命令执行此操作：

```
npm init electron-app my-app
```

这将创建一个名为“my-app”的新目录，其中包含 Electron.js 应用程序的基本结构。

接下来，我们需要将 TensorFlow.js 安装到我们的项目中。我们可以使用以下命令执行此操作：

```
cd my-app
npm install @tensorflow/tfjs
```

安装 TensorFlow.js 后，我们可以使用以下行将其导入到我们的 Electron.js 应用程序中：

```javascript
import * as tf from '@tensorflow/tfjs';
```

现在我们已经安装了 TensorFlow.js，我们可以开始在我们的应用程序中使用它了。

## 结论

在这篇文章中，我们探索了如何在 Electron.js 和 Node.js 中使用 TensorFlow.js。我们已经了解了使用 TensorFlow.js 的基础知识，然后展示了如何在 Electron.js 中使用它。