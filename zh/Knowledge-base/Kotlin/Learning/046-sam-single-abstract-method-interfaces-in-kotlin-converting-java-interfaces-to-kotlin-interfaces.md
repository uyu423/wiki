---
title: 046：Kotlin 中的 SAM（单一抽象方法）接口：将 Java 接口转换为 Kotlin 接口
description: 
published: true
date: 2023-02-05T21:55:17.978Z
tags: 
editor: markdown
dateCreated: 2023-02-05T21:55:16.375Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [046: SAM (Single Abstract Method) Interfaces in Kotlin: Converting Java Interfaces to Kotlin Interfaces***English** document is available*](/en/Knowledge-base/Kotlin/Learning/046-sam-single-abstract-method-interfaces-in-kotlin-converting-java-interfaces-to-kotlin-interfaces)
{.links-list}


# 046：Kotlin 中的 SAM（单一抽象方法）接口：将 Java 接口转换为 Kotlin 接口

由于 Kotlin 是一种 JVM 语言，因此它与 Java 完全兼容。这意味着您可以毫无问题地将任何 Java 接口转换为 Kotlin 接口。

但是，有一个警告：Kotlin 不支持 SAM（单一抽象方法）接口。这意味着您不能将具有单个抽象方法的 Java 接口转换为 Kotlin 接口。

这是因为 Kotlin 的类型系统与 Java 的不同。在 Kotlin 中，每个接口都必须至少有一个抽象方法，即使它只是一个没有主体的虚拟方法。

如果您要将具有多个抽象方法的 Java 接口转换为 Kotlin，这不是问题。但是，如果您要转换 SAM 接口，则需要向 Kotlin 接口添加一个抽象方法。

没有简单的方法可以做到这一点，因此您需要手动添加抽象方法。最好的方法是添加一个没有主体的虚拟方法。这将确保 Kotlin 接口与 Java 接口兼容。

以下是 Java SAM 接口的示例：

```java
public interface Runnable {
     public void run();
}
```

这是等效的 Kotlin 接口：

```kotlin
interface Runnable {
    fun run()
}
```

如您所见，Kotlin 接口有一个额外的抽象方法，```run()```，这是 Kotlin 类型系统所必需的。

如果要将 Java 接口转换为 Kotlin，则应始终检查该接口是否为 SAM 接口。如果是，您将需要向 Kotlin 接口添加一个额外的抽象方法。