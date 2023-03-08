---
title: 056: Debugging TensorFlow.js and Node.js Applications
description: 
published: true
date: 2023-02-02T20:04:32.605Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:04:27.953Z
---

- [056: Depuración de aplicaciones TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/056-debugging-tensorflow-js-and-node-js-applications)
{.links-list}
- [056：调试 TensorFlow.js 和 Node.js 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/056-debugging-tensorflow-js-and-node-js-applications)
{.links-list}
- [056: TensorFlow.js 및 Node.js 애플리케이션 디버깅***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/056-debugging-tensorflow-js-and-node-js-applications)
{.links-list}


Debugging TensorFlow.js and Node.js Applications

TensorFlow.js and Node.js are two popular JavaScript platforms for machine learning and web development respectively. In this post, we'll show you how to debug TensorFlow.js and Node.js applications.

We'll start with an overview of debugging tools for each platform. Then we'll walk through a few common debugging scenarios and how to resolve them.

## Debugging Tools

### TensorFlow.js

The TensorFlow.js debugging tools are based on the Chrome DevTools. To use them, you'll need to run your TensorFlow.js application in a browser that supports the DevTools.

Once you have your application running in the browser, open the DevTools and select the "Sources" tab. From here, you can set breakpoints, inspect variables, and step through your code.

The TensorFlow.js debugging tools also include a "Debugger for TensorFlow.js" panel. This panel provides a higher-level view of your TensorFlow.js code and can be used to debug TensorFlow.js operations.

### Node.js

The Node.js debugging tools are based on the V8 Debugging Protocol. To use them, you'll need to run your Node.js application with the --inspect flag.

Once your application is running with the --inspect flag, you can attach a debugger to it. We recommend using the Visual Studio Code debugger, which supports the V8 Debugging Protocol.

Once you have your debugger attached, you can set breakpoints, inspect variables, and step through your code.

## Debugging Scenarios

### TensorFlow.js

#### Scenario: my application is not running

If your TensorFlow.js application is not running, the first thing to check is the browser console for errors. The browser console can be opened with the DevTools "Console" tab.

If there are no errors in the browser console, the next thing to check is the TensorFlow.js operations panel. This panel can be opened with the DevTools "Debugger for TensorFlow.js" tab.

If you see any errors in the TensorFlow.js operations panel, you can click on them to see more details.

#### Scenario: my application is running slowly

If your TensorFlow.js application is running slowly, the first thing to check is the browser console for warnings. The browser console can be opened with the DevTools "Console" tab.

If there are no warnings in the browser console, the next thing to check is the TensorFlow.js operations panel. This panel can be opened with the DevTools "Debugger for TensorFlow.js" tab.

If you see any warnings in the TensorFlow.js operations panel, you can click on them to see more details.

#### Scenario: my application is not using the GPU

If your TensorFlow.js application is not using the GPU, the first thing to check is the browser console for errors. The browser console can be opened with the DevTools "Console" tab.

If there are no errors in the browser console, the next thing to check is the TensorFlow.js operations panel. This panel can be opened with the DevTools "Debugger for TensorFlow.js" tab.

If you see any errors in the TensorFlow.js operations panel, you can click on them to see more details.

### Node.js

#### Scenario: my application is not running

If your Node.js application is not running, the first thing to check is the debugger console for errors. The debugger console can be opened with the Visual Studio Code "Debug" panel.

If there are no errors in the debugger console, the next thing to check is the Node.js operations panel. This panel can be opened with the Visual Studio Code "Node.js" panel.

If you see any errors in the Node.js operations panel, you can click on them to see more details.

#### Scenario: my application is running slowly

If your Node.js application is running slowly, the first thing to check is the debugger console for warnings. The debugger console can be opened with the Visual Studio Code "Debug" panel.

If there are no warnings in the debugger console, the next thing to check is the Node.js operations panel. This panel can be opened with the Visual Studio Code "Node.js" panel.

If you see any warnings in the Node.js operations panel, you can click on them to see more details.

#### Scenario: my application is not using the CPU

If your Node.js application is not using the CPU, the first thing to check is the debugger console for errors. The debugger console can be opened with the Visual Studio Code "Debug" panel.

If there are no errors in the debugger console, the next thing to check is the Node.js operations panel. This panel can be opened with the Visual Studio Code "Node.js" panel.

If you see any errors in the Node.js operations panel, you can click on them to see more details.

## Additional Information

### TensorFlow.js

For more information on debugging TensorFlow.js applications, see the TensorFlow.js debugging documentation.

### Node.js

For more information on debugging Node.js applications, see the Node.js debugging documentation.