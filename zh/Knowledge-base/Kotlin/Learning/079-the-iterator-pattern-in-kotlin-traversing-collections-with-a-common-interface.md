---
title: 079：Kotlin 中的迭代器模式：使用通用接口遍历集合
description: 
published: true
date: 2023-02-14T05:17:36.213Z
tags: 
editor: markdown
dateCreated: 2023-02-14T05:17:29.026Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [079: The Iterator Pattern in Kotlin: Traversing Collections with a Common Interface***English** document is available*](/en/Knowledge-base/Kotlin/Learning/079-the-iterator-pattern-in-kotlin-traversing-collections-with-a-common-interface)
{.links-list}


# Kotlin 中的迭代器模式：使用通用接口遍历集合

迭代器模式是一种设计模式，其中迭代器用于遍历容器并访问容器的元素。迭代器模式用于提供一种在不暴露底层实现的情况下顺序访问聚合对象元素的方法。

Kotlin 是一种在 Java 虚拟机上运行的静态类型编程语言。 Kotlin 是一种简洁、安全、可互操作且工具友好的语言。它是 Apache 2.0 许可下的开源项目。

Kotlin 标准库提供了一组标准迭代器，它们是定义如何迭代元素集合的接口。 Kotlin 中有 3 个标准的迭代器：

- 迭代器
- 列表迭代器
- 可变迭代器

迭代器模式是一种在不暴露底层实现的情况下遍历 Kotlin 集合的有用方法。通过使用迭代器，我们可以顺序安全地访问 Kotlin 集合的元素，而不必担心底层实现。

## Kotlin 中的迭代器

在 Kotlin 中，迭代器是一个对象，它提供了一种按顺序访问集合元素的方法。 Kotlin 的标准库提供了一组标准迭代器，这些迭代器是定义如何迭代元素集合的接口。 Kotlin 中有 3 个标准的迭代器：

- 迭代器
- 列表迭代器
- 可变迭代器

迭代器有两个方法：`hasNext()` 和 `next()`。如果集合中有另一个元素可以使用 `next()` 方法访问，则 `hasNext()` 方法返回 true。 `next()` 方法返回集合中的下一个元素。

我们可以使用迭代器迭代任何 Kotlin 集合，包括列表、集合和映射。让我们来看看如何使用带有列表的迭代器。


```kotlin
val list = listOf(1, 2, 3, 4, 5)
val iterator = list.iterator()

while (iterator.hasNext()) {
    println(iterator.next())
}
```

在上面的示例中，我们创建了一个整数列表和该列表的迭代器。然后我们使用 `hasNext()` 方法检查列表中是否有更多元素可以使用 `next()` 方法访问。如果有更多元素，我们将元素打印到控制台。

我们还可以使用 forEach() 方法迭代 Kotlin 集合。 `forEach()` 方法将 lambda 作为参数，并为集合中的每个元素调用 lambda。

```kotlin
val list = listOf(1, 2, 3, 4, 5)

list.forEach {
    println(it)
}
```

在上面的示例中，我们创建了一个整数列表，并使用 `forEach()` 方法遍历该列表。我们将 lambda 传递给将每个元素打印到控制台的“forEach()”方法。

## Kotlin 中的可变迭代器

可变迭代器是可用于修改基础集合的迭代器。 Kotlin 的标准库提供了一个 MutableIterator 接口，它定义了如何迭代和修改可变元素集合。

可变迭代器具有三个方法：`hasNext()`、`next()` 和 `remove()`。 `hasNext()` 和 `next()` 方法的工作方式与它们对迭代器的工作方式相同。 `remove()` 方法从底层集合中移除由 `next()` 方法返回的最后一个元素。

让我们来看看如何使用带有列表的可变迭代器。

```kotlin
val list = mutableListOf(1, 2, 3, 4, 5)
val iterator = list.iterator()

while (iterator.hasNext()) {
    val element = iterator.next()
    if (element % 2 == 0) {
        iterator.remove()
    }
}

println(list)
```

在上面的示例中，我们为该列表创建了一个可变的整数列表和一个可变的迭代器。然后我们使用 `hasNext()` 方法检查列表中是否有更多元素可以使用 `next()` 方法访问。如果有更多元素，我们从列表中获取元素并检查它是否可以被 2 整除。如果是，我们使用 `remove()` 方法将其从列表中删除。

我们还可以使用 `forEach()` 方法来迭代和修改 Kotlin 集合。 `forEach()` 方法将 lambda 作为参数，并为集合中的每个元素调用 lambda。 lambda 有两个参数：元素和元素的索引。

```kotlin
val list = mutableListOf(1, 2, 3, 4, 5)

list.forEach { element, index ->
    if (element % 2 == 0) {
        list.removeAt(index)
    }
}

println(list)
```

在上面的示例中，我们创建了一个可变的整数列表，并使用 `forEach()` 方法遍历该列表。我们将 lambda 传递给带有两个参数的 `forEach()` 方法：元素和元素的索引。如果该元素可以被 2 整除，我们使用 removeAt() 方法将其从列表中删除。

## 结论

在本文中，我们了解了迭代器模式以及如何在 Kotlin 中使用迭代器。我们还了解了可变迭代器以及如何使用它们来修改底层集合。