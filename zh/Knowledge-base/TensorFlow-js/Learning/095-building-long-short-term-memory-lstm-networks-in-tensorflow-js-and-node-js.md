---
title: 095：在 TensorFlow.js 和 Node.js 中构建长短期记忆 (LSTM) 网络
description: 
published: true
date: 2023-02-03T05:17:55.550Z
tags: 
editor: markdown
dateCreated: 2023-02-03T05:17:53.921Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [095: Building Long Short-Term Memory (LSTM) Networks in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/095-building-long-short-term-memory-lstm-networks-in-tensorflow-js-and-node-js)
{.links-list}


# 095：在 TensorFlow.js 和 Node.js 中构建长短期记忆 (LSTM) 网络

在本文中，我们将研究如何在 TensorFlow.js 和 Node.js 中构建长短期记忆 (LSTM) 网络。

LSTM 是一种循环神经网络，非常适合处理顺序数据。顺序数据是每个元素都依赖于前一个元素的数据，例如时间序列数据。

LSTM 能够通过使用可以长时间记住信息的“记忆”单元来学习长期依赖关系。 LSTM 还能够处理与输出元素顺序不同的输入元素，这对于处理时间序列数据很重要。

## 在 TensorFlow.js 中构建 LSTM 网络

我们将从了解如何在 TensorFlow.js 中构建 LSTM 网络开始。

首先，我们需要安装 TensorFlow.js。我们可以使用 Node.js 包管理器 npm 来做到这一点：

```
npm install @tensorflow/tfjs
```

接下来，我们需要创建一个名为 `lstm.js` 的新文件并导入 TensorFlow.js：

```javascript
const tf = require('@tensorflow/tfjs');
```

现在我们准备开始构建我们的 LSTM 网络。

我们将从定义模型开始：

```javascript
const model = tf.sequential();
```

接下来，我们将向模型添加一个 LSTM 层。 `tf.layers.lstm` 函数的第一个参数是单元数，即 LSTM 层中的记忆单元数。我们将使用 16 个单位：

```javascript
model.add(tf.layers.lstm({units: 16, inputShape: [1, 1]}));
```

`inputShape` 参数是输入数据的形状。第一个元素是时间步数，第二个元素是特征数。在我们的例子中，我们有一个时间步长和一个特征。

接下来，我们将向模型添加一个致密层。这是一个标准的全连接层，将输出单个值：

```javascript
model.add(tf.layers.dense({units: 1}));
```

现在我们需要编译模型。我们需要指定损失函数和优化器。我们将使用均方误差损失函数和 Adam 优化器：

```javascript
model.compile({loss: 'meanSquaredError', optimizer: 'adam'});
```

我们现在准备好训练模型了。我们将使用 `tf.tensor2d` 来指定训练数据。第一个参数是数据，第二个参数是数据的形状。在我们的例子中，我们有两个训练示例，每个都有一个时间步长和一个特征：

```javascript
const xs = tf.tensor2d([[1], [2]]);
const ys = tf.tensor2d([[1], [2]]);
```

我们将训练模型 10 个时期，这是模型将看到训练数据的次数：

```javascript
model.fit(xs, ys, {epochs: 10});
```

一旦模型被训练好，我们就可以用它来进行预测。我们将使用 `tf.tensor2d` 来指定输入数据。在我们的例子中，我们有一个时间步长和一个特征：

```javascript
const xs = tf.tensor2d([[3]]);
```

然后我们可以调用 `model.predict` 方法进行预测：

```javascript
model.predict(xs).print();
```

这将输出预测，这是一个单一的值。

## 在 Node.js 中构建 LSTM 网络

我们现在来看看如何在 Node.js 中构建 LSTM 网络。

首先，我们需要安装 TensorFlow.js。我们可以使用 Node.js 包管理器 npm 来做到这一点：

```
npm install @tensorflow/tfjs
```

接下来，我们需要创建一个名为 `lstm.js` 的新文件并导入 TensorFlow.js：

```javascript
const tf = require('@tensorflow/tfjs');
```

现在我们准备开始构建我们的 LSTM 网络。

我们将从定义模型开始：

```javascript
const model = tf.sequential();
```

接下来，我们将向模型添加一个 LSTM 层。 `tf.layers.lstmLayer` 函数的第一个参数是单元数，即 LSTM 层中的记忆单元数。我们将使用 16 个单位：

```javascript
model.add(tf.layers.lstmLayer({units: 16, inputShape: [1, 1]}));
```

`inputShape` 参数是输入数据的形状。第一个元素是时间步数，第二个元素是特征数。在我们的例子中，我们有一个时间步长和一个特征。

接下来，我们将向模型添加一个致密层。这是一个标准的全连接层，将输出单个值：

```javascript
model.add(tf.layers.denseLayer({units: 1}));
```

现在我们需要编译模型。我们需要指定损失函数和优化器。我们将使用均方误差损失函数和 Adam 优化器：

```javascript
model.compile({loss: 'meanSquaredError', optimizer: 'adam'});
```

我们现在准备好训练模型了。我们将使用 `tf.tensor2d` 来指定训练数据。第一个参数是数据，第二个参数是数据的形状。在我们的例子中，我们有两个训练示例，每个都有一个时间步长和一个特征：

```javascript
const xs = tf.tensor2d([[1], [2]]);
const ys = tf.tensor2d([[1], [2]]);
```

我们将训练模型 10 个时期，这是模型将看到训练数据的次数：

```javascript
model.fit(xs, ys, {epochs: 10});
```

一旦模型被训练好，我们就可以用它来进行预测。我们将使用 `tf.tensor2d` 来指定输入数据。在我们的例子中，我们有一个时间步长和一个特征：

```javascript
const xs = tf.tensor2d([[3]]);
```

然后我们可以调用 `model.predict` 方法进行预测：

```javascript
model.predict(xs).print();
```

这将输出预测，这是一个单一的值。

## 结论

在本文中，我们了解了如何在 TensorFlow.js 和 Node.js 中构建长短期记忆 (LSTM) 网络。 LSTM 是一种循环神经网络，非常适合处理顺序数据。

如果您有兴趣了解有关 LSTM 的更多信息，我推荐以下资源：

- [递归神经网络的不合理有效性](https://karpathy.github.io/2015/05/21/rnn-effectiveness/)
- [理解 LSTM 网络](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
- [长短期记忆](https://en.wikipedia.org/wiki/Long_short-term_memory)