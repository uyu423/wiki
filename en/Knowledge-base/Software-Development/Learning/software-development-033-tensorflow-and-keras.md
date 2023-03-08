---
title: Software Development 033: TensorFlow and Keras
description: 
published: true
date: 2023-02-28T13:32:22.315Z
tags: 
editor: markdown
dateCreated: 2023-02-28T13:32:15.087Z
---

- [소프트웨어 개발 033: TensorFlow 및 Keras***Korean** document is available*](/ko/Knowledge-base/Software-Development/Learning/software-development-033-tensorflow-and-keras)
{.links-list}


# Software Development 033: TensorFlow and Keras

## What is TensorFlow?

TensorFlow is a powerful open-source software library for data analysis and machine learning. Keras is a high-level neural networks API that is built on top of TensorFlow.

TensorFlow was originally developed by Google Brain team members for internal Google use. It was released under the Apache 2.0 open source license in November 2015.

Keras was developed by François Chollet, a Google engineer. It was released in March 2015 under the MIT open source license.

## Installation

You can install TensorFlow and Keras on your own computer by following the instructions on the TensorFlow website.

## Hello, world!

The "Hello, world!" program is a simple program that prints "Hello, world!" to the screen.

In Python, the "Hello, world!" program looks like this:

```python
print("Hello, world!")
```

In TensorFlow, the "Hello, world!" program looks like this:

```python
import tensorflow as tf

tf.print("Hello, world!")
```

In Keras, the "Hello, world!" program looks like this:

```python
from keras.models import Sequential
from keras.layers import Dense, Activation

model = Sequential()
model.add(Dense(1, input_dim=1))
model.add(Activation('sigmoid'))

model.compile(optimizer='rmsprop',
              loss='binary_crossentropy',
              metrics=['accuracy'])

model.fit(x, y, epochs=1000, batch_size=32)
```

## TensorFlow vs. Keras

TensorFlow is a lower-level library than Keras. That means that it is more flexible, but it also requires more work to get started.

If you are just getting started with deep learning, you should probably use Keras. It is easier to use and will save you time in the long run.

## Resources

- [TensorFlow website](https://www.tensorflow.org/)
- [Keras website](https://keras.io/)
- [TensorFlow Tutorial](https://www.tensorflow.org/tutorials/)
- [Keras Tutorial](https://keras.io/getting-started/sequential-model-guide/)