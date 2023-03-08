---
title: Bokeh
description: 
published: true
date: 2023-02-01T10:37:57.409Z
tags: 
editor: markdown
dateCreated: 2023-02-01T10:37:56.013Z
---

- [Bokeh***Korean** version of this document is available*](/ko/Knowledge-base/Dictionary/bokeh)
{.links-list}
- [Bokeh***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Dictionary/bokeh)
{.links-list}

# Overview

Bokeh is an interactive visualization library for Python that enables users to create sophisticated and powerful data visualizations. It is a powerful tool for data exploration and analysis, and is used by data scientists, statisticians, and other professionals who need to analyze and present data in an effective and meaningful way. Bokeh is designed to be used with Jupyter notebooks and other interactive tools, and provides a wide range of features and capabilities.

# Description

Bokeh is an interactive visualization library for Python that enables users to create sophisticated and powerful data visualizations. It is a powerful tool for data exploration and analysis, and is used by data scientists, statisticians, and other professionals who need to analyze and present data in an effective and meaningful way. Bokeh is designed to be used with Jupyter notebooks and other interactive tools, and provides a wide range of features and capabilities.

Bokeh is a library that provides a high-level interface for creating interactive data visualizations. It is built on top of the popular plotting library Matplotlib, and provides a number of features that make it easier to create interactive visualizations. Bokeh is designed to be used with Jupyter notebooks and other interactive tools, and provides a wide range of features and capabilities.

Bokeh provides a number of different types of visualizations, including line charts, bar charts, scatter plots, histograms, and more. It also provides a number of tools for manipulating and exploring data, such as filtering, sorting, and zooming. Bokeh also provides a number of tools for creating interactive visualizations, such as interactive sliders, buttons, and other widgets.

Bokeh is designed to be used with Jupyter notebooks and other interactive tools, and provides a wide range of features and capabilities. It is easy to use and provides a number of features that make it easier to create interactive visualizations. Bokeh is also designed to be used with other libraries, such as NumPy and Pandas, and can be used to create powerful and sophisticated visualizations.

# History

Bokeh was developed by the team at Continuum Analytics in 2012. The team was led by Bryan Van de Ven, who is now the Chief Scientist at Anaconda. Bokeh was designed to be an interactive visualization library for Python, and was built on top of the popular plotting library Matplotlib.

Bokeh was initially released as an open source project in 2012, and has since become one of the most popular visualization libraries for Python. It is used by data scientists, statisticians, and other professionals who need to analyze and present data in an effective and meaningful way.

# Features

Bokeh provides a wide range of features and capabilities for creating interactive data visualizations. It is designed to be used with Jupyter notebooks and other interactive tools, and provides a wide range of features and capabilities.

Bokeh provides a number of different types of visualizations, including line charts, bar charts, scatter plots, histograms, and more. It also provides a number of tools for manipulating and exploring data, such as filtering, sorting, and zooming. Bokeh also provides a number of tools for creating interactive visualizations, such as interactive sliders, buttons, and other widgets.

Bokeh is designed to be used with other libraries, such as NumPy and Pandas, and can be used to create powerful and sophisticated visualizations. It also provides a number of features that make it easier to create interactive visualizations, such as the ability to embed HTML and JavaScript code into Bokeh visualizations.

# Example

Here is an example of a simple Bokeh visualization. This example uses the NumPy and Pandas libraries to create a simple line chart.

```
import numpy as np
import pandas as pd

# Create a dataframe with some random data
df = pd.DataFrame(np.random.randn(10, 4), columns=list('ABCD'))

# Create a Bokeh figure
from bokeh.plotting import figure
p = figure(title="Simple Line Chart")

# Add a line renderer with legend and line thickness
p.line(df.index, df['A'], legend="A", line_width=2)

# Show the results
show(p)
```

# Pros and Cons

Bokeh is a powerful and sophisticated visualization library for Python. It provides a wide range of features and capabilities for creating interactive data visualizations. However, there are some drawbacks to using Bokeh.

Pros:

- Easy to use and provides a wide range of features and capabilities for creating interactive data visualizations.
- Designed to be used with other libraries, such as NumPy and Pandas, and can be used to create powerful and sophisticated visualizations.
- Provides a number of tools for manipulating and exploring data, such as filtering, sorting, and zooming.

Cons:

- Can be difficult to learn and use for those who are not familiar with Python and other programming languages.
- Can be difficult to debug and troubleshoot.
- Not as widely used as other visualization libraries, such as Matplotlib.