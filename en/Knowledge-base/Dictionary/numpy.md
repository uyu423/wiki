---
title: Numpy
description: 
published: true
date: 2023-01-31T06:36:43.795Z
tags: 
editor: markdown
dateCreated: 2023-01-31T06:36:40.418Z
---

- [Numpy***Korean** version of this document is available*](/ko/Knowledge-base/Dictionary/numpy)
{.links-list}
- [Numpy***Japanese** version of this document is available*](/ja/Knowledge-base/Dictionary/numpy)
{.links-list}
- [Numpy***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Dictionary/numpy)
{.links-list}

  
# Overview
Numpy is an open-source library that is used in scientific computing in Python. It is a powerful tool for data analysis and manipulation, and it provides many useful features such as fast execution speed, object-oriented programming, and powerful data structures. Numpy can be used for a wide variety of tasks, from data analysis to machine learning to scientific computing.

# History
Numpy was created by Travis Oliphant in 2006. It was developed as a part of the SciPy library, an open-source library for scientific computing. Numpy has grown in popularity since its creation, and is now used routinely by data scientists, machine learning engineers, and software developers around the world.

# Description
Numpy is a powerful library that allows for fast and efficient manipulation of numerical data in Python. It provides many useful features, such as:

* **Array objects**: Numpy provides array objects which are capable of holding multiple elements of the same type. Arrays can be used to store and manipulate large amounts of data quickly and efficiently.

* **Mathematical functions**: Numpy provides many mathematical functions that can be used to perform mathematical operations on arrays. These functions include basic mathematical operations, such as addition, subtraction, multiplication, and division, as well as more advanced functions, such as matrix multiplication, Fourier transforms, and linear algebra operations.

* **Object-oriented programming**: Numpy provides an object-oriented approach to data manipulation, which makes it easy to use and understand. It allows for the use of objects, classes, and functions to manipulate and analyze data. 

# Example
Let's say we have a two-dimensional array of data points. We can use Numpy to easily calculate the average of each row in the array by using the following code:

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

# Pros and Cons
Numpy is a powerful, flexible library that enables efficient data analysis and manipulation. It has many advantages, such as:

* **Speed**: Numpy is highly optimized, allowing it to execute faster than most other libraries. 

* **Object-oriented programming**: Numpy's object-oriented approach makes it easy to use and understand.

* **A wide range of functions**: Numpy provides a wide range of mathematical functions, making it easy to perform complex calculations.

However, Numpy also has some drawbacks, such as:

* **Lack of support for some data types**: Numpy does not support some data types, such as objects and strings.

* **Limited documentation**: While Numpy provides good documentation, it is limited in scope and may not always be clear or easy to understand.

# Related Links
- [Numpy (English) *Official Site*](https://numpy.org/)
- [Numpy Tutorial (English) *Real Python*](https://realpython.com/numpy-tutorial-python/)
- [NumPy Tutorial (German) *Python Academy*](https://www.python-academy.com/python_numpy_tutorial.html)
{.links-list}