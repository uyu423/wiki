---
title: 023：使用 TensorFlow.js 和 Node.js 生成文本
description: 
published: true
date: 2023-02-02T12:17:20.891Z
tags: 
editor: markdown
dateCreated: 2023-02-02T12:17:19.205Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [023: Text Generation with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/023-text-generation-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 生成文本

在本文中，我们将学习如何使用 TensorFlow.js 和 Node.js 生成文本。我们将使用 char-rnn 模型，这是一种循环神经网络 (RNN)，可以学习预测文本序列中的下一个字符。

## 什么是 char-rnn？

char-rnn 是一种 RNN，可以学习预测文本序列中的下一个字符。我们将使用的 char-rnn 模型基于论文“字符感知神经语言模型”(https://arxiv.org/abs/1508.06615) 中描述的模型。

## 什么是 TensorFlow.js？

TensorFlow.js 是一个 JavaScript 库，用于在浏览器和 Node.js 中训练和部署机器学习模型。

## 什么是 Node.js？

Node.js 是一个基于 Chrome 的 V8 JavaScript 引擎构建的 JavaScript 运行时。

## 入门

首先，我们需要安装 TensorFlow.js 和 Node.js。我们将使用 TensorFlow.js char-rnn 模型，它是一个 Node.js 模块。

```
npm install @tensorflow/tfjs-node
npm install @tensorflow/tfjs-node-charrnn
```

接下来，我们需要下载训练数据。对于此示例，我们将使用莎士比亚作品的数据集 (https://www.kaggle.com/kinguistics/shakespeare-plays)。

一旦我们有了训练数据，我们就可以开始训练 char-rnn 模型了。训练过程可能需要几分钟才能完成。

```
const tf = require('@tensorflow/tfjs-node');
const charRNN = require('@tensorflow/tfjs-node-charrnn');

const model = charRNN.create(
  'https://storage.googleapis.com/tfjs-models/tfjs/charrnn/data/shakespeare_input.txt',
  {
    rnnType: 'lstm',
    embeddingSize: 128,
    rnnUnits: 128,
    batchSize: 64,
    seqLength: 128,
    temperature: 0.8,
    numEpochs: 20
  });

model.fit().then(() => {
  // The model is trained!
});
```

一旦模型被训练好，我们就可以用它来生成文本。

```
model.generate('The').then((text) => {
  console.log(text);
});
```

## 附加信息

- 有关 TensorFlow.js 的更多信息，请参阅 TensorFlow.js 文档 (https://js.tensorflow.org/)。
- 有关 Node.js 的更多信息，请参阅 Node.js 文档 (https://nodejs.org/en/docs/)。