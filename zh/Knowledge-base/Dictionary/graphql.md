---
title: GraphQL
description: 
published: true
date: 2023-02-11T18:17:45.623Z
tags: 
editor: markdown
dateCreated: 2023-02-11T18:17:43.534Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [GraphQL***English** document is available*](/en/Knowledge-base/Dictionary/graphql)
{.links-list}


# 概述
GraphQL 是一种用于 API 的查询语言，也是使用现有数据完成这些查询的运行时。它提供了一种高效、强大且灵活的方法来开发 Web API。

# 描述
GraphQL 是 Facebook 于 2012 年创建的一种查询语言，它提供了 REST 和 ad-hoc 网络服务架构的替代方案。它允许客户端定义他们需要的数据的结构，并且从服务器返回完全相同的数据结构。这消除了对多个 API 提取的需要并减少了数据的过度提取，从而使应用程序更快、更高效。

GraphQL 被组织成一个类型系统，它定义了不同类型数据之间的关系，以及一种允许客户端请求特定字段数据的查询语言。 GraphQL 查询语言用于定义应从服务器返回的数据。 GraphQL 查询被发送到端点，服务器以请求的格式响应数据。

GraphQL 通常用于 Web 和移动应用程序，以及微服务架构。它还用于数据驱动的应用程序，例如内容管理系统，以定义应返回的数据的结构。

# 历史
GraphQL 由 Facebook 于 2012 年创建，作为传统 REST 架构的替代方案。最初，它在 Facebook 内部用于为他们的移动应用程序提供支持，但后来在 2015 年作为开源发布。从那时起，GraphQL 变得越来越流行，现在被各种各样的公司和组织使用。

# 特征
GraphQL 具有多项特性，使其成为传统 REST 架构的有吸引力的替代方案。这些包括：

- 自记录：GraphQL 是自记录的，这意味着数据的结构在查询中定义，因此服务器知道要返回什么数据。
- 灵活：GraphQL 是灵活的，允许客户准确地请求他们需要的数据，消除了多次 API 获取的需要。
- 高效：GraphQL 查询是高效的，因为它们只返回请求的数据，减少了数据的过度获取。
- 类型系统：GraphQL 有一个类型系统，它定义了不同类型数据之间的关系。

# 例子
下面是一个 GraphQL 查询的例子：

```
query {
  user(id: "123") {
    name
    age
    email
  }
}
```

此查询请求 ID 为“123”的用户的姓名、年龄和电子邮件。然后服务器将以与查询相同的结构响应请求的数据：

```
{
  "user": {
    "name": "John Doe",
    "age": 30,
    "email": "john@example.com"
  }
}
```

# 优点和缺点
与传统的 REST 架构相比，GraphQL 有几个优势，包括灵活性、效率和自记录查询。但是，它也有一些缺点，例如缺乏标准化和需要额外的工具来实施。

# 争议
GraphQL 一直是一些争议的主题，因为一些开发人员认为它过于复杂并且需要额外的工具才能实现。

# 相关技术
GraphQL 通常与其他技术结合使用，例如 Apollo，一个用于构建数据驱动应用程序的平台。

# 题外话
GraphQL 是一种越来越流行的技术，它的使用正在迅速增长。

# 其他的
GraphQL 是一种开源技术，其源代码可在 GitHub 上获得。