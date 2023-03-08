---
title: 在 Java 中构建自定义类加载器
description: 
published: true
date: 2023-02-12T17:17:48.387Z
tags: 
editor: markdown
dateCreated: 2023-02-12T17:17:41.612Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Building Custom Class Loaders in Java***English** document is available*](/en/Knowledge-base/Java/building-custom-class-loaders-in-java)
{.links-list}


# 在 Java 中构建自定义类加载器

在开发 Java 应用程序时，您可能需要创建自己的自定义类加载器。当您想要从默认类路径以外的位置加载类，或者您想要修改类的加载方式时，通常会出现这种情况。

在本文中，我们将了解如何在 Java 中创建自定义类加载器。我们还将查看自定义类加载器的一些常见用例。

## 什么是类加载器？

在深入探讨如何创建自定义类加载器之前，让我们先退后一步，了解什么是类加载器。

类加载器是一种软件，负责将类加载到 Java 应用程序中。当 Java 应用程序启动时，Java 虚拟机 (JVM) 加载类加载器。这个类加载器负责加载应用程序的类。

JVM 带有一个默认的类加载器，称为引导类加载器。该类加载器负责加载核心 Java 类，例如 `java.lang.String` 和 `java.util.ArrayList`。

除了引导类加载器之外，JVM 还带有另外两个类加载器：系统类加载器和扩展类加载器。

系统类加载器负责加载应用程序类路径中的类。类路径是 JVM 应该搜索类的位置列表。默认情况下，类路径包括 `jre/lib/` 和 `jre/class/` 目录。

扩展类加载器负责加载 `extensions/` 目录中的类。 `extensions/` 目录是开发人员可以放置他们希望对系统上的所有应用程序可用的 JAR 文件的地方。

## 为什么需要自定义类加载器？

现在我们已经回顾了什么是类加载器，让我们来看看您可能需要创建自定义类加载器的一些原因。

### 从不同的位置加载类

创建自定义类加载器的一个常见原因是从默认类路径以外的位置加载类。

例如，假设您的文件系统上有一个目录，其中包含您要加载到应用程序中的一些自定义类。您可以将此目录添加到您的类路径，但您的应用程序将只能从该目录加载类。

如果您希望您的应用程序能够从多个目录加载类，您需要创建一个自定义类加载器。这个自定义类加载器可以在多个目录中搜索类，而不仅仅是类路径。

### 修改类的加载方式

创建自定义类加载器的另一个常见原因是修改类加载的方式。

例如，假设您有一个 JAR 文件，其中包含您要加载到应用程序中的一些类。但是，您不希望系统类加载器加载这些类。相反，您希望使用自定义类加载器将这些类加载到单独的命名空间中。

这只是您可能希望如何修改类加载方式的一个示例。还有很多其他的可能性。

## 创建自定义类加载器

现在我们已经了解了您可能需要创建自定义类加载器的一些原因，让我们来看看如何实际创建一个。

创建自定义类加载器相对简单。您只需要创建一个扩展 java.lang.ClassLoader 的类。此类必须覆盖 `loadClass()` 方法。

这是一个简单的例子：

```java
public class MyClassLoader extends ClassLoader {
 
    @Override
    public Class<?> loadClass(String name) throws ClassNotFoundException {
        // Load the class from the filesystem
        // ...
        // Return the loaded class
        return null;
    }
}
```

在此示例中，我们创建了一个自定义类加载器，用于从文件系统加载类。这个类加载器实际上并不加载任何类，但它提供了一个框架，您可以使用它来创建自己的自定义类加载器。

## 使用自定义类加载器

创建自定义类加载器后，您需要告诉 JVM 使用它。您可以通过设置 java.class.path 系统属性来做到这一点。

例如，假设您有一个自定义类加载器，它从 `/path/to/classes` 目录加载类。您可以通过将“java.class.path”系统属性设置为“/path/to/classes”来告诉 JVM 使用此类加载器。

启动 Java 应用程序时，您可以在命令行上设置 java.class.path 系统属性：

```
java -Djava.class.path=/path/to/classes MyApplication
```

或者，您可以以编程方式设置系统属性：

```java
System.setProperty("java.class.path", "/path/to/classes");
```

一旦您设置了 java.class.path 系统属性，JVM 将使用您的自定义类加载器来加载类。

## 结论

在本文中，我们研究了如何在 Java 中创建自定义类加载器。我们还看到了自定义类加载器的一些常见用例。