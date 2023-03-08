---
title: Scikit-learn
description: 
published: true
date: 2023-02-26T22:32:39.046Z
tags: 
editor: markdown
dateCreated: 2023-02-26T22:32:32.110Z
---

- [Scikit-learn***Korean** document is available*](/ko/Knowledge-base/Dictionary/scikit-learn)
{.links-list}


# Overview
Scikit-learn is a free and open-source machine learning library for Python. It is designed to provide powerful and efficient tools for data mining and data analysis. Scikit-learn offers a wide range of supervised and unsupervised learning algorithms, and it is built on top of other popular Python libraries such as NumPy, SciPy, and matplotlib.

# Description
Scikit-learn is a powerful and efficient library for machine learning in Python. It is designed to provide a wide range of supervised and unsupervised learning algorithms, as well as tools for data mining and data analysis. It is built on top of other popular Python libraries such as NumPy, SciPy, and matplotlib.

Scikit-learn provides a range of supervised and unsupervised learning algorithms, including classification, regression, clustering, and dimensionality reduction. These algorithms can be used for a variety of tasks, including image recognition, text classification, and time series forecasting.

The library is designed to be easy to use, with a consistent interface and a focus on providing clear explanations and examples. It also includes a range of tools for model evaluation and selection, such as cross-validation and hyperparameter tuning.

# History
Scikit-learn was originally developed by David Cournapeau as a Google Summer of Code project in 2007. It was later released as an open-source project in 2010, and has since become one of the most popular machine learning libraries for Python.

# Features
Scikit-learn provides a range of supervised and unsupervised learning algorithms, including:
- Classification algorithms, such as logistic regression, support vector machines, and naive Bayes.
- Regression algorithms, such as linear regression, support vector machines, and decision trees.
- Clustering algorithms, such as k-means and hierarchical clustering.
- Dimensionality reduction algorithms, such as principal component analysis and linear discriminant analysis.

It also includes a range of tools for model evaluation and selection, such as cross-validation and hyperparameter tuning.

# Example
Scikit-learn can be used for a variety of tasks, such as image recognition, text classification, and time series forecasting. For example, it can be used to classify images of handwritten digits, as shown in the following example:

```python
from sklearn import datasets
from sklearn import svm

# Load the digits dataset
digits = datasets.load_digits()

# Create a Support Vector Classifier
clf = svm.SVC(gamma=0.001, C=100.)

# Train the classifier
clf.fit(digits.data[:-1], digits.target[:-1])

# Predict the label of the last image
predicted = clf.predict(digits.data[-1:])

# Print the predicted label
print(predicted)
```

# Pros and Cons
Scikit-learn is a powerful and efficient library for machine learning in Python. It is designed to be easy to use, with a consistent interface and a focus on providing clear explanations and examples.

However, Scikit-learn does not provide deep learning algorithms, and it can be difficult to use for complex tasks such as natural language processing.

# Related Technology
Scikit-learn is built on top of other popular Python libraries such as NumPy, SciPy, and matplotlib. It is also related to other machine learning libraries for Python, such as TensorFlow and Keras.