---
title: Spring Boot 中的模型-视图-视图模型 (MVVM) 模式
description: 
published: true
date: 2023-02-08T12:32:37.784Z
tags: 
editor: markdown
dateCreated: 2023-02-08T12:32:36.160Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [The Model-View-ViewModel (MVVM) Pattern in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/the-model-view-viewmodel-mvvm-pattern-in-spring-boot)
{.links-list}


# Spring Boot 中的模型-视图-视图模型 (MVVM) 模式

模型-视图-视图模型 (MVVM) 是一种架构设计模式，它将应用程序分为三个主要的逻辑组件模型、视图和视图模型。

MVVM 背后的主要思想是将大量业务逻辑和数据操作从 View 层移至 ViewModel 层。这有助于清理和分离代码，使应用程序更易于维护和测试。

ViewModel 然后通过可观察对象公开与视图相关的数据。 ViewModel 还公开了 View 可以绑定到的命令。这使 ViewModel 可以完全控制 View，而 View 不必知道 ViewModel。

## 模型

模型代表应用程序的数据和业务逻辑。在 MVVM 应用程序中，模型不知道 ViewModel，因此它对 ViewModel 没有任何依赖性。

模型负责管理应用程序的数据。它响应数据请求并在数据更改时通知观察者。

该模型还包含应用程序的业务逻辑。这是操纵数据和执行应用程序业务规则的逻辑。

## 看法

View 负责显示数据并调用 ViewModel 上的操作。

View 不应包含任何操作数据或执行应用程序业务规则的逻辑。此逻辑应包含在 ViewModel 中。

View 也不应该知道 ViewModel 的存在。 ViewModel 应该完全独立于 View。

## 视图模型

ViewModel 负责向视图提供数据并处理用户输入。

ViewModel 通过 observables 将数据暴露给 View。 ViewModel 还公开了 View 可以绑定到的命令。

ViewModel 包含操作数据和执行应用程序业务规则的逻辑。 ViewModel 还包含特定于 View 的代码。

ViewModel 不应该知道 View。 ViewModel 应该完全独立于 View。

## 数据绑定

数据绑定是一种允许 View 和 ViewModel 自动同步的机制。

数据绑定允许 ViewModel 在 ViewModel 中的数据发生变化时自动更新 View。数据绑定还允许 View 在用户输入更改时自动更新 ViewModel。

数据绑定是一个双向过程。对 View 中的数据所做的更改将传播到 ViewModel。对 ViewModel 中的数据所做的更改将传播到视图。

数据绑定是一种强大的机制，有助于保持 View 和 ViewModel 同步。

## 结论

模型-视图-视图模型 (MVVM) 是一种架构设计模式，它将应用程序分为三个主要的逻辑组件模型、视图和视图模型。

MVVM 背后的主要思想是将大量业务逻辑和数据操作从 View 层移至 ViewModel 层。这有助于清理和分离代码，使应用程序更易于维护和测试。

ViewModel 然后通过可观察对象公开与视图相关的数据。 ViewModel 还公开了 View 可以绑定到的命令。这使 ViewModel 可以完全控制 View，而 View 不必知道 ViewModel。

数据绑定是一种允许 View 和 ViewModel 自动同步的机制。数据绑定是一种强大的机制，有助于保持 View 和 ViewModel 同步。

## 参考

1. [模型-视图-视图模型 (MVVM) 模式](https://msdn.microsoft.com/en-us/library/hh848246.aspx)
2. [模型视图视图模型 (MVVM) 解释](https://www.codeproject.com/Articles/100175/Model-View-ViewModel-MVVM-Explained)
3. [MVVM Light Toolkit](http://www.mvvmlight.net/)
4. [MVVM中的数据绑定](https://www.tutorialspoint.com/mvvm/mvvm_data_binding.htm)