---
title: 096：在 TensorFlow.js 和 Node.js 中构建门控循环单元 (GRU)
description: 
published: true
date: 2023-02-03T05:38:01.199Z
tags: 
editor: markdown
dateCreated: 2023-02-03T05:37:59.443Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [096: Building Gated Recurrent Units (GRUs) in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/096-building-gated-recurrent-units-grus-in-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 和 Node.js 中的 GRU

## 什么是 GRU？

门控循环单元 (GRU) 是一种循环神经网络 (RNN)，旨在更好地捕获顺序数据中的长期依赖性。与传统的 RNN 不同，GRU 有两个门控制信息流入和流出隐藏状态。更新门决定让多少新信息进入，而重置门决定遗忘多少旧信息。

## 在 TensorFlow.js 中构建 GRU

TensorFlow.js 是一个 JavaScript 库，用于在浏览器和 Node.js 中训练和部署机器学习模型。在本教程中，我们将了解如何在 TensorFlow.js 中构建 GRU 并使用它来预测序列中的下一个单词。

### 安装 TensorFlow.js

如果您在浏览器中运行本教程，则可以使用以下脚本标签安装 TensorFlow.js：

```
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest"></script>
```

如果您在 Node.js 中运行本教程，则可以使用以下命令安装 TensorFlow.js：

```
npm install @tensorflow/tfjs
```

### 加载数据

我们将在本教程中使用亚马逊产品评论的数据集。该数据集包含不同产品的评论，以及每个评论的星级。

我们首先需要将数据集加载到 TensorFlow.js 中。我们可以使用 `tf.data.csv` 函数来做到这一点：

```
const dataset = tf.data.csv('https://storage.googleapis.com/tfjs-datasets/amazon_reviews_multilingual_CSV_V2/reviews.csv', {
  columnConfigs: {
    review_body: {
      isLabel: true
    },
    review_title: {
      isLabel: true
    },
    star_rating: {
      isLabel: true
    }
  }
});
```

### 预处理数据

在训练模型之前，我们需要对数据进行预处理。我们需要执行以下预处理步骤：

- 将评论标记为句子。
- 将句子标记为单词。
- 将单词转换为整数。

我们可以使用 `tf.tokenize` 和 `tf.tensorize` 函数分别对评论进行分词并将其转换为整数。

```
const sentences = dataset.map(({review_body, review_title}) => tf.tokenize(review_body + ' ' + review_title));

const words = sentences.map(sentence => tf.tensor1d(sentence, 'int32'));
```

### 构建模型

我们现在准备构建我们的模型。我们将在本教程中使用 GRU。我们模型中的第一层将是“嵌入”层。该层将接受我们的单词并将它们转换为特定大小的向量。我们可以使用“inputDim”和“outputDim”参数指定向量的大小。我们还需要指定 `maskZero` 参数，它告诉图层忽略值为 0 的单词（即填充）。

```
const model = tf.sequential();
model.add(tf.layers.embedding({
  inputDim: 10000,
  outputDim: 64,
  maskZero: true
}));
```

我们模型中的下一层将是 GRU 层。该层将获取“嵌入”层输出的向量，并将它们转换为单个向量，以捕获序列中的信息。我们可以使用 units 参数指定隐藏状态的大小。

```
model.add(tf.layers.gru({
  units: 64,
  returnSequences: true,
  recurrentInitializer: 'glorotUniform'
}));
```

我们模型中的最后一层将是一个“密集”层。该层将获取 GRU 层输出的向量，并将其转换为我们词汇表中单词的概率分布。我们可以使用 units 参数指定图层中的单元数。我们还需要指定 `activation` 和 `kernelInitializer` 参数。 `activation` 参数指定要使用的激活函数，而 `kernelInitializer` 参数指定层权重的初始化器。

```
model.add(tf.layers.dense({
  units: 10000,
  activation: 'softmax',
  kernelInitializer: 'glorotUniform'
}));
```

### 编译模型

在我们训练我们的模型之前，我们需要编译它。我们需要在编译模型时指定以下参数：

- 要使用的优化器。我们将在本教程中使用 `adam` 优化器。
- 要使用的损失函数。我们将在本教程中使用 categoricalCrossentropy 损失函数。
- 要跟踪的指标。我们将跟踪本教程的“准确度”指标。

```
model.compile({
  optimizer: 'adam',
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy']
});
```

### 训练模型

我们现在准备好训练我们的模型了。我们可以使用 `model.fit` 方法来做到这一点。在训练模型时，我们需要指定以下参数：

- 训练数据。这应该是一个“tf.data.Dataset”对象。
- 要训练的时期数。我们将为本教程训练 10 个 epoch。
- 要使用的批量大小。在本教程中，我们将使用 32 的批量大小。

我们还可以指定一个“validationData”参数。这应该是一个包含验证数据的“tf.data.Dataset”对象。如果我们指定一个 validationData 参数，模型将在每个 epoch 结束时根据验证数据进行评估。

```
model.fit(words, {
  epochs: 10,
  batchSize: 32,
  validationData: words
});
```

### 进行预测

我们可以使用训练有素的模型对新数据进行预测。在我们做出预测之前，我们需要将新数据标记化并将其转换为整数。我们可以使用 `tf.tokenize` 和 `tf.tensorize` 函数来做到这一点：

```
const newSentences = tf.tokenize('this is a new sentence');
const newWords = tf.tensor1d(newSentences, 'int32');
```

然后我们可以使用 model.predict 方法对新数据进行预测：

```
model.predict(newWords).print();
```

## 在 Node.js 中构建 GRU

在本节中，我们将了解如何在 Node.js 中构建 GRU。我们将使用与上一节相同的亚马逊产品评论数据集。

### 安装依赖项

在开始编码之前，我们需要安装以下依赖项：

- `@tensorflow/tfjs-node`：这是 TensorFlow.js Node.js 绑定。
- `csv-parser`：这是一个用于 Node.js 的 CSV 解析器。
- `tokenizer`：这是 Node.js 的自然语言处理库。

我们可以使用以下命令安装这些依赖项：

```
npm install @tensorflow/tfjs-node csv-parser tokenizer
```

### 加载数据

我们将从将数据集加载到内存中开始。我们可以使用 `csv-parser` 库来做到这一点：

```
const parser = csvParser();

parser.on('data', (data) => {
  // do something with the data
});

parser.on('end', () => {
  // do something when the parsing is finished
});

fs.createReadStream('reviews.csv').pipe(parser);
```

### 预处理数据

在训练模型之前，我们需要对数据进行预处理。我们需要执行以下预处理步骤：

- 将评论标记为句子。
- 将句子标记为单词。
- 将单词转换为整数。

我们可以使用 `tokenizer` 库将评论标记为句子和单词。然后我们可以使用 tf.tensor1d 函数将单词转换为整数：

```
const sentences = reviews.map((review) => tokenizer.sentences(review));

const words = sentences.map((sentence) => tf.tensor1d(sentence.map((word) => tokenizer.words(word))));
```

### 构建模型

我们现在准备构建我们的模型。我们将在本教程中使用 GRU。我们模型中的第一层将是“嵌入”层。该层将接受我们的单词并将它们转换为特定大小的向量。我们可以使用“inputDim”和“outputDim”参数指定向量的大小。我们还需要指定 `maskZero` 参数，它告诉图层忽略值为 0 的单词（即填充）。

```
const model = tf.sequential();
model.add(tf.layers.embedding({
  inputDim: 10000,
  outputDim: 64,
  maskZero: true
}));
```

我们模型中的下一层将是 GRU 层。该层将获取“嵌入”层输出的向量，并将它们转换为单个向量，以捕获序列中的信息。我们可以使用 units 参数指定隐藏状态的大小。

```
model.add(tf.layers.gru({
  units: 64,
  returnSequences: true,
  recurrentInitializer: 'glorotUniform'
}));
```

我们模型中的最后一层将是一个“密集”层。该层将获取 GRU 层输出的向量，并将其转换为我们词汇表中单词的概率分布。我们可以使用 units 参数指定图层中的单元数。我们还需要指定 `activation` 和 `kernelInitializer` 参数。 `activation` 参数指定要使用的激活函数，而 `kernelInitializer` 参数指定层权重的初始化器。

```
model.add(tf.layers.dense({
  units: 10000,
  activation: 'softmax',
  kernelInitializer: 'glorotUniform'
}));
```

### 编译模型

在我们训练我们的模型之前，我们需要编译它。我们需要在编译模型时指定以下参数：

- 要使用的优化器。我们将在本教程中使用 `adam` 优化器。
- 要使用的损失函数。我们将在本教程中使用 categoricalCrossentropy 损失函数。
- 要跟踪的指标。我们将跟踪本教程的“准确度”指标。

```
model.compile({
  optimizer: 'adam',
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy']
});
```

### 训练模型

我们现在准备好训练我们的模型了。我们可以使用 `model.fit` 方法来做到这一点。在训练模型时，我们需要指定以下参数：

- 训练数据。这应该是一个“tf.data.Dataset”对象。
- 要训练的时期数。我们将为本教程训练 10 个 epoch。
- 要使用的批量大小。在本教程中，我们将使用 32 的批量大小。

我们还可以指定一个“validationData”参数。这应该是一个包含验证数据的“tf.data.Dataset”对象。如果我们指定一个 validationData 参数，模型将在每个 epoch 结束时根据验证数据进行评估。

```
model.fit(words, {
  epochs: 10,
  batchSize: 32,
  validationData: words
});
```

### 进行预测

我们可以使用训练有素的模型对新数据进行预测。在我们做出预测之前，我们需要将新数据标记化并将其转换为整数。我们可以使用 `tokenizer` 和 `tf.tensor1d` 库来做到这一点：

```
const newSentences = tokenizer.sentences('this is a new sentence');
const newWords = tf.tensor1d(newSentences.map((sentence) => tokenizer.words(sentence)));
```

然后我们可以使用 model.predict 方法对新数据进行预测：

```
model.predict(newWords).print();
```

## 资源

- [门控循环单元](https://en.wikipedia.org/wiki/Gated_recurrent_unit)
- [TensorFlow.js](https://js.tensorflow.org/)
- [用于 Node.js 的 TensorFlow.js](https://js.tensorflow.org/api/latest/# tensorflowjs_node)
- [csv-解析器](https://www.npmjs.com/package/csv-parser)
- [分词器](https://www.npmjs.com/package/tokenizer)