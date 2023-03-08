---
title: Introduction to Machine Learning with TensorFlow and Keras
description: 
published: true
date: 2023-02-09T22:55:34.227Z
tags: 
editor: markdown
dateCreated: 2023-02-09T22:55:32.566Z
---

- [Introducción al aprendizaje automático con TensorFlow y Keras***Spanish** document is available*](/es/Knowledge-base/Common/introduction-to-machine-learning-with-tensorflow-and-keras)
{.links-list}
- [使用 TensorFlow 和 Keras 进行机器学习简介***Chinese Simplified** document is available*](/zh/Knowledge-base/Common/introduction-to-machine-learning-with-tensorflow-and-keras)
{.links-list}
- [TensorFlow 및 Keras를 사용한 기계 학습 소개***Korean** document is available*](/ko/Knowledge-base/Common/introduction-to-machine-learning-with-tensorflow-and-keras)
{.links-list}


# Introduction to Machine Learning with TensorFlow and Keras

Developers looking to add machine learning to their applications have many options to choose from when it comes to frameworks and libraries. TensorFlow and Keras are two of the most popular options for deep learning, and in this article, we'll be taking a look at how to get started with both of them.

## TensorFlow

TensorFlow is a popular open-source platform for machine learning developed by Google. It offers a wide range of tools, libraries, and community resources that allow developers to create sophisticated machine learning models with ease.

TensorFlow also has a strong focus on production deployments, and it offers a number of features that make it easy to deploy machine learning models to services and devices.

## Keras

Keras is a high-level deep learning API developed with a focus on ease of use and fast development. It is built on top of TensorFlow and can be used to create sophisticated machine learning models with minimal code.

Keras is also a popular choice for prototyping and research, as it offers a simple, efficient way to build and experiment with deep learning models.

## Getting Started

In this section, we'll take a look at how to get started with TensorFlow and Keras. We'll start by installing the required dependencies, and then we'll take a look at some basic code examples.

### Installation

Before we can start using TensorFlow and Keras, we need to install the required dependencies. TensorFlow can be installed using pip:

```
pip install tensorflow
```

Keras can be installed using pip as well:

```
pip install keras
```

### Hello, TensorFlow

Now that we have TensorFlow and Keras installed, let's take a look at a simple example. We'll start by importing the TensorFlow library:

```python
import tensorflow as tf
```

Next, we'll create a TensorFlow Constant:

```python
tf.constant('Hello, TensorFlow!')
```

This code will print the string "Hello, TensorFlow!" to the console.

### Hello, Keras

Now let's take a look at a simple Keras example. We'll start by importing the Keras library:

```python
import keras
```

Next, we'll create a Keras Sequential model:

```python
model = keras.Sequential()
```

This code will create a simple Keras Sequential model. We can then add layers to the model using the .add() method:

```python
model.add(keras.layers.Dense(units=32, input_shape=(784,)))
model.add(keras.layers.Activation('relu'))
model.add(keras.layers.Dense(units=10))
model.add(keras.layers.Activation('softmax'))
```

This code will add a dense layer with 32 neurons, an activation layer, a dense layer with 10 neurons, and an activation layer.

We can then compile the model using the .compile() method:

```python
model.compile(loss='categorical_crossentropy',
              optimizer='sgd',
              metrics=['accuracy'])
```

This code will compile the model using the categorical cross entropy loss function, the stochastic gradient descent optimizer, and the accuracy metric.

We can then fit the model to data using the .fit() method:

```python
model.fit(x_train, y_train,
          batch_size=128, epochs=5,
          verbose=1,
          validation_data=(x_test, y_test))
```

This code will fit the model to the training data for 5 epochs. The model will be trained using mini-batches of size 128. The .fit() method also takes a validation_data argument, which is used to evaluate the model during training.

We can then evaluate the model using the .evaluate() method:

```python
score = model.evaluate(x_test, y_test, verbose=0)
```

This code will evaluate the model on the test data and return the loss and accuracy.

## Conclusion

In this article, we've taken a look at how to get started with TensorFlow and Keras. We've installed the required dependencies and looked at some basic code examples.

If you're interested in learning more about TensorFlow and Keras, I would recommend checking out the following resources:

- The TensorFlow website: https://www.tensorflow.org/
- The Keras website: https://keras.io/
- The TensorFlow documentation: https://www.tensorflow.org/docs/
- The Keras documentation: https://keras.io/docs/