---
title: 041：使用 TensorFlow.js 和 Node.js 进行过度拟合和正则化
description: 
published: true
date: 2023-02-02T16:36:23.323Z
tags: 
editor: markdown
dateCreated: 2023-02-02T16:36:21.766Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [041: Overfitting and Regularization with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/041-overfitting-and-regularization-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 进行过拟合和正则化

在机器学习中，过拟合是一种模型在训练数据上表现良好但在测试数据上表现不佳的现象。当模型过于紧密地记住训练数据并且不能很好地泛化到新数据时，就会发生这种情况。

对抗过度拟合的一种方法是通过正则化，这是向模型添加约束以防止其过度拟合的过程。在本文中，我们将探讨两种正则化方法，权重正则化和 dropout 正则化，以及如何在 TensorFlow.js 和 Node.js 中实现它们。

## 权重正则化

权重正则化是一种限制模型权重以防止过度拟合的方法。有两种常见的权重正则化类型：

* L1正则化：约束权重接近于零
* L2正则化：约束权重具有较小的量级

在 TensorFlow.js 中，可以通过在创建模型时指定 `l1` 或 `l2` 正则化强度来实现权重正则化：

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({
  units: 100,
  kernelRegularizer: tf.regularizers.l2({l2: 0.01}),
  inputShape: [inputShape]
}));
```

在上面的示例中，我们使用强度为 0.01 的 L2 正则化。

## 丢弃正则化

Dropout 正则化是一种将模型中的一部分权重随机设置为零的方法。这迫使模型学习以更少的权重运行，并防止它过度拟合。

在 TensorFlow.js 中，可以通过在创建模型时指定 dropoutRate 来实现 dropout 正则化：

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({
  units: 100,
  dropoutRate: 0.1,
  inputShape: [inputShape]
}));
```

在上面的例子中，我们使用了 0.1 的 dropout，这意味着 10% 的权重将被设置为零。

## 结论

在这篇文章中，我们探讨了两种正则化方法，权重正则化和 dropout 正则化，以及如何在 TensorFlow.js 和 Node.js 中实现它们。正则化是对抗过度拟合的有力工具，可以与交叉验证等其他方法结合使用。