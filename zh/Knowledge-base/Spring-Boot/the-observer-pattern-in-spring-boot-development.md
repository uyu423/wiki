---
title: Spring Boot开发中的观察者模式
description: 
published: true
date: 2023-02-08T13:32:49.714Z
tags: 
editor: markdown
dateCreated: 2023-02-08T13:32:47.570Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [The Observer Pattern in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-observer-pattern-in-spring-boot-development)
{.links-list}


# Spring Boot开发中的观察者模式

观察者模式是一种软件设计模式，其中一个对象（称为主题）维护其从属列表（称为观察者），并自动通知它们任何状态更改，通常是通过调用它们的方法之一。

它是事件驱动编程非常有用的模式，也是模型-视图-控制器 (MVC) 架构模式的基础之一。

在本文中，我们将了解如何在 Spring Boot 应用程序中使用观察者模式。我们将从查看模式的基本概念及其通常的使用方式开始。然后我们将看到 Spring Boot 如何通过其对 JavaBeans 规范的内置支持使实现该模式变得容易。

## 什么是观察者模式？

正如我们所提到的，观察者模式是一种软件设计模式，其中一个对象（称为主体）维护其依赖者（称为观察者）的列表，并自动通知它们任何状态更改，通常是通过调用它们的方法之一。

这个定义有几点需要注意：

- 主题是一个对象，而不是一个类。这意味着主题可以是任何类型的对象，包括原始类型，如 int 或 String。

- 观察者也是对象，而不是类。这意味着观察者可以是任何类型的对象，包括原始类型，如 int 或 String。

- 主题维护其观察者列表。此列表通常作为集合实现，例如 ArrayList 或 LinkedList。

- 主题通过调用他们的方法之一通知其观察者。调用的方法取决于实现，但它通常是特定于观察者模式的方法，例如 update() 或 handleEvent()。

- 观察者模式常用于事件驱动编程。这意味着观察者会在主题发生状态变化时得到通知，而不是被轮询变化。

现在我们已经了解了观察者模式的基本概念，让我们来看看它通常是如何使用的。

## 观察者模式是如何使用的？

观察者模式有几种不同的使用方式，但最常见的是事件驱动编程。

在事件驱动编程中，应用程序通常围绕中央事件循环进行组织。事件由用户、硬件或应用程序本身生成，并由事件处理程序处理。

观察者模式可用于将事件处理程序与事件循环分离。事件处理程序可以作为观察者实现，并且可以在事件循环中注册。当事件发生时，事件循环通知观察者，观察者可以处理该事件。

这有几个优点：

- 事件处理程序可以作为可重用组件来实现。

- 事件处理程序可以在运行时注册和注销。

- 可以按任何顺序调用事件处理程序。

- 可以同时调用事件处理程序。

让我们看看如何在 Spring Boot 应用程序中使用观察者模式。

## 在 Spring Boot 中使用观察者模式

Spring Boot 内置了对 JavaBeans 规范的支持，可以轻松使用观察者模式。

JavaBeans 是 Java 组件的规范，它定义了一组用于编写 Java 代码的约定。约定之一是 JavaBeans 组件必须为其每个属性都具有 JavaBeans 样式的设置方法。

例如，如果一个组件有一个名为 foo 的属性，则该组件必须有一个 setFoo() 方法。调用 setFoo() 方法时，组件必须触发 FooPropertyChangeEvent。

Spring Boot 使用此约定来支持观察者模式。启动 Spring Boot 应用程序时，它会扫描类路径以查找具有 JavaBeans 样式设置方法的类。对于每个 setter 方法，它都会注册一个观察者。

当调用 setter 方法时，会通知观察者。观察者然后可以采取任何适当的操作，例如调用主题上的方法或记录消息。

让我们通过一个简单的例子看看这是如何工作的。

## 例子

考虑一个具有名为 foo 的属性的 Spring Boot 应用程序。应用程序在 application.properties 文件中设置 foo 属性：

富=酒吧

该应用程序还有一个名为 FooObserver 的类，它实现了 Observer 接口：

公共类 FooObserver 实现观察者 {

    @覆盖
    public void update(Observable o, Object arg) {
        // 做一点事
    }

}

当应用程序启动时，Spring Boot 框架会扫描类路径以查找具有 JavaBeans 样式设置方法的类。它找到 FooObserver 类并将其注册为 foo 属性的观察者。

当应用程序设置 foo 属性时，Spring Boot 框架调用 FooObserver 的 update() 方法。然后 update() 方法可以采取任何适当的操作，例如记录消息或调用主题的方法。

此示例展示了如何使用观察者模式来解耦 Spring Boot 应用程序的组件。观察者可以作为可重用组件来实现，并且可以在运行时注册和注销。

## 结论

在本文中，我们了解了如何在 Spring Boot 应用程序中使用观察者模式。我们已经了解了模式的基本概念及其通常的使用方式。然后，我们了解了 Spring Boot 如何通过其对 JavaBeans 规范的内置支持轻松实现该模式。