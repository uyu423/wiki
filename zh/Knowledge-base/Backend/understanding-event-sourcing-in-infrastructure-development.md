---
title: 了解基础设施开发中的事件溯源
description: 
published: true
date: 2023-01-31T08:36:20.870Z
tags: 
editor: markdown
dateCreated: 2023-01-31T08:36:19.143Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Understanding Event Sourcing in Infrastructure Development***English** version of this document is available*](/en/Knowledge-base/Backend/understanding-event-sourcing-in-infrastructure-development)
{.links-list}


本文适用于想要了解什么是事件溯源以及如何使用它来简化基础架构开发的 IT 开发人员。



事件溯源是一个在 IT 开发对话中变得越来越普遍的术语。但它是什么？事件溯源是通过将对应用程序状态的所有更改记录为事件序列来构建应用程序的实践。

这一系列事件通常称为事件日志。事件日志有很多优点：

1. 它们提供应用程序状态更改的完整历史记录。
2. 它们可用于重建应用程序在任何给定时间点的当前状态。
3. 它们可用于重放对应用程序状态的更改，这对于调试或审计目的很有用。

事件溯源对开发人员有很多好处：

1. 它使调试应用程序变得更容易，因为所有更改都被记录下来并且可以追溯到其原始原因。
2. 更容易审核应用程序，因为所有更改都被记录下来并且可以追溯到其原始原因。
3. 更容易向应用程序添加新功能，因为开发人员可以重放事件日志以查看应用程序状态如何更改以响应各种事件。

事件溯源有很多缺点：

1. 在现有应用程序中实施事件溯源可能很困难。
2. 维护事件日志可能很困难，因为它们会随着时间的推移而变大。
3.查询事件日志可能很困难，因为它们通常以线性格式存储。

尽管存在这些缺点，事件溯源已成为构建应用程序的流行技术，尤其是在微服务领域。这是因为事件溯源为微服务架构提供了许多好处，包括：

1.改进了调试，因为每个微服务都可以维护自己的事件日志。
2.改进审计，因为每个微服务都可以维护自己的事件日志。
3. 改进的可扩展性，因为每个微服务都可以维护自己的事件日志。
4. 改进模块化，因为每个微服务都可以维护自己的事件日志。

如果您有兴趣了解有关事件溯源的更多信息，可以在线获取大量资源，包括：

1. [事件溯源](https://martinfowler.com/eaaDev/EventSourcing.html) - Martin Fowler 的事件溯源综合指南。
2. [A Practical Introduction to Event Sourcing](https://www.infoq.com/articles/introduction-to-event-sourcing) - 来自 InfoQ 的事件溯源实用介绍。
3. [事件溯源](https://www.microservices.com/articles/event-sourcing/) - 来自 Microservices.com 的事件溯源指南。