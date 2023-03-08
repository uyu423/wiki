---
title: 033：Kotlin 中的默认参数和命名参数：提供默认值和命名参数
description: 
published: true
date: 2023-02-01T12:04:38.282Z
tags: 
editor: markdown
dateCreated: 2023-02-01T12:04:36.826Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [033: Default and Named Arguments in Kotlin: Providing Default Values and Named Parameters***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/033-default-and-named-arguments-in-kotlin-providing-default-values-and-named-parameters)
{.links-list}



# 033：Kotlin 中的默认参数和命名参数：提供默认值和命名参数

Kotlin 对默认参数和命名参数的支持使得为函数参数提供合理的默认值以及仅指定与默认值不同的参数变得容易。

## 默认参数

考虑一个用日期和时间格式化字符串的函数：

```kotlin
fun formatDateTime(
    date: String,
    time: String,
    dateFormat: String = "yyyy-MM-dd",
    timeFormat: String = "HH:mm:ss"
): String {
    return "$date $time"
}
```

这个函数有四个参数，其中两个有默认值。调用函数时，我们可以为前两个参数提供值，后两个参数将使用默认值：

```kotlin
formatDateTime("2019-01-01", "12:00:00") // "2019-01-01 12:00:00"
```

我们还可以为所有四个参数提供值：

```kotlin
formatDateTime(
    date = "2019-01-01",
    time = "12:00:00",
    dateFormat = "dd/MM/yy",
    timeFormat = "hh:mm a"
) // "01/01/19 12:00 PM"
```

## 命名参数

当调用带有多个参数的函数时，参数的顺序很重要。这会使代码难以阅读，尤其是当某些参数具有默认值时。

Kotlin 对命名参数的支持让我们可以指定参数名称和值，这使代码更易于阅读：

```kotlin
fun formatDateTime(
    date: String,
    time: String,
    dateFormat: String = "yyyy-MM-dd",
    timeFormat: String = "HH:mm:ss"
): String {
    return "$date $time"
}
 
formatDateTime(
    time = "12:00:00",
    date = "2019-01-01",
    timeFormat = "hh:mm a",
    dateFormat = "dd/MM/yy"
) // "01/01/19 12:00 PM"
```

在上面的示例中，我们指定了参数名称和值。这使代码更易于阅读，尤其是当某些参数具有默认值时。

## 仅指定与默认值不同的参数

当调用带有多个参数的函数时，我们可以只指定与默认值不同的参数。例如，考虑以下函数：

```kotlin
fun formatDateTime(
    date: String,
    time: String,
    dateFormat: String = "yyyy-MM-dd",
    timeFormat: String = "HH:mm:ss"
): String {
    return "$date $time"
}
```

这个函数有四个参数，其中两个有默认值。我们可以用两个参数调用这个函数，默认值将用于其余参数：

```kotlin
formatDateTime("2019-01-01", "12:00:00") // "2019-01-01 12:00:00"
```

我们还可以仅指定与默认值不同的参数：

```kotlin
formatDateTime(
    date = "2019-01-01",
    time = "12:00:00",
    timeFormat = "hh:mm a"
) // "2019-01-01 12:00:00"
```

在上面的示例中，我们为“date”和“time”参数指定了值，默认值将用于“dateFormat”参数。

## 结论

Kotlin 对默认参数和命名参数的支持使得为函数参数提供合理的默认值以及仅指定与默认值不同的参数变得容易。这可以使代码更易于阅读和理解。