---
title: D3.js
description: 
published: true
date: 2023-02-17T05:55:43.386Z
tags: 
editor: markdown
dateCreated: 2023-02-17T05:55:40.910Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [D3.js***English** document is available*](/en/Knowledge-base/Dictionary/d3-js)
{.links-list}


# 概述
D3.js 是一个开源 JavaScript 库，用于在 Web 浏览器中创建交互式数据可视化。它是数据分析和数据驱动文档操作的强大工具。

# 描述
D3.js 是一个 JavaScript 库，使开发人员能够在 Web 浏览器中创建数据可视化。它使用 SVG、HTML 和 CSS 来创建交互式数据可视化，例如条形图、折线图和散点图。 D3.js 提供了广泛的功能，包括数据绑定、动画和动态数据操作。它还支持使用来自外部源的数据，例如 CSV 文件、JSON 和 XML。

D3.js 被设计为高度模块化和可扩展的，允许开发人员创建自定义数据可视化。它具有广泛的插件和库，可用于添加其他特性和功能。

# 历史
D3.js 由 Mike Bostock 于 2011 年创建。它最初作为 JavaScript 库发布，用于创建数据可视化和交互式文档。从那时起，它就被开发人员和数据科学家广泛采用，用于创建数据驱动的可视化。

# 特征
D3.js 具有广泛的功能，使其成为数据分析和数据驱动文档操作的强大工具。一些主要功能包括：

- 数据绑定：D3.js 可以将数据绑定到 DOM 元素，允许开发人员创建动态数据可视化。
- 动画：D3.js 支持动画和过渡，允许开发人员创建交互式可视化。
- 动态数据操作：D3.js 支持对来自外部源的数据进行操作，例如 CSV 文件、JSON 和 XML。
- 可扩展性：D3.js 被设计为高度模块化和可扩展的，允许开发人员创建自定义数据可视化。

# 例子
以下是使用 D3.js 创建的条形图的简单示例：

```
<script src="https://d3js.org/d3.v4.min.js"></script>
<script>
  var data = [4, 8, 15, 16, 23, 42];

  var x = d3.scaleLinear()
    .domain([0, d3.max(data)])
    .range([0, 420]);

  d3.select(".chart")
    .selectAll("div")
    .data(data)
    .enter().append("div")
    .style("width", function(d) { return x(d) + "px"; })
    .text(function(d) { return d; });
</script>

<div class="chart"></div>
```

# 优点和缺点
D3.js 是用于数据分析和数据驱动文档操作的强大工具。它具有广泛的功能，并且具有高度模块化和可扩展性。但是，它可能很难学习，并且可能需要大量时间和精力来创建复杂的可视化效果。

# 相关技术
D3.js 通常与其他技术结合使用，例如 React 和 Redux。 React 是一个用于构建用户界面的 JavaScript 库，而 Redux 是一个用于管理应用程序状态的状态管理库。

# 题外话
D3.js 通常与其他技术结合使用，例如 React 和 Redux。 React 是一个用于构建用户界面的 JavaScript 库，而 Redux 是一个用于管理应用程序状态的状态管理库。

# 其他的
D3.js 是一个开源项目，由大型开发人员社区积极维护。它还用于各种行业，例如金融、医疗保健和媒体。