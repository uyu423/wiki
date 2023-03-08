---
title: Plotly Dash
description: 
published: true
date: 2023-02-11T14:17:41.721Z
tags: 
editor: markdown
dateCreated: 2023-02-11T14:17:39.879Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Plotly Dash***English** document is available*](/en/Knowledge-base/Dictionary/plotly-dash)
{.links-list}


# 概述
Plotly Dash 是一个用于创建交互式 Web 应用程序的开源 Python 库。它建立在流行的 Plotly 库之上，使用户能够创建高度可定制和交互式的数据可视化。数据科学家、开发人员和分析师使用 Dash 创建功能强大的数据驱动应用程序。

# 描述
Plotly Dash 是一个用于使用 Python 创建交互式 Web 应用程序的库。它建立在流行的 Plotly 库之上，使用户能够创建高度可定制和交互式的数据可视化。数据科学家、开发人员和分析师使用 Dash 创建功能强大的数据驱动应用程序。 Dash 应用程序由两部分组成：Web 应用程序前端和运行应用程序的 Python 代码。 Web 应用程序前端使用 HTML、CSS 和 JavaScript 编写，负责显示数据可视化。 Python 代码负责创建数据可视化并且是用 Python 编写的。

Dash 应用程序是高度可定制和交互的。 Dash 允许用户创建具有各种交互功能的数据可视化，例如缩放、平移和悬停。 Dash 还提供了种类繁多的图表和绘图，包括折线图、条形图、散点图等。

# 特征
Plotly Dash 提供了多种功能，可用于使用 Python 创建交互式 Web 应用程序。一些功能包括：

- 种类繁多的图表和绘图，包括折线图、条形图、散点图等。
- 具有缩放、平移和悬停等功能的高度可定制和交互式数据可视化。
- 与其他 Python 库（如 Pandas、SciPy 和 NumPy）轻松集成。
- 轻松将 Dash 应用程序部署到 Web。

# 例子
下面是一个显示折线图的简单 Dash 应用程序示例。

```python
import dash
import dash_core_components as dcc
import dash_html_components as html
import plotly.graph_objects as go

app = dash.Dash()

app.layout = html.Div([
    dcc.Graph(
        figure=go.Figure(
            data=[
                go.Scatter(
                    x=[1, 2, 3],
                    y=[4, 5, 6],
                    mode='lines'
                )
            ]
        )
    )
])

if __name__ == '__main__':
    app.run_server(debug=True)
```

# 优点和缺点
优点：

- 易于使用和高度可定制。
- 各种各样的图表和绘图。
- 与其他 Python 库轻松集成。
- 轻松将应用程序部署到 Web。

缺点：

- 不适合大型和复杂的应用程序。
- 对 JavaScript 和 HTML 等其他语言的有限支持。

# 相关技术
Plotly Dash 与其他库相关，例如 Plotly、Bokeh 和 Matplotlib。这些库都用于在 Python 中创建数据可视化。 Plotly 和 Dash 都建立在流行的 Plotly 库之上，使用户能够创建高度可定制和交互式的数据可视化。 Bokeh 是一个用于使用 Python 创建交互式数据可视化的库，用于创建交互式 Web 应用程序。 Matplotlib 是一个用 Python 创建静态数据可视化的库，用于创建静态数据可视化。