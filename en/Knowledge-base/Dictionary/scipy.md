---
title: SciPy
description: 
published: true
date: 2023-02-28T21:32:45.695Z
tags: 
editor: markdown
dateCreated: 2023-02-28T21:32:38.403Z
---

- [SciPy***Korean** document is available*](/ko/Knowledge-base/Dictionary/scipy)
{.links-list}


# Overview 
SciPy is a free and open-source Python library used for scientific computing and technical computing. It contains modules for optimization, linear algebra, integration, interpolation, special functions, FFT, signal and image processing, ODE solvers, and other tasks common in science and engineering.

# Description
SciPy is a collection of mathematical algorithms and convenience functions built on the NumPy extension of Python. It adds significant power to the interactive Python session by providing the user with high-level commands and classes for manipulating and visualizing data. With SciPy, an interactive Python session becomes a data-processing and system-prototyping environment rivaling systems such as MATLAB, IDL, Octave, R-Lab, and SciLab.

SciPy builds on the NumPy array object and is part of the NumPy stack which includes tools like Matplotlib, pandas and SymPy, and an expanding set of scientific computing libraries. The SciPy library is one of the core packages that make up the SciPy stack. It provides many user-friendly and efficient numerical routines such as routines for numerical integration and optimization. 

The SciPy library depends on NumPy, which provides convenient and fast N-dimensional array manipulation. The SciPy library is built to work with NumPy arrays and provides many user-friendly and efficient numerical routines such as routines for numerical integration and optimization. 

# History
SciPy was created in 2001 by Travis Oliphant and Pearu Peterson, both of whom had worked on NumPy. It was initially released in 2002 and has since grown to become one of the most popular Python scientific computing libraries.

# Features
SciPy contains modules for optimization, linear algebra, integration, interpolation, special functions, FFT, signal and image processing, ODE solvers, and other tasks common in science and engineering. It also provides several high-level commands and classes for manipulating and visualizing data.

The SciPy library is built to work with NumPy arrays and provides many user-friendly and efficient numerical routines such as routines for numerical integration and optimization. It also contains a large number of optimized numerical routines, including routines for linear algebra, Fourier transform, and random number generation.

# Example
Let's look at an example of how to use SciPy to calculate the integral of a function.

First, we need to import the SciPy library:

```
import scipy
```

Then, we define the function we want to integrate:

```
def f(x):
    return x**2
```

Finally, we use SciPy's `integrate.quad` function to calculate the integral:

```
result = scipy.integrate.quad(f, 0, 1)
print(result)
```

The result of the integration is `(0.33333333333333337, 3.700743415417189e-15)`, which is the integral of the function `f(x) = x**2` from 0 to 1.

# Pros and Cons
The main advantage of SciPy is its wide range of modules and functions for scientific computing, which makes it a powerful and versatile tool for data analysis and manipulation. It is also open source and free to use, which makes it accessible to a wide range of users.

The main disadvantage of SciPy is that it is built on top of NumPy, so it requires a good understanding of NumPy to use it effectively. In addition, SciPy can be slow for certain operations, such as linear algebra calculations.

# Related Technology
SciPy is closely related to NumPy, a Python library for scientific computing. It is also related to other Python libraries such as Matplotlib, pandas, and SymPy, which are part of the SciPy stack.