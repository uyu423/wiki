---
title: 016: Debugging Nest.js applications
description: 
published: true
date: 2023-02-15T01:32:26.113Z
tags: 
editor: markdown
dateCreated: 2023-02-15T01:32:18.365Z
---

- [016: Depuración de aplicaciones Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/016-debugging-nest-js-applications)
{.links-list}
- [016: 调试 Nest.js 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/016-debugging-nest-js-applications)
{.links-list}
- [016: Nest.js 애플리케이션 디버깅***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/016-debugging-nest-js-applications)
{.links-list}


# Debugging Nest.js applications

Nest.js is a Node.js framework for building server-side applications. It uses TypeScript and is based on Express.

Debugging Nest.js applications can be challenging, as there are multiple ways to debug Node.js applications in general, and Nest.js adds its own complexities on top of that. In this post, we'll go over some of the basics of debugging Nest.js applications.

## Debugging Node.js applications

Node.js applications can be debugged in a number of ways. The most common way is to use the Node.js debugger, which can be invoked with the `debug` command.

```
$ node debug <script.js>
```

This will start the Node.js debugger and provide a prompt where you can enter commands. For a full list of commands, type `help` at the prompt.

Another way to debug Node.js applications is to use a graphical debugger, such as the one provided by Visual Studio Code. To use this, you'll need to install the Node.js extension for Visual Studio Code.

Once the extension is installed, you can open your Nest.js project in Visual Studio Code and set breakpoints in your code. To start the debugger, press F5 or click the Debug icon in the Activity Bar.

## Debugging Nest.js applications

Nest.js adds its own layer on top of Node.js, so the methods for debugging Nest.js applications are similar to those for debugging Node.js applications.

The most common way to debug Nest.js applications is to use the `nest` command, which is provided by the Nest.js CLI.

```
$ nest debug <script.ts>
```

This will start the Nest.js debugger and provide a prompt where you can enter commands. For a full list of commands, type `help` at the prompt.

Another way to debug Nest.js applications is to use a graphical debugger, such as the one provided by Visual Studio Code. To use this, you'll need to install the Nest.js extension for Visual Studio Code.

Once the extension is installed, you can open your Nest.js project in Visual Studio Code and set breakpoints in your code. To start the debugger, press F5 or click the Debug icon in the Activity Bar.

## Additional Information

- [Debugging Node.js applications](https://nodejs.org/en/docs/guides/debugging-getting-started/)
- [Debugging Nest.js applications](https://docs.nestjs.com/cli/debug)
- [Visual Studio Code extension for Nest.js](https://marketplace.visualstudio.com/items?itemName=nestjs.nest-cli)