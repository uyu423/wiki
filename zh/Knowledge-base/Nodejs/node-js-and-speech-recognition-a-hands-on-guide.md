---
title: Node.js 和语音识别：动手指南
description: 
published: true
date: 2023-02-02T06:36:44.586Z
tags: 
editor: markdown
dateCreated: 2023-02-02T06:36:43.020Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Node.js and Speech Recognition: A Hands-On Guide***English** document is available*](/en/Knowledge-base/Nodejs/node-js-and-speech-recognition-a-hands-on-guide)
{.links-list}


# Node.js 和语音识别：动手指南

### 介绍

在本文中，我们将探讨如何使用 Node.js 进行语音识别。我们将了解如何设置基本的 Node.js 项目，如何使用流行的“recognize-speech”库来识别语音，以及如何使用 Google Cloud Speech-to-Text 来识别语音。

我们还将研究如何使用这些工具构建可用于控制计算机的简单语音识别应用程序。

### 设置 Node.js 项目

在开始使用语音识别之前，我们需要设置一个 Node.js 项目。如果您以前从未使用过 Node.js，请不要担心 - 它非常容易上手。

首先，我们需要安装 Node.js。您可以通过访问 Node.js 网站并下载适用于您的操作系统的安装程序来执行此操作。

一旦安装了 Node.js，我们就可以创建一个新项目。为您的项目创建一个新目录，然后使用 npm 初始化项目：

```
$ mkdir my-project
$ cd my-project
$ npm init
```

这将在您的项目中创建一个“package.json”文件。此文件包含有关项目的元数据，包括项目所需的依赖项。

接下来，我们需要安装“recognize-speech”库。我们可以使用以下命令执行此操作：

```
$ npm install --save recognize-speech
```

这将安装“recognize-speech”库并将其添加到“package.json”文件的“dependencies”部分。

### 使用 `recognize-speech` 库识别语音

现在我们已经设置了一个基本的 Node.js 项目，我们可以开始使用“recognize-speech”库来识别语音。

`recognize-speech` 库提供了一个用于识别语音的简单 API。要使用它，我们首先需要创建一个“识别器”对象：

```javascript
var Recognizer = require('recognize-speech');

var recognizer = new Recognizer();
```

接下来，我们需要为 speech 事件注册一个事件处理程序：

```javascript
recognizer.on('speech', function(data) {
  // The data object contains the recognized text
  console.log(data.text);
});
```

最后，我们需要开始识别过程。我们可以通过调用 `recognize` 方法来做到这一点：

```javascript
recognizer.recognize('speech.wav');
```

这将启动识别过程并将识别的文本打印到控制台。

### 使用谷歌云语音转文本

Google Cloud Speech-to-Text 是一种基于云的语音识别服务，可用于识别语音。要使用它，我们首先需要创建一个“语音”对象：

```javascript
var Speech = require('@google-cloud/speech');

var speech = new Speech();
```

接下来，我们需要为 `data` 事件注册一个事件处理程序：

```javascript
speech.on('data', function(data) {
  // The data object contains the recognized text
  console.log(data.text);
});
```

最后，我们需要开始识别过程。我们可以通过调用 `recognize` 方法来做到这一点：

```javascript
speech.recognize('speech.wav');
```

这将启动识别过程并将识别的文本打印到控制台。

### 构建语音识别应用

现在我们已经了解了如何使用 Node.js 进行语音识别，让我们构建一个可用于控制计算机的简单语音识别应用程序。

该应用程序将使用“recognize-speech”库来识别语音，并使用“osascript”库来控制计算机。

首先，我们需要安装 `osascript` 库：

```
$ npm install --save osascript
```

接下来，我们需要在代码中引入 `osascript` 库：

```javascript
var osascript = require('osascript');
```

现在，我们可以编写 `recognize` 函数：

```javascript
function recognize(speech, callback) {
  // ...
}
```

此函数将语音录音作为输入并调用“recognize-speech”库的“recognize”方法。如果识别成功，它会用识别的文本调用`callback`函数。

最后，我们需要编写 `main` 函数：

```javascript
function main() {
  // ...
}
```

该函数将在应用程序启动时调用。它将创建一个“识别器”对象并为“语音”事件注册一个事件处理程序。

当 `speech` 事件被触发时，它会调用带有语音记录的 `recognize` 函数。如果识别成功，就会使用`osascript`库来控制电脑。

要运行该应用程序，我们可以使用以下命令：

```
$ node app.js
```

### 结论

在本文中，我们了解了如何使用 Node.js 进行语音识别。我们了解了如何设置基本的 Node.js 项目、如何使用“recognize-speech”库来识别语音以及如何使用 Google Cloud Speech-to-Text。

我们还了解了如何使用这些工具来构建可用于控制计算机的简单语音识别应用程序。