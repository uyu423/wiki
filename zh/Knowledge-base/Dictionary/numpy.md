---
title: Numpy
description: 
published: true
date: 2023-01-31T06:36:41.985Z
tags: 
editor: markdown
dateCreated: 2023-01-31T06:36:40.421Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Numpy***English** version of this document is available*](/en/Knowledge-base/Dictionary/numpy)
{.links-list}

  
# 概述
Numpy 是一个开源库，用于 Python 中的科学计算。它是数据分析和操作的强大工具，提供了许多有用的特性，例如执行速度快、面向对象编程和强大的数据结构。 Numpy 可用于各种任务，从数据分析到机器学习再到科学计算。

# 历史
Numpy 由 Travis Oliphant 于 2006 年创建。它是作为 SciPy 库的一部分开发的，SciPy 库是一个用于科学计算的开源库。 Numpy 自创建以来越来越受欢迎，现在被世界各地的数据科学家、机器学习工程师和软件开发人员常规使用。

# 描述
Numpy 是一个强大的库，可以在 Python 中快速高效地处理数字数据。它提供了许多有用的功能，例如：

* **数组对象**：Numpy 提供了能够容纳多个相同类型元素的数组对象。数组可用于快速高效地存储和操作大量数据。

* **数学函数**：Numpy 提供了许多数学函数，可用于对数组执行数学运算。这些函数包括基本的数学运算，例如加法、减法、乘法和除法，以及更高级的函数，例如矩阵乘法、傅里叶变换和线性代数运算。

* **面向对象编程**：Numpy 提供了一种面向对象的数据操作方法，使其易于使用和理解。它允许使用对象、类和函数来操作和分析数据。

# 例子
假设我们有一个二维数据点数组。我们可以使用 Numpy 使用以下代码轻松计算数组中每一行的平均值：

```python
import numpy as np

# Create a 2D array 
data = np.array([[1,2,3],
                 [4,5,6],
                 [7,8,9]])

# Calculate the average of each row
row_means = np.mean(data, axis=1)

# Print the result
print(row_means)

# Output: [2. 5. 8.]
```

# 优点和缺点
Numpy 是一个功能强大、灵活的库，可实现高效的数据分析和操作。它有很多优点，例如：

* **速度**：Numpy 经过高度优化，使其执行速度比大多数其他库更快。

* **面向对象编程**：Numpy 的面向对象方法使其易于使用和理解。

* **广泛的函数**：Numpy 提供了广泛的数学函数，可以轻松执行复杂的计算。

但是，Numpy 也有一些缺点，例如：

* **缺乏对某些数据类型的支持**：Numpy 不支持某些数据类型，例如对象和字符串。

* **有限的文档**：虽然 Numpy 提供了很好的文档，但它的范围有限并且可能并不总是清晰或易于理解。

# 相关链接
- [Numpy（英文）*官方网站*](https://numpy.org/)
- [Numpy 教程（英文）*Real Python*](https://realpython.com/numpy-tutorial-python/)
- [NumPy 教程（德语）*Python 学院*](https://www.python-academy.com/python_numpy_tutorial.html)
{.links-list}