---
title: 022：使用 TensorFlow.js 和 Node.js 进行语音识别
description: 
published: true
date: 2023-02-02T12:04:36.259Z
tags: 
editor: markdown
dateCreated: 2023-02-02T12:04:34.679Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [022: Speech Recognition with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/022-speech-recognition-with-tensorflow-js-and-node-js)
{.links-list}


# 022：使用 TensorFlow.js 和 Node.js 进行语音识别

在本文中，我们将研究如何使用 TensorFlow.js 和 Node.js 构建语音识别系统。

我们将从查看如何设置环境开始，然后我们将进入代码。

## 设置环境

我们需要做的第一件事是安装 TensorFlow.js。我们可以使用以下命令来做到这一点：

```
npm install @tensorflow/tfjs
```

完成后，我们需要为 TensorFlow.js 安装 Node.js 绑定。我们可以使用以下命令来做到这一点：

```
npm install @tensorflow/tfjs-node
```

有了这些，我们现在可以继续编写代码了。

## 代码

我们将从加载 TensorFlow.js 库和 Node.js 绑定开始。我们可以使用以下代码来做到这一点：

```javascript
const tf = require('@tensorflow/tfjs');
require('@tensorflow/tfjs-node');
```

接下来，我们需要加载语音识别库。我们可以使用以下代码来做到这一点：

```javascript
const speech = require('@tensorflow-models/speech-commands');
```

有了这个，我们现在可以继续有趣的部分：代码。

我们将从创建一个新的语音识别模型开始。我们可以使用以下代码来做到这一点：

```javascript
const model = speech.createModel();
```

接下来，我们需要训练模型。我们可以使用以下代码来做到这一点：

```javascript
model.train({
  fileNames: [
    'file1.wav',
    'file2.wav',
    'file3.wav',
  ],
  labels: [
    'label1',
    'label2',
    'label3',
  ]
});
```

训练好模型后，我们现在可以使用它来识别语音。我们可以使用以下代码来做到这一点：

```javascript
model.recognize(audio, (err, result) => {
  if (err) {
    console.error(err);
  } else {
    console.log(result);
  }
});
```

就是这样！你现在有一个工作的语音识别系统。

## 结论

在本文中，我们了解了如何使用 TensorFlow.js 和 Node.js 构建语音识别系统。我们首先研究了如何设置环境，然后才开始编写代码。

如果您有兴趣了解更多信息，我建议您查看以下资源：

- 官方 TensorFlow.js 文档：https://js.tensorflow.org/
- TensorFlow.js 文档的官方 Node.js 绑定：https://js.tensorflow.org/tfjs-node/
- 官方语音识别库文档：https://js.tensorflow.org/speech-commands/