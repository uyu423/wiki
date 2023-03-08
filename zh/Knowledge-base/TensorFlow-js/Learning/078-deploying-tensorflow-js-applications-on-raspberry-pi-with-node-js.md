---
title: 078：使用 Node.js 在 Raspberry Pi 上部署 TensorFlow.js 应用程序
description: 
published: true
date: 2023-02-03T01:04:40.419Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:04:38.863Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [078: Deploying TensorFlow.js Applications on Raspberry Pi with Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/078-deploying-tensorflow-js-applications-on-raspberry-pi-with-node-js)
{.links-list}


## 介绍

Raspberry Pi 是一款信用卡大小的计算机，可用于各种电子项目。其应用范围广泛，可用于教育、工业、科研等各个领域。

Raspberry Pi 最流行的应用之一是将其用作机器学习的边缘设备。 TensorFlow.js 是一个用于训练和部署机器学习模型的 JavaScript 库。

在本文中，我们将指导您完成为 TensorFlow.js 设置 Raspberry Pi 的过程。我们还将向您展示如何在 Raspberry Pi 上部署 TensorFlow.js 应用程序。

## 设置树莓派

您需要做的第一件事是设置您的 Raspberry Pi。您可以按照此链接中的说明进行操作：https://www.raspberrypi.org/documentation/setup/

设置好 Raspberry Pi 后，您需要在其上安装 Node.js。 Node.js 是运行 TensorFlow.js 应用程序所需的 JavaScript 运行时。

您可以按照此链接中的说明在 Raspberry Pi 上安装 Node.js：https://nodejs.org/en/download/package-manager/# installing-node-js-via-package-manager

## 部署 TensorFlow.js 应用程序

安装 Node.js 后，您现在可以在 Raspberry Pi 上部署 TensorFlow.js 应用程序。

有两种部署 TensorFlow.js 应用程序的方法：

1. 使用网络服务器为应用程序提供服务。
2. 使用命令行工具部署应用程序。

### 使用 Web 服务器

第一种方法是使用 Web 服务器来为应用程序提供服务。我们将使用 Node.js Web 服务器 Express.js。

Express.js 是 Node.js 的 Web 应用程序框架。它用于构建 Web 应用程序和 API。

您可以通过运行以下命令来安装 Express.js：

```
npm install express --save
```

安装 Express.js 后，您可以创建一个名为 app.js 的文件并向其中添加以下代码：

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello world!');
});

app.listen(3000, () => console.log('Example app listening on port 3000!'));
```

此代码创建一个 Web 服务器，该服务器使用字符串“Hello world!”响应 HTTP 请求。

您可以通过运行以下命令来启动 Web 服务器：

```
node app.js
```

您现在可以通过 http://localhost:3000 访问 Web 服务器。

### 使用命令行工具

第二种方法是使用命令行工具来部署应用程序。我们将使用 TensorFlow.js CLI。

TensorFlow.js CLI 是一个命令行工具，可用于训练、部署和使用 TensorFlow.js 模型。

您可以通过运行以下命令来安装 TensorFlow.js CLI：

```
npm install -g @tensorflow/tfjs-node
```

安装 TensorFlow.js CLI 后，您可以使用它来部署 TensorFlow.js 应用程序。

假设您在 app 目录中有一个 TensorFlow.js 应用程序。您可以通过运行以下命令来部署应用程序：

```
tfjs deploy --dir app
```

这将启动一个为 TensorFlow.js 应用程序提供服务的 Web 服务器。您可以在 http://localhost:3000 访问该应用程序。

## 结论

在本文中，我们向您展示了如何在 Raspberry Pi 上部署 TensorFlow.js 应用程序。我们还向您展示了如何使用 Web 服务器来为应用程序提供服务。