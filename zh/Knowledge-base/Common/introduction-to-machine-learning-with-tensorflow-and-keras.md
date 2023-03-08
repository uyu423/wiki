---
title: 使用 TensorFlow 和 Keras 进行机器学习简介
description: 
published: true
date: 2023-02-09T22:55:38.958Z
tags: 
editor: markdown
dateCreated: 2023-02-09T22:55:32.557Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Introduction to Machine Learning with TensorFlow and Keras***English** document is available*](/en/Knowledge-base/Common/introduction-to-machine-learning-with-tensorflow-and-keras)
{.links-list}


# 使用 TensorFlow 和 Keras 进行机器学习简介

希望将机器学习添加到他们的应用程序中的开发人员在框架和库方面有很多选择。 TensorFlow 和 Keras 是深度学习的两个最流行的选择，在本文中，我们将了解如何开始使用它们。

## 张量流

TensorFlow 是由谷歌开发的流行的机器学习开源平台。它提供范围广泛的工具、库和社区资源，使开发人员能够轻松创建复杂的机器学习模型。

TensorFlow 还非常注重生产部署，它提供了许多功能，可以轻松地将机器学习模型部署到服务和设备。

## 凯拉斯

Keras 是一种高级深度学习 API，专注于易用性和快速开发。它建立在 TensorFlow 之上，可用于以最少的代码创建复杂的机器学习模型。

Keras 也是原型设计和研究的热门选择，因为它提供了一种简单、高效的方式来构建和试验深度学习模型。

## 入门

在本节中，我们将了解如何开始使用 TensorFlow 和 Keras。我们将从安装所需的依赖项开始，然后我们将看一些基本的代码示例。

### 安装

在开始使用 TensorFlow 和 Keras 之前，我们需要安装所需的依赖项。可以使用 pip 安装 TensorFlow：

```
pip install tensorflow
```

Keras 也可以使用 pip 安装：

```
pip install keras
```

### 你好，TensorFlow

现在我们已经安装了 TensorFlow 和 Keras，让我们看一个简单的例子。我们将从导入 TensorFlow 库开始：

```python
import tensorflow as tf
```

接下来，我们将创建一个 TensorFlow 常量：

```python
tf.constant('Hello, TensorFlow!')
```

此代码将打印字符串“Hello, TensorFlow!”到控制台。

### 你好，凯拉斯

现在让我们看一个简单的 Keras 示例。我们将从导入 Keras 库开始：

```python
import keras
```

接下来，我们将创建一个 Keras Sequential 模型：

```python
model = keras.Sequential()
```

此代码将创建一个简单的 Keras Sequential 模型。然后我们可以使用 .add() 方法向模型添加层：

```python
model.add(keras.layers.Dense(units=32, input_shape=(784,)))
model.add(keras.layers.Activation('relu'))
model.add(keras.layers.Dense(units=10))
model.add(keras.layers.Activation('softmax'))
```

此代码将添加一个具有 32 个神经元的致密层、一个激活层、一个具有 10 个神经元的致密层和一个激活层。

然后我们可以使用 .compile() 方法编译模型：

```python
model.compile(loss='categorical_crossentropy',
              optimizer='sgd',
              metrics=['accuracy'])
```

此代码将使用分类交叉熵损失函数、随机梯度下降优化器和精度度量来编译模型。

然后我们可以使用 .fit() 方法将模型拟合到数据：

```python
model.fit(x_train, y_train,
          batch_size=128, epochs=5,
          verbose=1,
          validation_data=(x_test, y_test))
```

此代码将使模型适合 5 个时期的训练数据。该模型将使用大小为 128 的小批量进行训练。 .fit() 方法还采用 validation_data 参数，用于在训练期间评估模型。

然后我们可以使用 .evaluate() 方法评估模型：

```python
score = model.evaluate(x_test, y_test, verbose=0)
```

此代码将根据测试数据评估模型并返回损失和准确性。

## 结论

在本文中，我们了解了如何开始使用 TensorFlow 和 Keras。我们已经安装了所需的依赖项并查看了一些基本代码示例。

如果您有兴趣了解有关 TensorFlow 和 Keras 的更多信息，我建议您查看以下资源：

- TensorFlow 网站：https://www.tensorflow.org/
- Keras 网站：https://keras.io/
- TensorFlow 文档：https://www.tensorflow.org/docs/
- Keras 文档：https://keras.io/docs/