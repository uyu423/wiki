---
title: Robert C. Martin
description: 
published: true
date: 2023-02-02T17:24:41.105Z
tags: 
editor: markdown
dateCreated: 2023-02-02T17:24:38.978Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Robert C. Martin***English** document is available*](/en/Knowledge-base/Dictionary/robert-c-martin)
{.links-list}


# 概述
罗伯特 C. 马丁（也被称为鲍勃叔叔）是一位著名的软件工程师、作家和演讲者。他以在软件设计原则（如 SOLID 原则）方面的工作以及在软件工程和软件工艺方面的著作而闻名。他是敏捷软件开发实践的坚定拥护者，并撰写了多本关于该主题的书籍。

# 描述
Robert C. Martin 是一位软件工程师、作家和演讲者，他以在软件设计原则（如 SOLID 原则）方面的工作以及他在软件工程和软件工艺方面的著作而闻名。他是敏捷软件开发实践的坚定拥护者，并撰写了多本关于该主题的书籍。

Martin 是成功的咨询公司 Object Mentor Inc. 的创始人，并且是多本书的作者，包括“Clean Code: A Handbook of Agile Software Craftsmanship”和“The Clean Coder: A Code of Conduct for Professional Programmers”。他还是流行的软件架构和设计框架 Uncle Bob's Architecture 的创建者。

Martin 大力提倡软件工艺以及编写干净、可维护的代码的重要性。他经常在会议上发表演讲，并就软件设计、软件测试和软件工程最佳实践等主题发表过多次演讲。

# 历史
Robert C. Martin 1952 年出生于宾夕法尼亚州，1976 年毕业于马萨诸塞大学，获得计算机科学学位。毕业后，他开始从事软件工程师的工作，此后在软件行业担任过各种职位。

在 80 年代后期，Martin 开始研究 SOLID 原则，这是一组五个软件设计原则，为创建可维护和可扩展的软件提供了一个框架。 20 世纪 90 年代中期，他开始撰写有关软件工程和软件工艺的文章，并于 2000 年创立了 Object Mentor Inc.，这是一家成功的咨询公司。

从那以后，马丁写了几本书，包括《整洁代码：敏捷软件工艺手册》和《整洁代码：专业程序员行为准则》。他还是流行的软件架构和设计框架 Uncle Bob's Architecture 的创建者。

# 特征
SOLID 原则是 Robert C. Martin 工作的基石，是一组五个软件设计原则，为创建可维护和可扩展的软件提供了一个框架。这些原则是：

- 单一职责原则：一个类应该有一个且只有一个改变的理由。
- 开闭原则：软件实体应该对扩展开放，对修改关闭。
- Liskov 替换原则：派生类必须可以替换它们的基类。
- 接口隔离原则：不应该强迫客户依赖于他们不使用的方法。
- 依赖倒置原则：依赖于抽象，而不是具体化。

Martin 还大力提倡软件工艺以及编写干净、可维护的代码的重要性。他写了几本书，并就软件设计、软件测试和软件工程最佳实践等主题发表过多次演讲。

# 例子
作为如何应用 SOLID 原则的示例，请考虑以下代码：

```
class Database {
  public void save(String data) {
    // code to save data to the database
  }
 
  public void delete(String data) {
    // code to delete data from the database
  }
}
```

这段代码违反了单一职责原则，因为保存和删除数据都在同一个类中处理。为了坚持这一原则，应该重构代码以创建两个单独的类——一个用于保存数据，一个用于删除数据。

# 优点和缺点
SOLID 原则是一套包含五个软件设计原则的集合，它们为创建可维护和可扩展的软件提供了一个框架。这些原则的主要好处是它们使维护和扩展代码变得更加容易，因为每个类都有单一的职责，并且对扩展开放但对修改关闭。

然而，这些原则有一些缺点。例如，在设计复杂系统时可能很难坚持单一职责原则，重构代码以坚持这些原则可能需要花费更多的时间和精力。

# 争议
Martin 在软件设计原则和软件工艺方面的工作遇到了一些争议。一些人认为 SOLID 原则过于严格，可能导致代码过于复杂。其他人则认为，Martin 对软件工艺的关注可能会导致对“完美”代码的关注，这可能很耗时，而且并不总是必要的。

# 相关技术
SOLID 原则与 DRY（Don't Repeat Yourself）原则密切相关，DRY 原则指出代码不应不必要地重复。 DRY 原则通常与 SOLID 原则结合使用，以创建可维护和可扩展的代码。

# 题外话
Martin 还是敏捷软件开发实践的坚定拥护者。他写了几本关于这个主题的书，包括“敏捷软件开发：原则、模式和实践”和“敏捷宣言”。

# 其他
除了在软件设计和敏捷软件开发方面的工作外，Martin 还是软件测试的坚定倡导者。他写了几本关于这个主题的书，包括“软件测试的艺术”和“测试驱动开发：实例”。