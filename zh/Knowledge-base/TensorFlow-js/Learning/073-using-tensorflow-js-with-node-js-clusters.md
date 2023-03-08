---
title: 073：将 TensorFlow.js 与 Node.js 集群结合使用
description: 
published: true
date: 2023-02-02T23:43:28.316Z
tags: 
editor: markdown
dateCreated: 2023-02-02T23:43:26.638Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [073: Using TensorFlow.js with Node.js Clusters***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/073-using-tensorflow-js-with-node-js-clusters)
{.links-list}


# 在 Node.js 集群中使用 TensorFlow.js

TensorFlow.js 是一个强大的工具，可用于在浏览器和 Node.js 服务器上训练和部署机器学习模型。在本文中，我们将了解如何将 TensorFlow.js 与 Node.js 集群结合使用。

## 什么是 TensorFlow.js？

TensorFlow.js 是一个用于机器学习的开源库，可以在浏览器和 Node.js 服务器上使用。它允许您在 JavaScript 中训练和部署机器学习模型。

## 什么是 Node.js 集群？

Node.js 集群是一种通过在一台机器上运行 Node.js 进程的多个实例来提高 Node.js 应用程序性能的方法。集群可用于提高 CPU 密集型任务的性能，例如机器学习。

## 如何将 TensorFlow.js 与 Node.js 集群一起使用

将 TensorFlow.js 与 Node.js 集群结合使用是提高机器学习应用程序性能的好方法。要将 TensorFlow.js 与 Node.js 集群一起使用，您需要使用 `cluster` 模块。

`cluster` 模块允许您创建一个 Node.js 进程集群。要使用“集群”模块，您需要创建一个主进程和工作进程。主进程负责创建工作进程。工作进程负责运行任务。

在您的应用程序中，您需要创建一个包含主进程代码的文件和一个包含工作进程代码的文件。主进程文件应如下所示：

```javascript
const cluster = require('cluster');

// The code for the master process

cluster.on('exit', (worker, code, signal) => {
  console.log(`worker ${worker.process.pid} died`);
});

```

工作进程文件应如下所示：

```javascript
const cluster = require('cluster');

// The code for the worker process

if (cluster.isWorker) {
  console.log(`I am a worker, my id is ${cluster.worker.id}`);
}

```

要运行您的应用程序，您需要使用 `cluster` 模块。例如，要在 4 个 worker 上运行您的应用程序，您可以使用以下命令：

```javascript
node master.js 4
```

## 附加信息

- 您可以在 [Node.js 文档](https://nodejs.org/api/cluster.html) 中找到有关 `cluster` 模块的更多信息。
- 您可以在 [TensorFlow.js 文档](https://js.tensorflow.org/) 中找到有关 TensorFlow.js 的更多信息。