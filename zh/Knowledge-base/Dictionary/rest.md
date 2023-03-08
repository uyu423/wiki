---
title: REST
description: 
published: true
date: 2023-02-17T18:09:25.377Z
tags: 
editor: markdown
dateCreated: 2023-01-30T17:17:31.227Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [REST***English** version of this document is available*](/en/Knowledge-base/Dictionary/rest)
{.links-list}


# 概述

Representational State Transfer (REST) 是一种用于设计分布式系统（例如 Web 服务）的架构风格。它基于客户端-服务器架构和无状态通信的原则。

# 历史

REST 最早由 Roy Fielding 于 2000 年作为其博士论文的一部分提出。他认为现有的体系结构，例如 RPC 和 SOAP，过于复杂并且没有反映 Web 的工作方式。

# 描述

REST 基于客户端和服务器可以使用统一接口进行通信的想法。此接口基于 **HTTP** 的原理，HTTP 是一种用于在 Web 上的计算机之间交换数据的协议。它被设计为**无状态**，这意味着来自客户端的每个请求都被视为一个独立的事务，并且服务器不会在请求之间维护有关客户端的任何信息。

REST 架构的主要组件是**资源**、**表示**和**操作**。资源是系统的基本元素，例如用户或书籍。表示是在客户端和服务器之间交换的数据，例如 HTML 文档或 JSON 对象。动作是可以对资源执行的操作，例如创建、更新或删除它们。

REST 依赖于**超媒体**的概念。这是服务器可以在响应中提供指向其他相关资源的链接的想法。例如，对图书请求的响应可能包含指向作者个人资料页面的链接。这允许客户端访问附加信息而无需发出附加请求。

# 题外话

REST 还支持使用**缓存**，这可以通过减少需要在客户端和服务器之间传输的数据量来提高系统性能。

REST 还支持**版本控制**的概念，它允许在不破坏现有客户端的情况下发布 API 的新版本。这是通过在 URL 中包含版本信息并同时支持 API 的多个版本来实现的。

# 相关链接
- [RESTful Web 服务*O'Reilly Media*](https://www.oreilly.com/library/view/restful-web-services/9780596155860/)
- [REST API 教程*REST API 教程*](https://restapitutorial.com/)
- [REST 简介*Google Developers*](https://developers.google.com/drive/api/v3/about-rest)
{.links-list}