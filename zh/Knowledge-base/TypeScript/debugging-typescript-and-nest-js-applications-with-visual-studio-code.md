---
title: 使用 Visual Studio Code 调试 TypeScript 和 Nest.js 应用程序
description: 
published: true
date: 2023-02-01T15:23:48.064Z
tags: 
editor: markdown
dateCreated: 2023-02-01T15:23:46.474Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Debugging TypeScript and Nest.js Applications with Visual Studio Code***English** version of this document is available*](/en/Knowledge-base/TypeScript/debugging-typescript-and-nest-js-applications-with-visual-studio-code)
{.links-list}



# 使用 Visual Studio Code 调试 TypeScript 和 Nest.js 应用程序

TypeScript 是一种强大的语言，可提供静态类型检查和代码重构。 Nest.js 是一个用于构建可扩展的服务器端应用程序的框架。 Visual Studio Code 是一种流行的代码编辑器，它为 TypeScript 和 Nest.js 提供了出色的支持。

在本文中，我们将讨论如何使用 Visual Studio Code 调试 TypeScript 和 Nest.js 应用程序。我们将了解如何设置断点、检查变量和使用控制台。我们还将了解调试器的一些高级功能，例如调用堆栈和调试器控制台。

## 设置调试器

我们需要做的第一件事是设置调试器。为此，请打开 Visual Studio Code，然后按 `Ctrl+Shift+P` (Windows) 或 `Cmd+Shift+P` (macOS) 打开命令面板。键入 `debug` 并选择 `Debug: Open launch.json` 命令。

这将打开 .vscode/launch.json 文件。我们需要为我们的 TypeScript 应用程序添加一个配置。配置应如下所示：

```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "Launch Program",
            "program": "${workspaceFolder}/dist/index.js",
            "outFiles": [
                "${workspaceFolder}/dist/**/*.js"
            ]
        }
    ]
}
```

让我们分解一下这个配置。 `type` 属性指定调试器的类型。我们想使用 `node` 调试器，因为我们正在调试 Node.js 应用程序。 `request` 属性指定启动的类型。我们想使用 `launch` 请求，以便调试器启动程序。

`name` 属性是配置的名称。这是将显示在“调试”下拉列表中的名称。 `program` 属性是我们要调试的程序的路径。在这种情况下，我们正在调试 dist 目录中的 index.js 文件。

`outFiles` 属性是一组 glob 模式，用于指定应该考虑进行调试的文件。在这种情况下，我们将所有 JavaScript 文件包含在 dist 目录中。

## 启动调试器

现在我们已经创建了启动配置，我们可以启动调试器了。为此，请按“F5”或从“命令面板”中选择“调试：启动调试”命令。这将启动调试器并将其附加到程序。

## 打破异常

调试器最有用的功能之一是能够中断异常。这在尝试追踪错误时非常有用。要启用此功能，请打开 `.vscode/launch.json` 文件并将 `"stopOnEntry": true` 属性添加到配置中。这将导致调试器在程序的第一行中断。

## 设置断点

调试器的另一个有用特性是设置断点的能力。断点是代码中的一个点，程序将在此处停止执行，以便您可以检查程序的状态。要设置断点，只需单击要中断的代码行。将出现一个红点，表示已设置断点。

## 检查变量

当程序的执行在断点处停止时，您可以检查变量的值。为此，只需将鼠标悬停在变量上即可。变量的值将显示在工具提示中。

您还可以使用“调试控制台”来检查变量。要打开“调试控制台”，请按“Ctrl+Shift+Y”(Windows) 或“Cmd+Shift+Y”(macOS)。 “调试控制台”将显示在“输出”面板中。

## 使用调用栈

`Call Stack` 面板是一个非常有用的调试工具。它显示了导致程序执行的当前点的函数调用序列。要打开“调用堆栈”面板，请按“Ctrl+\”(Windows) 或“Cmd+\”(macOS)。

## 结论

在本文中，我们学习了如何使用 Visual Studio Code 调试 TypeScript 和 Nest.js 应用程序。我们已经了解了如何设置断点、检查变量和使用控制台。我们还了解了调试器的一些高级功能，例如调用堆栈和调试器控制台。