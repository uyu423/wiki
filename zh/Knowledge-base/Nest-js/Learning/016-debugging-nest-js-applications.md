---
title: 016: 调试 Nest.js 应用程序
description: 
published: true
date: 2023-02-15T01:32:20.443Z
tags: 
editor: markdown
dateCreated: 2023-02-15T01:32:18.359Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [016: Debugging Nest.js applications***English** document is available*](/en/Knowledge-base/Nest-js/Learning/016-debugging-nest-js-applications)
{.links-list}


# 调试 Nest.js 应用程序

Nest.js 是一个用于构建服务器端应用程序的 Node.js 框架。它使用 TypeScript 并基于 Express。

调试 Nest.js 应用程序可能具有挑战性，因为通常有多种方法可以调试 Node.js 应用程序，而 Nest.js 又增加了自己的复杂性。在这篇文章中，我们将回顾调试 Nest.js 应用程序的一些基础知识。

## 调试 Node.js 应用程序

可以通过多种方式调试 Node.js 应用程序。最常见的方法是使用 Node.js 调试器，它可以通过 `debug` 命令调用。

```
$ node debug <script.js>
```

这将启动 Node.js 调试器并提供一个提示符，您可以在其中输入命令。如需完整的命令列表，请在提示符下键入“help”。

调试 Node.js 应用程序的另一种方法是使用图形调试器，例如 Visual Studio Code 提供的调试器。要使用它，您需要为 Visual Studio Code 安装 Node.js 扩展。

安装扩展后，您可以在 Visual Studio Code 中打开 Nest.js 项目并在代码中设置断点。要启动调试器，请按 F5 或单击活动栏中的“调试”图标。

## 调试 Nest.js 应用程序

Nest.js 在 Node.js 之上添加了自己的层，因此调试 Nest.js 应用程序的方法与调试 Node.js 应用程序的方法类似。

调试 Nest.js 应用程序的最常见方法是使用 Nest.js CLI 提供的 `nest` 命令。

```
$ nest debug <script.ts>
```

这将启动 Nest.js 调试器并提供一个提示符，您可以在其中输入命令。如需完整的命令列表，请在提示符下键入“help”。

调试 Nest.js 应用程序的另一种方法是使用图形调试器，例如 Visual Studio Code 提供的调试器。要使用它，您需要为 Visual Studio Code 安装 Nest.js 扩展。

安装扩展后，您可以在 Visual Studio Code 中打开 Nest.js 项目并在代码中设置断点。要启动调试器，请按 F5 或单击活动栏中的“调试”图标。

## 附加信息

- [调试 Node.js 应用程序](https://nodejs.org/en/docs/guides/debugging-getting-started/)
- [调试 Nest.js 应用程序](https://docs.nestjs.com/cli/debug)
- [Nest.js 的 Visual Studio 代码扩展](https://marketplace.visualstudio.com/items?itemName=nestjs.nest-cli)