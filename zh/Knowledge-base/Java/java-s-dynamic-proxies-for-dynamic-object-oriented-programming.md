---
title: 用于动态面向对象编程的 Java 动态代理
description: 
published: true
date: 2023-02-03T06:23:35.292Z
tags: 
editor: markdown
dateCreated: 2023-02-03T06:23:33.658Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Java's Dynamic Proxies for Dynamic Object Oriented Programming***English** document is available*](/en/Knowledge-base/Java/java-s-dynamic-proxies-for-dynamic-object-oriented-programming)
{.links-list}



# 用于动态面向对象编程的 Java 动态代理

Java 的动态代理允许以类型安全、面向对象的方式创建动态代码。在本文中，我们将探讨如何使用动态代理来创建动态代码，以及如何在实际应用中使用它们。

## 什么是动态代理？

动态代理是一个实现在运行时指定的接口列表的类。当在动态代理实例上调用方法时，方法调用将转发到 Proxy 类的 invoke() 方法，该方法将调用分派到适当的方法处理程序。

动态代理可用于在对象周围创建一个“包装器”，它可用于在不修改原始代码的情况下向对象添加功能。例如，动态代理可用于向对象上的所有方法调用添加日志记录，或者在允许调用方法之前添加安全检查。

## 创建动态代理

创建动态代理相对简单。首先，您需要创建 Proxy 类的实例，传入要代理的类的 ClassLoader 以及代理应实现的接口数组。例如：

```java
ClassLoader classLoader = MyObject.class.getClassLoader();
Class[] interfaces = new Class[] { MyObject.class };

MyObject myObject = (MyObject) Proxy.newProxyInstance(classLoader, interfaces, new MyObjectInvocationHandler(myObject));
```

在上面的示例中，我们使用 Proxy 类为 MyObject 类创建动态代理。 MyObject 类必须可由给定的 ClassLoader 加载，并且必须实现 MyObject 接口。 Proxy.newProxyInstance() 方法的第三个参数是 InvocationHandler 的实例，它负责处理代理上的方法调用。

在上面的示例中，我们创建了一个简单的 InvocationHandler，它只是将方法调用转发给原始对象。但是，您可以轻松地将自己的逻辑添加到 InvocationHandler，例如记录方法调用或添加安全检查。

## 使用动态代理

一旦创建了动态代理，就可以像使用任何其他对象一样使用它。例如，如果您有 MyObject 类的动态代理，则可以像在原始对象上一样调用代理上的方法：

```java
myObject.doSomething();
```

## 为什么使用动态代理？

动态代理是创建动态代码的强大工具。它们可用于在不修改原始代码的情况下向对象添加功能，这在您无法访问源代码的情况下非常有用。

动态代理还可用于创建“包装器”对象，这些对象可用于在不更改对象接口的情况下向对象添加功能。例如，您可以使用动态代理在对象周围创建一个包装器，将日志记录添加到对象上的所有方法调用，而无需更改对象的接口。

## 何时使用动态代理

在需要向对象添加功能而不修改原始代码的情况下，动态代理非常有用。它们也可用于创建“包装器”对象，这些对象可用于在不更改对象接口的情况下向对象添加功能。

## 何时不使用动态代理

动态代理不应在性能至关重要的情况下使用，因为它们添加了一个可能影响性能的间接层。它们也不应该在需要将底层对象传递给本地方法的情况下使用，因为 JVM 本身不支持 Proxy 类。

## 结论

动态代理是创建动态代码的强大工具。它们可用于在不修改原始代码的情况下向对象添加功能，这在您无法访问源代码的情况下非常有用。动态代理还可用于创建“包装器”对象，这些对象可用于在不更改对象接口的情况下向对象添加功能。