---
title: React
description: 
published: true
date: 2023-01-31T13:57:54.550Z
tags: 
editor: markdown
dateCreated: 2023-01-31T13:57:52.920Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [React***English** version of this document is available*](/en/Knowledge-base/Dictionary/react)
{.links-list}


# 概述
React 是一个用于构建用户界面的 JavaScript 库。它由 Facebook 和一个由个人开发者和公司组成的社区维护。 React 可以用作开发单页或移动应用程序的基础。

# 历史
React 是由 Facebook 的软件工程师 Jordan Walke 创建的。他于 2011 年首次发布了名为“FaxJS”的 React 早期原型。React 的首次公开发布是在 2013 年 5 月 29 日。从那时起，React 已成为最流行的用于构建用户界面的 JavaScript 库之一。

# 描述
React 是一个用于构建用户界面的 JavaScript 库。它用于创建可在 Web 应用程序中使用的可重用组件。 React 被设计为简单、高效和灵活。它使用声明式编程风格，使其更易于阅读和理解。

# 特征
React 具有多项特性，使其成为 Web 开发的热门选择。这些包括：

- **虚拟 DOM：** React 使用虚拟 DOM 来有效地更新 UI。这允许 React 更改 UI 而无需重新渲染整个页面。

- **JSX：** React 使用称为 JSX 的语法扩展，它允许开发人员在他们的 JavaScript 代码中编写类似 HTML 的语法。

- **React Native：** React Native 是一个移动开发框架，允许开发人员使用 React 创建适用于 iOS 和 Android 的原生应用程序。

- **Flux：** Flux 是 React 的应用程序架构，可帮助管理应用程序内的数据流。

- **服务器端渲染：** React 支持服务器端渲染，这允许开发人员在将 React 组件发送到客户端之前在服务器上渲染它们。

# 例子
下面是一个显示项目列表的 React 组件示例：

```javascript
import React from 'react';

class List extends React.Component {
  render() {
    return (
      <ul>
        {this.props.items.map(item => (
          <li key={item.id}>{item.name}</li>
        ))}
      </ul>
    );
  }
}
```

# 优点和缺点
React 有几个优点，包括：

- **易于学习：** React 易于学习和使用，是所有技能水平的开发人员的绝佳选择。

- **性能：** React 的虚拟 DOM 和服务器端渲染使其快速高效。

- **可重用组件：** React 组件是可重用的，这使得创建复杂的用户界面变得容易。

但是，使用 React 也有一些缺点，例如：

- **陡峭的学习曲线：**对于刚接触库的开发人员来说，React 可能很难学习。

- **缺乏文档：** React 的文档可能难以理解，这会使开发人员难以上手。

#争议
由于使用 JSX 语法，React 一直是一些争议的主题。一些开发人员认为 JSX 不是一种“真正的”编程语言，不应该用于 Web 开发。其他人则认为 JSX 是一种强大的工具，可以更轻松地编写复杂的用户界面。

# 相关技术
React 通常与其他技术结合使用，例如：

- **Redux：** Redux 是 React 的状态管理库，可帮助管理应用程序内的数据流。

- **GraphQL：** GraphQL 是一种 API 查询语言，可以更轻松地从服务器获取数据。

- **TypeScript：** TypeScript 是 JavaScript 的类型化超集，它为 React 应用程序增加了类型安全性。

# 题外话
React 已成为用于构建用户界面的最流行的 JavaScript 库之一。它被许多大公司使用，例如 Facebook、Airbnb 和 Netflix。 React 还被用于创建一些最流行的移动应用程序，例如 Instagram 和 Uber。

# 其他
React 是一个开源项目，在 MIT 许可下发布。这意味着任何人都可以免费使用 React，而无需支付任何费用或版税。 React 也得到了大型开发人员社区的积极维护和支持。