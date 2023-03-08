---
title: 052：使用 TensorFlow.js 和 Node.js 的自定义回调
description: 
published: true
date: 2023-02-02T19:04:49.187Z
tags: 
editor: markdown
dateCreated: 2023-02-02T19:04:47.423Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [052: Custom Callbacks with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/052-custom-callbacks-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 的自定义回调

在本文中，我们将学习如何使用 TensorFlow.js 和 Node.js 创建自定义回调。

TensorFlow.js 是一个强大的 JavaScript 机器学习工具。它允许您在浏览器或 Node.js 中创建、训练和部署机器学习模型。

Node.js 是一个 JavaScript 运行时，允许您在服务器上运行 JavaScript 代码。 Node.js 也是 TensorFlow.js 的一个重要平台，因为它允许您将机器学习模型部署到生产环境中。

使用 TensorFlow.js 创建自定义回调是扩展机器学习模型功能的好方法。回调允许您定义在训练过程中的特定点执行的自定义函数。例如，您可以使用回调来跟踪训练损失，或在每个时期后保存模型。

在本文中，我们将学习如何使用 TensorFlow.js 和 Node.js 创建自定义回调。我们还将学习如何使用回调来跟踪训练损失并在每个时期后保存模型。

## 什么是回调？

回调是在训练过程中的特定点执行的函数。回调是扩展机器学习模型功能的有效方式。

TensorFlow.js 中有两种类型的回调：

* **层回调：**这些回调在创建层时执行。
* **模型回调：**这些回调在模型编译和训练开始时执行。

在这篇文章中，我们将重点关注模型回调。

## 创建自定义回调

使用 TensorFlow.js 创建自定义回调很简单。首先，我们需要创建一个新的 JavaScript 文件并导入 TensorFlow.js 库。

接下来，我们需要创建一个扩展 Callback 类的新类。此类将包含我们的自定义回调函数。

在我们的示例中，我们将创建一个自定义回调来跟踪训练损失并在每个时期后保存模型。

```javascript
const tf = require('@tensorflow/tfjs');

class CustomCallback extends tf.Callback {
  onTrainBegin(logs) {
    // This function is executed when training begins.
    // We can use it to initialize our custom variables.
    this.losses = [];
  }

  onTrainEnd(logs) {
    // This function is executed when training ends.
    // We can use it to save our custom variables.
    console.log('Final loss: ', this.losses[-1]);
  }

  onBatchEnd(batch, logs) {
    // This function is executed at the end of each training batch.
    // We can use it to track the training loss.
    this.losses.push(logs.loss);
  }

  onEpochEnd(epoch, logs) {
    // This function is executed at the end of each training epoch.
    // We can use it to save the model.
    console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
    this.model.save(`model_at_epoch_${epoch}.h5`);
  }
}
```

在这个例子中，我们创建了四个自定义回调函数：

* onTrainBegin：训练开始时执行该函数。我们可以用它来初始化我们的自定义变量。
* onTrainEnd：训练结束时执行该函数。我们可以用它来保存我们的自定义变量。
* onBatchEnd：此函数在每个训练批次结束时执行。我们可以用它来跟踪训练损失。
* onEpochEnd：这个函数在每个训练时期结束时执行。我们可以用它来保存模型。

## 使用自定义回调

现在我们已经创建了自定义回调，让我们看看如何使用它。

首先，我们需要创建一个新的 TensorFlow.js 模型。在这个例子中，我们将使用一个简单的顺序模型。

接下来，我们需要使用自定义回调来编译模型。

最后，我们可以使用 fit 方法训练模型。

```javascript
const model = tf.sequential();

model.compile({
  optimizer: 'sgd',
  loss: 'binaryCrossentropy',
  callbacks: new CustomCallback()
});

model.fit(x, y, {
  epochs: 10
});
```

在此示例中，我们使用自定义回调来跟踪训练损失并在每个时期后保存模型。

## 结论

在本文中，我们学习了如何使用 TensorFlow.js 和 Node.js 创建自定义回调。我们还学习了如何使用回调来跟踪训练损失并在每个时期后保存模型。

创建自定义回调是扩展机器学习模型功能的好方法。回调允许您定义在训练过程中的特定点执行的自定义函数。

如果您有兴趣了解有关 TensorFlow.js 的更多信息，请务必查看 TensorFlow.js 网站 (https://js.tensorflow.org/)。