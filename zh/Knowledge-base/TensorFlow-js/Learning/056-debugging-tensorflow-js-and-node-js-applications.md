---
title: 056：调试 TensorFlow.js 和 Node.js 应用程序
description: 
published: true
date: 2023-02-02T20:04:29.574Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:04:27.951Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [056: Debugging TensorFlow.js and Node.js Applications***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/056-debugging-tensorflow-js-and-node-js-applications)
{.links-list}


调试 TensorFlow.js 和 Node.js 应用程序

TensorFlow.js 和 Node.js 是分别用于机器学习和 Web 开发的两个流行的 JavaScript 平台。在本文中，我们将向您展示如何调试 TensorFlow.js 和 Node.js 应用程序。

我们将从每个平台的调试工具概述开始。然后我们将介绍一些常见的调试场景以及如何解决它们。

## 调试工具

### 张量流.js

TensorFlow.js 调试工具基于 Chrome DevTools。要使用它们，您需要在支持 DevTools 的浏览器中运行您的 TensorFlow.js 应用程序。

在浏览器中运行应用程序后，打开 DevTools 并选择“Sources”选项卡。从这里，您可以设置断点、检查变量并单步执行代码。

TensorFlow.js 调试工具还包括“TensorFlow.js 调试器”面板。此面板提供了 TensorFlow.js 代码的高级视图，可用于调试 TensorFlow.js 操作。

### 节点.js

Node.js 调试工具基于 V8 调试协议。要使用它们，您需要使用 --inspect 标志运行您的 Node.js 应用程序。

一旦您的应用程序使用 --inspect 标志运行，您就可以将调试器附加到它。我们建议使用支持 V8 调试协议的 Visual Studio Code 调试器。

附加调试器后，您可以设置断点、检查变量并单步执行代码。

## 调试场景

### 张量流.js

#### 场景：我的应用程序没有运行

如果您的 TensorFlow.js 应用程序没有运行，首先要检查浏览器控制台是否有错误。可以使用 DevTools 的“控制台”选项卡打开浏览器控制台。

如果浏览器控制台没有错误，接下来要检查的是 TensorFlow.js 操作面板。可以使用 DevTools 的“TensorFlow.js 调试器”选项卡打开此面板。

如果您在 TensorFlow.js 操作面板中看到任何错误，您可以单击它们以查看更多详细信息。

#### 场景：我的应用程序运行缓慢

如果您的 TensorFlow.js 应用程序运行缓慢，首先要检查浏览器控制台是否有警告。可以使用 DevTools 的“控制台”选项卡打开浏览器控制台。

如果浏览器控制台中没有警告，接下来要检查的是 TensorFlow.js 操作面板。可以使用 DevTools 的“TensorFlow.js 调试器”选项卡打开此面板。

如果您在 TensorFlow.js 操作面板中看到任何警告，您可以单击它们以查看更多详细信息。

#### 场景：我的应用程序没有使用 GPU

如果您的 TensorFlow.js 应用程序未使用 GPU，首先要检查浏览器控制台是否有错误。可以使用 DevTools 的“控制台”选项卡打开浏览器控制台。

如果浏览器控制台没有错误，接下来要检查的是 TensorFlow.js 操作面板。可以使用 DevTools 的“TensorFlow.js 调试器”选项卡打开此面板。

如果您在 TensorFlow.js 操作面板中看到任何错误，您可以单击它们以查看更多详细信息。

### 节点.js

#### 场景：我的应用程序没有运行

如果您的 Node.js 应用程序没有运行，首先要检查调试器控制台是否有错误。可以使用 Visual Studio Code“调试”面板打开调试器控制台。

如果调试器控制台中没有错误，接下来要检查的是 Node.js 操作面板。可以使用 Visual Studio Code“Node.js”面板打开此面板。

如果您在 Node.js 操作面板中看到任何错误，您可以单击它们以查看更多详细信息。

#### 场景：我的应用程序运行缓慢

如果您的 Node.js 应用程序运行缓慢，首先要检查调试器控制台是否有警告。可以使用 Visual Studio Code“调试”面板打开调试器控制台。

如果调试器控制台中没有警告，接下来要检查的是 Node.js 操作面板。可以使用 Visual Studio Code“Node.js”面板打开此面板。

如果您在 Node.js 操作面板中看到任何警告，您可以单击它们以查看更多详细信息。

#### 场景：我的应用程序没有使用 CPU

如果您的 Node.js 应用程序没有使用 CPU，首先要检查调试器控制台是否有错误。可以使用 Visual Studio Code“调试”面板打开调试器控制台。

如果调试器控制台中没有错误，接下来要检查的是 Node.js 操作面板。可以使用 Visual Studio Code“Node.js”面板打开此面板。

如果您在 Node.js 操作面板中看到任何错误，您可以单击它们以查看更多详细信息。

## 附加信息

### 张量流.js

有关调试 TensorFlow.js 应用程序的更多信息，请参阅 TensorFlow.js 调试文档。

### 节点.js

有关调试 Node.js 应用程序的更多信息，请参阅 Node.js 调试文档。