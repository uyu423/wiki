---
title: 051：在 TensorFlow.js 和 Node.js 中使用回调
description: 
published: true
date: 2023-02-02T18:43:29.548Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:43:27.809Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [051: Using Callbacks with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/051-using-callbacks-with-tensorflow-js-and-node-js)
{.links-list}


# 在 TensorFlow.js 和 Node.js 中使用回调

TensorFlow.js 是一个强大的 JavaScript 机器学习工具。 Node.js 是一个 JavaScript 运行时，允许您在服务器上运行 JavaScript。在本文中，我们将向您展示如何在 TensorFlow.js 和 Node.js 中使用回调。

## 什么是回调？

回调是作为参数传递给另一个函数的函数。当另一个函数完成执行时调用回调函数。回调通常在 JavaScript 中用于执行异步操作。

## 在 TensorFlow.js 中使用回调

TensorFlow.js 提供了一个回调 API，允许您执行异步操作。回调 API 在 tf.tensor 类中可用。

要使用回调 API，您必须首先创建一个 `tf.tensor` 对象。 `tf.tensor` 类将数据数组和形状数组作为参数。数据数组是一个包含张量数据的 JavaScript 数组。形状数组是一个包含张量维度的 JavaScript 数组。

一旦创建了 `tf.tensor` 对象，就可以使用 .then() 方法注册回调函数。 .then() 方法将回调函数作为参数。当“tf.tensor”对象准备就绪时调用回调函数。

`.then()` 方法返回一个 `Promise` 对象。 `Promise` 对象表示 `.then()` 方法的结果。 `Promise` 对象有一个 `.then()` 方法，可以用来注册另一个回调函数。

以下是使用 .then() 方法注册回调函数的示例：

```javascript
const tensor = tf.tensor([1, 2, 3, 4], [2, 2]);

tensor.then(t => {
  // The callback function is called when the tensor is ready.
  // The tensor is passed as an argument to the callback function.
  // The tensor can be used in the callback function.
  console.log(t);
});
```

## 在 Node.js 中使用回调

Node.js 提供了一个回调 API，允许您执行异步操作。回调 API 在 fs 模块中可用。

`fs` 模块提供了一个用于与文件系统交互的 API。 `fs` 模块有一个 `readFile()` 方法，可用于异步读取文件。 `readFile()` 方法将文件路径和回调函数作为参数。读取文件时调用回调函数。文件数据作为参数传递给回调函数。

以下是使用 readFile() 方法异步读取文件的示例：

```javascript
const fs = require('fs');

fs.readFile('file.txt', (err, data) => {
  // The callback function is called when the file is read.
  // The file data is passed as an argument to the callback function.
  // The file data can be used in the callback function.
  console.log(data);
});
```

## 附加信息

- [使用承诺](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_promises)
- [Node.js 回调](https://nodejs.org/api/fs.html# fs_fs_readfile_path_options_callback)