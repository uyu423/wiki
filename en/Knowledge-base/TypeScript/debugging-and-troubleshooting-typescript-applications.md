---
title: Debugging and Troubleshooting TypeScript Applications
description: 
published: true
date: 2023-02-24T04:32:23.017Z
tags: 
editor: markdown
dateCreated: 2023-02-24T04:32:16.136Z
---

- [TypeScript 애플리케이션 디버깅 및 문제 해결***Korean** document is available*](/ko/Knowledge-base/TypeScript/debugging-and-troubleshooting-typescript-applications)
{.links-list}


# Debugging and Troubleshooting TypeScript Applications

TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. It provides support for classes, modules, and interface. TypeScript is popular among web developers because of its static type checking, which helps to catch errors early in the development process.

Despite the benefits of using TypeScript, debugging TypeScript applications can be challenging. This is because TypeScript is compiled to JavaScript, which is interpreted at runtime. This means that TypeScript code is not executed directly by the browser.

There are a few tools that can help with debugging TypeScript applications. The first is the TypeScript compiler. The TypeScript compiler can help to find syntax errors in TypeScript code. The second is a debugging tool such as the debugger in Visual Studio Code. The debugger can help to find runtime errors in TypeScript code.

The TypeScript compiler can help to find syntax errors in TypeScript code. To use the TypeScript compiler, open the TypeScript file in Visual Studio Code. In the TypeScript file, click on the TypeScript icon in the left gutter. This will open the TypeScript Compiler Errors output panel. The TypeScript compiler will report any syntax errors in the TypeScript code.

![TypeScript Compiler Errors](https://i.imgur.com/p0SfNcu.png)

The debugger can help to find runtime errors in TypeScript code. To use the debugger, open the TypeScript file in Visual Studio Code. In the TypeScript file, set a breakpoint on a line of code. A breakpoint is a point in the code where the debugger will pause execution. To set a breakpoint, click on the line of code and press F9.

![Set breakpoint](https://i.imgur.com/FwRoJjl.png)

Then, open the Debug panel. In the Debug panel, select the TypeScript file in the dropdown. This will start the debugger and launch the TypeScript file in the browser. The debugger will pause execution at the breakpoint.

![Debug TypeScript](https://i.imgur.com/cgqUMjN.png)

In the Debug panel, you can view the value of variables in the Scope section. You can also view the call stack in the Call Stack section. The call stack shows the sequence of function calls that led to the current line of code.

![Debug panel](https://i.imgur.com/eZUjPxa.png)

To continue execution, click the play button or press F5. This will resume execution and the debugger will run to the next breakpoint.

There are many other tools that can help with debugging TypeScript applications. For a more comprehensive list, see [Debugging TypeScript](https://www.typescriptlang.org/docs/handbook/debugging.html).