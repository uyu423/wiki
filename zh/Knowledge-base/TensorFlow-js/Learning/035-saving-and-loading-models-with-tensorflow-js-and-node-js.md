---
title: 035：使用 TensorFlow.js 和 Node.js 保存和加载模型
description: 
published: true
date: 2023-02-02T15:17:20.462Z
tags: 
editor: markdown
dateCreated: 2023-02-02T15:17:18.812Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [035: Saving and Loading Models with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/035-saving-and-loading-models-with-tensorflow-js-and-node-js)
{.links-list}


## 使用 TensorFlow.js 和 Node.js 保存和加载模型

在本文中，我们将学习如何使用 TensorFlow.js 和 Node.js 保存和加载模型。我们将涵盖以下主题：

- 使用 TensorFlow.js 保存模型
- 使用 TensorFlow.js 加载模型
- 使用带有 Node.js 的模型

### 使用 TensorFlow.js 保存模型

第一步是保存我们的模型。我们可以使用 `tf.Model.save` 方法来做到这一点。此方法有两个参数：

- `path`: 保存模型的路径。
- `overwrite`: 一个布尔值，指示是否覆盖指定路径上的现有模型。

这是保存模型的示例：

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});

model.save('/tmp/model/1/model.json', true);
```

在此示例中，我们已将模型保存到“/tmp/model/1”目录。 `overwrite` 参数设置为 `true`，因此如果该目录中已有模型，它将被覆盖。

### 使用 TensorFlow.js 加载模型

现在我们已经保存了我们的模型，让我们学习如何加载它。我们可以使用 `tf.loadModel` 方法来做到这一点。此方法采用一个参数：

- `path`：保存模型的路径。

这是加载模型的示例：

```javascript
const model = await tf.loadModel('/tmp/model/1/model.json');
```

在这个例子中，我们从 /tmp/model/1 目录加载了我们的模型。

### 使用带有 Node.js 的模型

加载模型后，我们可以使用它进行预测。我们可以使用 model.predict 方法来做到这一点。此方法采用一个参数：

- `inputs`：进行预测的输入数据。这可以是单个“tf.Tensor”或“tf.Tensor”的“数组”。

下面是使用模型进行预测的示例：

```javascript
const input = tf.tensor2d([[1.0]]);
const output = model.predict(input);

output.print();
```

在此示例中，我们创建了一个值为“[[1.0]]”的“tf.Tensor”。我们已将此张量传递给 model.predict 方法，该方法返回一个预测。然后我们将预测打印到控制台。