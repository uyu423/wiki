---
title: 086：Android 上的 Kotlin：使用 Kotlin 构建 Android 应用程序
description: 
published: true
date: 2023-02-15T12:18:01.788Z
tags: 
editor: markdown
dateCreated: 2023-02-15T12:17:59.344Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [086: Kotlin on Android: Building Android Apps with Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/Learning/086-kotlin-on-android-building-android-apps-with-kotlin)
{.links-list}


# 086：Android 上的 Kotlin：使用 Kotlin 构建 Android 应用程序

Kotlin 是一种功能强大的编程语言，可用于构建 Android 应用程序。在本文中，我们将了解如何在 Android 上开始使用 Kotlin。

## 安装科特林

要在 Android 上开始使用 Kotlin，您首先需要安装 Kotlin 插件。您可以在 Android Studio 中执行此操作，方法是转到文件 > 设置 > 插件并搜索 Kotlin 插件。安装插件后，您需要重新启动 Android Studio。

Android Studio 重新启动后，您将能够创建一个新的 Kotlin 项目。为此，转到文件 > 新建 > 新建项目，然后从项目类型列表中选择 Kotlin 选项。

## 创建一个 Kotlin 项目

安装 Kotlin 插件后，您可以创建一个新的 Kotlin 项目。为此，转到文件 > 新建 > 新建项目，然后从项目类型列表中选择 Kotlin 选项。

当您创建一个新的 Kotlin 项目时，系统会要求您指定项目的名称和位置，以及项目 SDK。指定这些详细信息后，单击“完成”按钮创建项目。

## 创建 Kotlin 文件

创建 Kotlin 项目后，您可以创建 Kotlin 文件。为此，请转至文件 > 新建 > Kotlin 文件/类。

当您创建一个新的 Kotlin 文件时，系统会要求您指定文件的名称和位置。您还将被要求指定 Kotlin 文件类型。有四种 Kotlin 文件类型：

- 科特林类
- 科特林文件
- 科特林对象
- 科特林界面

指定文件的名称和位置后，单击“完成”按钮创建文件。

## 编写 Kotlin 代码

现在您已经创建了一个 Kotlin 项目和一个 Kotlin 文件，您可以开始编写 Kotlin 代码了。

Kotlin 代码写在扩展名为 .kt 的文件中。 Kotlin 文件可以包含一个或多个顶级声明。顶级声明是不在类、对象或接口内部的声明。

Kotlin 具有丰富的功能集，使其成为开发 Android 应用程序的绝佳选择。其中一些功能包括：

- 零安全
- 扩展功能
- 数据类
- 协程

在下一节中，我们将更详细地了解其中的一些功能。

## 空安全

Kotlin 最重要的特性之一是空安全。空安全是一种防止空指针异常发生的特性。

要使变量 null 安全，您需要使用 ?操作员。例如，以下代码将无法编译，因为 name 变量可以为 null：

```kotlin
var name: String = "John"
name = null
```

为了使代码为 null 安全，您需要使用 ?操作员：

```kotlin
var name: String? = "John"
name = null
```

现在代码可以编译了，因为 name 变量可以为 null。

## 扩展函数

Kotlin 的另一个重要特性是扩展函数。扩展函数允许您使用新功能扩展一个类，而不必对其进行子类化。

例如，假设您有一个带有 isEmpty() 函数的类，如果该类为空则返回 true，否则返回 false。您可以使用新的 isNotEmpty() 函数扩展此类，该函数返回与 isEmpty() 相反的函数：

```kotlin
fun isNotEmpty(): Boolean {
    return !isEmpty()
}
```

要使用新函数，您只需在类的实例上调用它：

```kotlin
val list = ArrayList<String>()
list.isNotEmpty() // returns false
```

## 数据类

Kotlin 还支持数据类。数据类是设计用来保存数据的类。它们类似于 JavaBeans，但创建和使用起来要简单得多。

要创建数据类，您需要使用数据关键字：

```kotlin
data class User(val name: String, val age: Int)
```

此代码创建一个具有两个属性的数据类：name 和 age。这些属性是使用 val 关键字声明的，这意味着它们是只读的。

要创建数据类的实例，您只需调用构造函数：

```kotlin
val user = User("John", 30)
```

要访问数据类的属性，可以使用点表示法：

```kotlin
user.name // returns "John"
user.age // returns 30
```

数据类还有一些有用的函数，例如 toString()、hashCode() 和 equals()：

```kotlin
user.toString() // returns "User(name=John, age=30)"
user.hashCode() // returns -1234
user.equals(other) // returns true if the two objects are equal
```

## 协程

协同程序是 Kotlin 中的一项新功能，可以更轻松地编写异步代码。协程类似于线程，但它们的重量要轻得多，并且可以在不阻塞线程的情况下挂起。

要使用协程，您需要导入 kotlinx.coroutines 包：

```kotlin
import kotlinx.coroutines.*
```

然后，您可以使用 launch() 函数启动一个新的协程：

```kotlin
GlobalScope.launch {
    // suspendable code
}
```

在 launch() 函数内部，您可以编写可挂起的代码。可以在不阻塞线程的情况下暂停此代码。

要暂停协程，可以使用 delay() 函数：

```kotlin
GlobalScope.launch {
    delay(1000) // suspend for 1 second
    // resume here
}
```

delay() 函数接受一个以毫秒为单位的时间参数。协程将在指定时间过去后恢复。

您还可以使用 yield() 函数挂起协程并允许其他协程运行：

```kotlin
GlobalScope.launch {
    yield() // suspend and allow other coroutines to run
    // resume here
}
```

## 结论

在这篇文章中，我们研究了如何在 Android 上开始使用 Kotlin。我们已经了解了如何安装 Kotlin 插件、创建 Kotlin 项目和编写 Kotlin 代码。我们还看到了一些使 Kotlin 成为开发 Android 应用程序的绝佳选择的功能。