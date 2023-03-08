---
title: 使用 Node.js Worker 进行并发处理
description: 
published: true
date: 2023-02-05T06:17:28.584Z
tags: 
editor: markdown
dateCreated: 2023-02-05T06:17:23.244Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Working with Node.js Workers for Concurrent Processing***English** document is available*](/en/Knowledge-base/Nodejs/working-with-node-js-workers-for-concurrent-processing)
{.links-list}


# 使用 Node.js Worker 进行并发处理

在本文中，我们将讨论如何使用 Node.js worker 进行并发处理。

并发处理是并行的一种形式，其中多个处理单元同时处理任务的不同部分。在计算机编程中，这通常是通过将任务分成可以并行执行的更小的子任务来实现的。

Node.js 是一个基于 V8 JavaScript 引擎构建的 JavaScript 运行时，允许并发处理。 Node.js worker 是独立的进程，可以独立于 Node.js 主进程运行。这些 worker 可用于执行 CPU 密集型任务，例如图像处理或数据加密。

在 Node.js 中有两种创建 worker 的方法：

- 使用 `child_process.fork()` 方法创建一个新进程。
- 使用 `cluster` 模块创建一个 worker。

`child_process.fork()` 方法是创建工人的推荐方法。此方法允许您在父进程和子进程之间传递数据，它还提供了一个用于在进程之间发送消息的 send() 方法。

`cluster` 模块是一个允许您创建工作人员的内置模块。如果您需要创建大量工作人员，集群模块会很有帮助。

## 创建工人

让我们首先使用 `child_process.fork()` 方法创建一个 worker。

```javascript
const {fork} = require('child_process');

const worker = fork('worker.js');
```

上面的代码通过调用 `fork()` 方法创建了一个新进程。 `fork()` 方法获取将在新进程中执行的 JavaScript 文件的路径。在这种情况下，我们将路径传递给 `worker.js` 文件。

`worker.js` 文件包含以下代码：

```javascript
console.log('Worker started');

process.on('message', (message) => {
  console.log(`Message from parent: ${message}`);
});

process.send('Hello from the child!');
```

上面的代码为“消息”事件设置了一个侦听器。当父进程向子进程发送消息时会触发此事件。侦听器将消息记录到控制台。

子进程还使用 send() 方法向父进程发送消息。

## 发送消息

既然我们已经了解了如何创建worker并在父子进程之间发送消息，那么让我们看一下如何从父进程向子进程发送消息。

```javascript
worker.send('Hello from the parent!');
```

上面的代码从父进程向子进程发送消息。该消息将由我们在 worker.js 文件中创建的 message 事件侦听器接收。

## 处理错误

与工人一起工作时处理错误很重要。否则，错误将不会被注意到并可能导致意外行为。

要处理子进程中的错误，您可以使用 `error` 事件：

```javascript
worker.on('error', (err) => {
  console.error(err);
});
```

上面的代码在子进程上设置了一个 `error` 事件监听器。当子进程中出现错误时会发出此事件。侦听器将错误记录到控制台。

## 终止工人

您可以使用 `kill()` 方法终止一个 worker：

```javascript
worker.kill();
```

上面的代码终止了工作进程。

## 概括

在本文中，我们了解了如何使用 Node.js worker 进行并发处理。我们还了解了如何创建工作程序、在父进程和子进程之间发送消息以及处理错误。