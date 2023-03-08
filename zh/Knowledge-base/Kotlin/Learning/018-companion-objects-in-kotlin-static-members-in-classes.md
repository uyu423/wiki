---
title: 018：Kotlin 中的伴随对象：类中的静态成员
description: 
published: true
date: 2023-02-16T05:32:17.094Z
tags: 
editor: markdown
dateCreated: 2023-02-16T05:32:14.981Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [018: Companion Objects in Kotlin: Static Members in Classes***English** document is available*](/en/Knowledge-base/Kotlin/Learning/018-companion-objects-in-kotlin-static-members-in-classes)
{.links-list}


# Kotlin 中的伴随对象：类中的静态成员

Kotlin 伴随对象允许您在类中定义静态成员。在本文中，我们将了解什么是伴生对象以及如何使用它们。

## 什么是伴随对象？

 伴随对象是与类关联的对象。它们用于在类中存储静态成员。

静态成员是与类相关联的成员，而不是与类的实例相关联的成员。这意味着您无需创建类的实例即可访问它们。

 伴随对象是使用“伴随对象”关键字声明的。它们可用于存储常量、实用函数和工厂方法。

## 如何使用伴随对象

伴随对象是使用“伴随对象”关键字声明的。它们可用于存储常量、实用函数和工厂方法。

要访问伴生对象的成员，您可以使用类名作为限定符。例如，如果在名为 MyClass.kt 的文件中有一个名为 MyClass 的伴生对象，您可以像这样访问其成员：

```kotlin
MyClass.Companion.myFunction()
```

如果你想从类中访问伴生对象的成员，你可以省略 `companion` 关键字。例如：

```kotlin
class MyClass {
    companion object {
        fun myFunction() {
            // ...
        }
    }
}
```

## 结论

在本文中，我们了解了伴生对象是什么以及如何使用它们。伴随对象是在类中存储静态成员的好方法。