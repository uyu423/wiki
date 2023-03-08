---
title: 024：Kotlin 中的枚举：创建命名值列表
description: 
published: true
date: 2023-02-16T07:33:05.551Z
tags: 
editor: markdown
dateCreated: 2023-02-16T07:32:57.678Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [024: Enumerations in Kotlin: Creating Lists of Named Values***English** document is available*](/en/Knowledge-base/Kotlin/Learning/024-enumerations-in-kotlin-creating-lists-of-named-values)
{.links-list}


# Kotlin 中的枚举：创建命名值列表

Kotlin 的枚举是创建命名值列表的强大工具。通过使用枚举，您可以创建可在您的代码中使用的类型安全、不可变的值列表。

枚举是使用 ```enum``` 关键字声明的。枚举中的每个值都称为“枚举常量”。枚举常量以逗号分隔。

这是 Kotlin 中枚举的一个简单示例：

```kotlin
enum class Color {
    RED,
    GREEN,
    BLUE
}
```

在这个例子中，我们创建了一个颜色枚举。 ```enum``` 关键字用于声明枚举，```class``` 关键字用于创建枚举常量。

枚举是不可变的，这意味着它们一旦创建就无法更改。这使它们可以在您的代码中安全使用。

在 Kotlin 中可以通过多种方式使用枚举。在这篇文章中，我们将了解一些可以在代码中使用枚举的方法。

## 使用枚举

在 Kotlin 中可以通过多种方式使用枚举。在本节中，我们将了解在代码中使用枚举的一些方法。

### 开关语句

枚举可以在 Kotlin 的```when``` 语句中使用。 ```When``` 语句是一种 ```switch``` 语句，允许您将值与可能值列表进行匹配。

下面是一个使用枚举的```when```语句的例子：

```kotlin
fun getColor(color: Color): String {
    when (color) {
        Color.RED -> return "Red"
        Color.GREEN -> return "Green"
        Color.BLUE -> return "Blue"
    }
}
```

在这个例子中，我们创建了一个函数，它接受一个 ```Color``` 枚举作为参数。然后我们使用 ```when``` 语句将 ```color``` 与可能值列表相匹配。

如果 ```color``` 是 ```RED```，该函数将返回字符串 ```"Red"```。如果 ```color``` 是 ```GREEN```，该函数将返回字符串 ```"Green"```。如果 ```color``` 是 ```BLUE```，该函数将返回字符串 ```"Blue"```。

### 遍历枚举

可以使用 ```for``` 循环迭代枚举。 ```for``` 循环将遍历枚举中的所有枚举常量。

以下是如何迭代枚举的示例：

```kotlin
for (color in Color.values()) {
    println(color)
}
```

在此示例中，我们使用 ```for``` 循环迭代 ```Color``` 枚举。我们将枚举的每个值打印到控制台。

此代码将以下内容打印到控制台：

```
RED
GREEN
BLUE
```

### 检查枚举值

您可以使用“in”关键字检查枚举中是否包含特定值。

以下是如何检查枚举中是否包含值的示例：

```kotlin
if (Color.RED in Color.values()) {
    println("Color.RED is in the Color enumeration")
}
```

在此示例中，我们使用 ```in``` 关键字来检查 ```Color.RED``` 枚举常量是否包含在 ```Color``` 枚举中。

如果 ```Color.RED``` 枚举常量包含在 ```Color``` 枚举中，代码将向控制台打印以下内容：

```
Color.RED is in the Color enumeration
```

### 按名称获取枚举值

您可以使用 ```valueOf()``` 函数通过名称获取枚举常量。

以下是如何通过名称获取枚举常量的示例：

```kotlin
val color: Color = Color.valueOf("RED")
```

在此示例中，我们使用 ```valueOf()``` 函数从 ```Color``` 枚举中获取 ```Color.RED``` 枚举常量。

### 创建你自己的枚举

除了标准的 Kotlin 枚举之外，您还可以创建自己的自定义枚举。

以下是如何创建自定义枚举的示例：

```kotlin
enum class MyEnum {
    FIRST_VALUE,
    SECOND_VALUE
}
```

在这个例子中，我们创建了一个名为 ```MyEnum``` 的自定义枚举。此枚举包含两个值：```FIRST_VALUE``` 和```SECOND_VALUE```。

您还可以使用自定义属性和方法创建枚举。

以下是如何使用自定义属性创建枚举的示例：

```kotlin
enum class MyEnum {
    FIRST_VALUE {
        override val property: Int
            get() = 1
    },
    SECOND_VALUE {
        override val property: Int
            get() = 2
    }

    abstract val property: Int
}
```

在此示例中，我们创建了一个枚举，其中包含一个名为“property”的自定义属性。这个属性是一个```抽象```属性，必须被每个枚举常量覆盖。

在这个例子中，我们覆盖了```FIRST_VALUE```和```SECOND_VALUE```枚举常量的```property```属性。

您还可以使用自定义方法创建枚举。

以下是如何使用自定义方法创建枚举的示例：

```kotlin
enum class MyEnum {
    FIRST_VALUE {
        override fun method(): String {
            return "First Value"
        }
    },
    SECOND_VALUE {
        override fun method(): String {
            return "Second Value"
        }
    }

    abstract fun method(): String
}
```

在此示例中，我们创建了一个枚举，其中包含一个名为 ```method()``` 的自定义方法。这个方法是一个```抽象```方法，必须被每个枚举常量覆盖。

在这个例子中，我们已经覆盖了```FIRST_VALUE```和```SECOND_VALUE```枚举常量的```method()```方法。

枚举是在 Kotlin 中创建命名值列表的强大工具。通过使用枚举，您可以创建可在您的代码中使用的类型安全、不可变的值列表。