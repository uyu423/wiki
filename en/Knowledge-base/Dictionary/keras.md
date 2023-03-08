---
title: Keras
description: 
published: true
date: 2023-02-16T03:56:02.548Z
tags: 
editor: markdown
dateCreated: 2023-02-16T03:55:53.566Z
---

- [Keras***Japanese** document is available*](/ja/Knowledge-base/Dictionary/keras)
{.links-list}
- [Keras***Spanish** document is available*](/es/Knowledge-base/Dictionary/keras)
{.links-list}
- [Keras***Chinese Simplified** document is available*](/zh/Knowledge-base/Dictionary/keras)
{.links-list}
- [Keras***Korean** document is available*](/ko/Knowledge-base/Dictionary/keras)
{.links-list}


# Overview
Keras is an open source neural network library written in Python. It is designed to be simple and intuitive for users of all skill levels to create and deploy deep learning models. Keras is a high-level API that can be used with TensorFlow, Theano, or CNTK backends.

# Description
Keras is a library for deep learning, a type of machine learning that uses neural networks to learn from data. It was developed by François Chollet, a Google engineer, and released in 2015. Keras is designed to be user-friendly and intuitive, and it provides a high-level API for building and training neural networks.

Keras is built on top of TensorFlow, Theano, or CNTK, which are lower-level libraries for building and training neural networks. It provides a simpler, more intuitive interface for users to create and train models. Keras also supports convolutional and recurrent neural networks, which are used for image and text processing, respectively.

Keras is a popular choice for deep learning due to its ease of use and flexibility. It is also used in many applications, including computer vision, natural language processing, and automatic speech recognition.

# Features
Keras provides a number of features to make it easier to work with deep learning models. These include:

- **High-level API:** Keras provides a high-level API for building and training neural networks, making it easy for users of all skill levels to create models.

- **Compatibility:** Keras is compatible with TensorFlow, Theano, and CNTK, allowing users to choose the backend that best fits their needs.

- **Modular design:** Keras is designed to be modular, allowing users to easily create and combine different layers and models.

- **Support for convolutional and recurrent networks:** Keras supports convolutional and recurrent neural networks, which are used for image and text processing, respectively.

- **Extensibility:** Keras is designed to be extensible, allowing users to create custom layers and models.

# Example
The following example shows how to create a simple convolutional neural network using Keras.

```python
from keras.layers import Conv2D, MaxPooling2D
from keras.models import Sequential

model = Sequential()
model.add(Conv2D(32, (3, 3), activation='relu', input_shape=(28, 28, 1)))
model.add(MaxPooling2D((2, 2)))
model.add(Conv2D(64, (3, 3), activation='relu'))
model.add(MaxPooling2D((2, 2)))
model.add(Conv2D(64, (3, 3), activation='relu'))

model.summary()
```

# Pros and Cons
Keras is a popular choice for deep learning due to its ease of use and flexibility. It is designed to be user-friendly and intuitive, and it provides a high-level API for building and training neural networks.

However, Keras is not suitable for all applications. It does not provide as much control over the model as lower-level libraries such as TensorFlow or Theano. It also does not support distributed computing, which can be important for large-scale projects.

# Related Technology
Keras is built on top of TensorFlow, Theano, and CNTK, which are lower-level libraries for building and training neural networks. It is also related to other machine learning frameworks such as Scikit-learn and PyTorch.