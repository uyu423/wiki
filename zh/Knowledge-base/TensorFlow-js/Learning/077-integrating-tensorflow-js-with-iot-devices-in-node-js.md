---
title: 077：在 Node.js 中将 TensorFlow.js 与物联网设备集成
description: 
published: true
date: 2023-02-03T00:43:19.807Z
tags: 
editor: markdown
dateCreated: 2023-02-03T00:43:18.157Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [077: Integrating TensorFlow.js with IoT Devices in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/077-integrating-tensorflow-js-with-iot-devices-in-node-js)
{.links-list}


# 在 Node.js 中将 TensorFlow.js 与物联网设备集成

TensorFlow.js 是一个开源库，可用于在浏览器中开发和训练机器学习模型。它还可用于在物联网设备上运行这些模型。在本文中，我们将展示如何结合使用 TensorFlow.js 和 Node.js 来开发可用于控制 IoT 设备的应用程序。

## 先决条件

在我们开始之前，您需要做一些事情：

- 对 JavaScript 有基本的了解
- Node.js 安装在你的电脑上
- 文本编辑器（我们推荐 [Visual Studio Code](https://code.visualstudio.com/)）

## 入门

我们将使用 [TensorFlow.js](https://js.tensorflow.org/) 库来开发我们的应用程序。我们需要做的第一件事是在我们的项目中包含 TensorFlow.js 库。我们可以通过将以下代码行添加到我们的 HTML 文件的头部来做到这一点：

```
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.0"> </script>
```

现在我们的项目中包含了 TensorFlow.js 库，我们可以开始开发我们的应用程序了。

## 开发应用程序

我们的应用程序将是一个简单的应用程序，它使用预训练模型来控制 IoT 设备。我们需要做的第一件事是加载模型。我们可以使用 tf.loadModel() 函数来做到这一点：

```javascript
const model = await tf.loadModel('https://my-model-url');
```

接下来，我们需要为我们的模型定义输入和输出。我们可以使用 tf.layers.input() 和 tf.layers.dense() 函数来做到这一点：

```javascript
const input = tf.layers.input({shape: [1]});
const output = tf.layers.dense({units: 1, activation: 'sigmoid'}).apply(input);
```

现在我们已经加载了模型并定义了输入和输出，我们可以编写实际控制 IoT 设备的代码。我们将通过创建一个接受输入并使用模型预测输出的函数来做到这一点：

```javascript
async function predict(input) {
  const output = model.predict(input);
  return output;
}
```

最后，我们需要编写代码来调用 predict() 函数并使用输出来控制 IoT 设备。我们将使用 Node.js [serialport](https://serialport.io/) 库来完成此操作：

```javascript
const SerialPort = require('serialport');
const Readline = require('@serialport/parser-readline');

const port = new SerialPort('/dev/ttyACM0', {
  baudRate: 9600
});

const parser = port.pipe(new Readline({ delimiter: '\r\n' }));

parser.on('data', async line => {
  const input = parseFloat(line);
  const output = await predict(input);
  port.write(output);
});
```

## 结论

在本文中，我们展示了如何结合使用 TensorFlow.js 和 Node.js 来开发可用于控制 IoT 设备的应用程序。我们只是初步了解了 TensorFlow.js 和 IoT 的可能性，但我们希望这能让您领略到可能性并激发您进一步探索。