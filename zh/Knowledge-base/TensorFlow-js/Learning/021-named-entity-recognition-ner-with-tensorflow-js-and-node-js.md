---
title: 021：使用 TensorFlow.js 和 Node.js 的命名实体识别 (NER)
description: 
published: true
date: 2023-02-02T11:43:40.750Z
tags: 
editor: markdown
dateCreated: 2023-02-02T11:43:39.123Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [021: Named Entity Recognition (NER) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/021-named-entity-recognition-ner-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 的命名实体识别 (NER)

在本文中，我们将研究如何使用 TensorFlow.js 和 Node.js 在 JavaScript 中执行命名实体识别 (NER)。 NER 是自然语言处理 (NLP) 中的一项任务，涉及识别和分类文本中的命名实体，例如人、地点、组织等。

我们将使用在 CoNLL 2003 NER 数据集上训练的预训练模型。该模型是一个双向长短期记忆 (BiLSTM) 模型，顶部有一个条件随机场 (CRF) 层。

## 先决条件

为了跟进这篇文章，您需要以下内容：

- Node.js（版本 8 或更高版本）
- 文本编辑器或 IDE

## 入门

首先，让我们创建一个新的 Node.js 项目。我们将使用 Express Web 框架，因此我们也需要安装它：

```
npm init
npm install --save express
```

接下来，我们需要安装 TensorFlow.js NER 模型。我们可以使用以下命令来做到这一点：

```
npm install @tensorflow-models/ner
```

这样，我们就可以开始编码了！

## 加载模型

我们需要做的第一件事是加载模型。我们可以使用以下代码来做到这一点：

```javascript
const tf = require('@tensorflow/tfjs-node');
const model = require('@tensorflow-models/ner');

async function main() {
  const ner = await model.load();
}

main();
```

在上面的代码中，我们首先导入了 TensorFlow.js 和 NER 模型。然后我们创建了一个异步函数，它将加载模型并将其存储在一个变量中。

## 预测命名实体

现在我们已经加载了模型，我们可以使用它来预测文本中的命名实体。我们可以使用以下代码来做到这一点：

```javascript
const tf = require('@tensorflow/tfjs-node');
const model = require('@tensorflow-models/ner');

async function main() {
  const ner = await model.load();

  const text = 'John Smith is a software engineer at Google.';

  const results = await ner.predict(text);

  console.log(results);
}

main();
```

在上面的代码中，我们添加了一个文本字符串，我们希望为其预测命名实体。然后我们使用模型的“预测”方法来获得结果。

结果将是一个对象数组，每个对象代表一个命名实体。每个对象都有一个“start”和“end”属性，代表输入文本中命名实体的开始和结束索引，以及一个“score”属性，代表模型对预测的信心。

## 可视化结果

可视化预测结果可能会有所帮助。我们可以使用以下代码来做到这一点：

```javascript
const tf = require('@tensorflow/tfjs-node');
const model = require('@tensorflow-models/ner');

async function main() {
  const ner = await model.load();

  const text = 'John Smith is a software engineer at Google.';

  const results = await ner.predict(text);

  for (const result of results) {
    console.log(
        `${text.substring(result.start, result.end)} (${result.score})`);
  }
}

main();
```

在上面的代码中，我们添加了一个循环，该循环将打印出每个命名实体，以及模型对该预测的置信度分数。

## 结论

在本文中，我们了解了如何使用 TensorFlow.js 和 Node.js 在 JavaScript 中执行命名实体识别。我们还了解了如何可视化预测结果。

如果您有兴趣了解有关 NER 或 TensorFlow.js 的更多信息，以下资源可能会对您有所帮助：

- [使用 TensorFlow 进行命名实体识别（博客文章）](https://blog.tensorflow.org/2018/12/named-entity-recognition-ner-tensorflow.html)
- [TensorFlow.js NER 模型](https://js.tensorflow.org/tutorials/tensorflow-for-js-nerds.html)
- [CoNLL 2003 NER 数据集](https://www.clips.uantwerpen.be/conll2003/ner/)