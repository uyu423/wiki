---
title: Bokeh
description: 
published: true
date: 2023-02-01T10:37:59.361Z
tags: 
editor: markdown
dateCreated: 2023-02-01T10:37:56.018Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Bokeh***English** version of this document is available*](/en/Knowledge-base/Dictionary/bokeh)
{.links-list}

# 概述

Bokeh 是一个用于 Python 的交互式可视化库，使用户能够创建复杂而强大的数据可视化。它是一种用于数据探索和分析的强大工具，供数据科学家、统计学家和其他需要以有效且有意义的方式分析和呈现数据的专业人员使用。 Bokeh 旨在与 Jupyter 笔记本和其他交互式工具一起使用，并提供广泛的特性和功能。

# 描述

Bokeh 是一个用于 Python 的交互式可视化库，使用户能够创建复杂而强大的数据可视化。它是一种用于数据探索和分析的强大工具，供数据科学家、统计学家和其他需要以有效且有意义的方式分析和呈现数据的专业人员使用。 Bokeh 旨在与 Jupyter 笔记本和其他交互式工具一起使用，并提供广泛的特性和功能。

Bokeh 是一个库，它提供用于创建交互式数据可视化的高级界面。它建立在流行的绘图库 Matplotlib 之上，并提供了许多功能，可以更轻松地创建交互式可视化。 Bokeh 旨在与 Jupyter 笔记本和其他交互式工具一起使用，并提供广泛的特性和功能。

Bokeh 提供了多种不同类型的可视化，包括折线图、条形图、散点图、直方图等。它还提供了许多用于操作和探索数据的工具，例如过滤、排序和缩放。 Bokeh 还提供了许多用于创建交互式可视化的工具，例如交互式滑块、按钮和其他小部件。

Bokeh 旨在与 Jupyter 笔记本和其他交互式工具一起使用，并提供广泛的特性和功能。它易于使用，并提供了许多功能，可以更轻松地创建交互式可视化。 Bokeh 还设计用于与 NumPy 和 Pandas 等其他库一起使用，并可用于创建强大而复杂的可视化效果。

# 历史

Bokeh 由 Continuum Analytics 的团队于 2012 年开发。该团队由 Bryan Van de Ven 领导，他现在是 Anaconda 的首席科学家。 Bokeh 旨在成为 Python 的交互式可视化库，并构建在流行的绘图库 Matplotlib 之上。

Bokeh 最初于 2012 年作为开源项目发布，此后已成为最受欢迎的 Python 可视化库之一。它供数据科学家、统计学家和其他需要以有效和有意义的方式分析和呈现数据的专业人员使用。

# 特征

Bokeh 为创建交互式数据可视化提供了广泛的特性和功能。它旨在与 Jupyter 笔记本和其他交互式工具一起使用，并提供广泛的特性和功能。

Bokeh 提供了多种不同类型的可视化，包括折线图、条形图、散点图、直方图等。它还提供了许多用于操作和探索数据的工具，例如过滤、排序和缩放。 Bokeh 还提供了许多用于创建交互式可视化的工具，例如交互式滑块、按钮和其他小部件。

Bokeh 旨在与 NumPy 和 Pandas 等其他库一起使用，并可用于创建强大而复杂的可视化效果。它还提供了许多功能，可以更轻松地创建交互式可视化，例如将 HTML 和 JavaScript 代码嵌入到 Bokeh 可视化中的能力。

# 例子

这是一个简单的 Bokeh 可视化示例。此示例使用 NumPy 和 Pandas 库创建一个简单的折线图。

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

# 优点和缺点

Bokeh 是一个强大而复杂的 Python 可视化库。它为创建交互式数据可视化提供了广泛的特性和功能。但是，使用 Bokeh 也有一些缺点。

优点：

- 易于使用并提供用于创建交互式数据可视化的广泛特性和功能。
- 旨在与 NumPy 和 Pandas 等其他库一起使用，并可用于创建强大而复杂的可视化效果。
- 提供大量用于操作和探索数据的工具，例如过滤、排序和缩放。

缺点：

- 不熟悉 Python 和其他编程语言的人可能难以学习和使用。
- 可能难以调试和排除故障。
- 不像其他可视化库那样广泛使用，例如 Matplotlib。