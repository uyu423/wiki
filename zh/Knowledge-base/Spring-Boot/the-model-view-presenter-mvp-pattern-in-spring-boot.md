---
title: Spring Boot 中的模型-视图-呈现器 (MVP) 模式
description: 
published: true
date: 2023-01-31T11:23:20.575Z
tags: 
editor: markdown
dateCreated: 2023-01-31T11:23:18.892Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [The Model-View-Presenter (MVP) Pattern in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-model-view-presenter-mvp-pattern-in-spring-boot)
{.links-list}


  MVP 模式是用于创建用户界面的 MVC 模式的派生物。它是 Web 应用程序的流行选择，因为它将应用程序的关注点分为三个不同的部分：模型、视图和演示者。这种关注点分离使代码更易于维护和测试。

MVP 模式类似于 MVC 模式，因为它也有模型、视图和控制器。然而，MVP 模式有几个关键的区别。首先，MVP 模式在视图和模型之间没有直接联系。相反，演示者充当两者之间的调解人。这允许视图和模型彼此完全独立。其次，MVP 模式更加强调演示者。演示者负责处理所有用户输入并相应地更新视图。

使用 MVP 模式有很多好处。首先，它使对代码进行单元测试变得更加容易。其次，它可以更轻松地更改用户界面，而无需更改底层代码。第三，它更容易将代码重用于其他目的。

如果您有兴趣在下一个 Spring Boot 项目中使用 MVP 模式，则需要牢记一些事项。首先，您需要为每个视图创建一个单独的 Presenter 类。其次，您需要将演示者注入到视图中。第三，您需要将视图绑定到演示者。第四，您需要将演示器连接到模型。最后，您需要向演示者注册视图。

完成所有这些后，您就可以开始在 Spring Boot 项目中使用 MVP 模式了。