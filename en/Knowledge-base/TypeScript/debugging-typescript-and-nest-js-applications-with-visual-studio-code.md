---
title: Debugging TypeScript and Nest.js Applications with Visual Studio Code
description: 
published: true
date: 2023-02-01T15:23:50.521Z
tags: 
editor: markdown
dateCreated: 2023-02-01T15:23:46.441Z
---

- [Depuración de aplicaciones TypeScript y Nest.js con Visual Studio Code***Spanish** version of this document is available*](/es/Knowledge-base/TypeScript/debugging-typescript-and-nest-js-applications-with-visual-studio-code)
{.links-list}
- [Visual Studio Code로 TypeScript 및 Nest.js 애플리케이션 디버깅***Korean** version of this document is available*](/ko/Knowledge-base/TypeScript/debugging-typescript-and-nest-js-applications-with-visual-studio-code)
{.links-list}
- [使用 Visual Studio Code 调试 TypeScript 和 Nest.js 应用程序***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/TypeScript/debugging-typescript-and-nest-js-applications-with-visual-studio-code)
{.links-list}



# Debugging TypeScript and Nest.js Applications with Visual Studio Code

TypeScript is a powerful language that provides static type-checking and code refactoring. Nest.js is a framework for building scalable server-side applications. Visual Studio Code is a popular code editor that offers excellent support for TypeScript and Nest.js.

In this article, we will discuss how to debug TypeScript and Nest.js applications with Visual Studio Code. We will look at how to set up breakpoints, inspect variables, and use the console. We will also learn about some of the advanced features of the debugger, such as the Call Stack and the Debugger Console.

## Setting Up the Debugger

The first thing we need to do is set up the debugger. To do this, open Visual Studio Code and press `Ctrl+Shift+P` (Windows) or `Cmd+Shift+P` (macOS) to open the Command Palette. Type `debug` and select the `Debug: Open launch.json` command.

This will open the `.vscode/launch.json` file. We need to add a configuration for our TypeScript application. The configuration should look something like this:

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

Let's break down this configuration. The `type` attribute specifies the type of debugger. We want to use the `node` debugger because we are debugging a Node.js application. The `request` attribute specifies the type of launch. We want to use the `launch` request so that the debugger will launch the program.

The `name` attribute is the name of the configuration. This is the name that will be displayed in the Debug drop-down list. The `program` attribute is the path to the program that we want to debug. In this case, we are debugging the `index.js` file in the `dist` directory.

The `outFiles` attribute is an array of glob patterns that specify the files that should be considered for debugging. In this case, we are including all of the JavaScript files in the `dist` directory.

## Launching the Debugger

Now that we have created a launch configuration, we can launch the debugger. To do this, press `F5` or select the `Debug: Start Debugging` command from the Command Palette. This will launch the debugger and attach it to the program.

## Breaking on Exceptions

One of the most useful features of the debugger is the ability to break on exceptions. This can be very helpful when trying to track down a bug. To enable this feature, open the `.vscode/launch.json` file and add the `"stopOnEntry": true` attribute to the configuration. This will cause the debugger to break on the first line of the program.

## Setting Breakpoints

Another useful feature of the debugger is the ability to set breakpoints. A breakpoint is a point in the code where the execution of the program will be halted so that you can examine the state of the program. To set a breakpoint, simply click on the line of code where you want to break. A red dot will appear to indicate that a breakpoint has been set.

## Inspecting Variables

When the execution of the program is halted at a breakpoint, you can inspect the values of variables. To do this, simply hover over the variable. The value of the variable will be displayed in a tooltip.

You can also use the `Debug Console` to inspect variables. To open the `Debug Console`, press `Ctrl+Shift+Y` (Windows) or `Cmd+Shift+Y` (macOS). The `Debug Console` will be displayed in the Output panel.

## Using the Call Stack

The `Call Stack` panel is a very useful tool for debugging. It shows the sequence of function calls that led to the current point in the execution of the program. To open the `Call Stack` panel, press `Ctrl+\` (Windows) or `Cmd+\` (macOS).

## Conclusion

In this article, we have learned how to debug TypeScript and Nest.js applications with Visual Studio Code. We have looked at how to set up breakpoints, inspect variables, and use the console. We have also learned about some of the advanced features of the debugger, such as the Call Stack and the Debugger Console.