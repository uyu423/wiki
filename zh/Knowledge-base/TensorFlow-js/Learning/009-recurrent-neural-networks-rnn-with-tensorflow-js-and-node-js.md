---
title: 009：使用 TensorFlow.js 和 Node.js 的递归神经网络 (RNN)
description: 
published: true
date: 2023-02-02T08:44:02.992Z
tags: 
editor: markdown
dateCreated: 2023-02-02T08:43:58.499Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [009: Recurrent Neural Networks (RNN) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/009-recurrent-neural-networks-rnn-with-tensorflow-js-and-node-js)
{.links-list}


# 介绍

递归神经网络 (RNN) 是一种非常适合处理顺序数据（例如文本、音频和视频）的神经网络。在本文中，我们将使用 TensorFlow.js 和 Node.js 构建一个可以逐字符生成新文本的 RNN。

# 设置项目

在我们开始之前，我们需要设置我们的项目。我们将使用 Node.js 的 Express Web 框架，所以首先我们需要安装它。

```
$ npm install express --save
```

接下来，我们需要安装 TensorFlow.js。我们将使用 Node.js API，因此我们需要安装“@tensorflow/tfjs-node”包。

```
$ npm install @tensorflow/tfjs-node --save
```

现在我们拥有了所需的所有依赖项，我们可以在项目的根目录中创建一个名为 index.js 的文件并开始编码。

# 构建循环神经网络

我们需要做的第一件事是加载我们将用于训练 RNN 的数据。我们将使用莎士比亚文本语料库，您可以在[此处](https://storage.googleapis.com/tfjs-examples/shakespeare.txt) 下载该语料库。

下载文本文件后，我们可以使用“fs”模块将其加载到我们的 Node.js 程序中。

```javascript
const fs = require('fs');

const text = fs.readFileSync('shakespeare.txt', 'utf8');
```

现在我们已经加载了文本，我们需要对其进行预处理，以使其适合训练我们的 RNN。我们将从将所有字符转换为小写并删除所有非字母数字字符开始。

```javascript
const text = text.toLowerCase();
const text = text.replace(/[^a-zA-Z0-9]/g, '');
```

接下来，我们需要将文本拆分为单个字符的数组。

```javascript
const chars = Array.from(text);
```

现在我们已经对文本进行了预处理，我们可以开始构建我们的 RNN。我们将使用长短期记忆 (LSTM) 单元，这是一种非常适合处理顺序数据的 RNN 单元。

我们可以使用以下代码在 TensorFlow.js 中创建一个 LSTM 单元：

```javascript
const lstmCell = tf.layers.lstmCell({
  units: 512,
  recurrentInputSize: 512,
  inputShape: [1, chars.length],
  kernelInitializer: 'glorotNormal',
  recurrentInitializer: 'orthogonal',
  biasInitializer: 'zeros',
  unitForgetBias: true,
  activation: 'tanh',
  recurrentActivation: 'sigmoid',
  useBias: true,
  kernelRegularizer: null,
  recurrentRegularizer: null,
  biasRegularizer: null,
  activityRegularizer: null,
  kernelConstraint: null,
  recurrentConstraint: null,
  biasConstraint: null,
  dropout: 0.0,
  recurrentDropout: 0.0
});
```

接下来，我们需要创建 RNN 本身。我们可以使用以下代码来做到这一点：

```javascript
const rnn = tf.layers.rnn({
  cell: lstmCell,
  inputShape: [1, chars.length],
  returnSequences: true,
  goBackwards: false,
  stateful: false,
  unroll: false
});
```

现在我们已经创建了 RNN，我们需要编译它。我们将使用 Adam 优化器和分类交叉熵作为我们的损失函数。

```javascript
rnn.compile({
  optimizer: 'adam',
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy']
});
```

# 训练 RNN

现在我们的 RNN 已经编译好了，我们可以开始训练它了。我们首先需要创建一些训练数据。我们将创建一个单热编码字符数组，其中每个字符都由一个零向量表示，索引中的 1 对应于该字符。

```javascript
const chars = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'];

const oneHotChars = [];

for (let i = 0; i < chars.length; i++) {
  const char = chars[i];
  const oneHotChar = [];

  for (let j = 0; j < chars.length; j++) {
    if (j === i) {
      oneHotChar.push(1.0);
    } else {
      oneHotChar.push(0.0);
    }
  }

  oneHotChars.push(oneHotChar);
}
```

现在我们有了 one-hot 编码的字符，我们需要创建我们的训练数据。我们将创建一组训练示例，其中每个训练示例都是一对单热编码字符。对中的第一个字符将是输入字符，第二个字符将是输出字符。

```javascript
const trainingData = [];

for (let i = 0; i < text.length - 1; i++) {
  const inputChar = oneHotChars[chars.indexOf(text[i])];
  const outputChar = oneHotChars[chars.indexOf(text[i + 1])];

  trainingData.push([inputChar, outputChar]);
}
```

现在我们有了训练数据，可以训练我们的 RNN 了。我们将训练它 10 个时期，并使用 32 的批量大小。

```javascript
rnn.fit(trainingData, {
  epochs: 10,
  batchSize: 32
});
```

# 生成文本

现在我们的 RNN 已经训练好了，我们可以用它来生成新的文本。我们将从创建一个接受一个字符并返回下一个字符的函数开始。

```javascript
function nextChar(char) {
  const oneHotChar = oneHotChars[chars.indexOf(char)];
  const output = rnn.predict(tf.tensor2d([oneHotChar], [1, oneHotChar.length]));
  const index = output.argMax(1).dataSync()[0];
  const nextChar = chars[index];

  return nextChar;
}
```

现在我们可以使用我们的 `nextChar` 函数来生成新的文本。我们将从字符“a”开始并生成 1000 个字符。

```javascript
let text = 'a';

for (let i = 0; i < 1000; i++) {
  text += nextChar(text[text.length - 1]);
}

console.log(text);
```

就是这样！您现在有了一个可以逐个字符生成新文本的有效 RNN。

# 附加信息

如果您有兴趣了解有关 RNN 的更多信息，我推荐以下资源：

- [TensorFlow 中的递归神经网络](https://www.tensorflow.org/tutorials/sequences/recurrent)
- [理解 LSTM 网络](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
- [使用 TensorFlow 构建循环神经网络](https://www.oreilly.com/learning/building-a-recurrent-neural-network-with-tensorflow)