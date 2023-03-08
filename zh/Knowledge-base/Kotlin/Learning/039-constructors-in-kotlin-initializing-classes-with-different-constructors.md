---
title: 039：Kotlin 中的构造函数：使用不同的构造函数初始化类
description: 
published: true
date: 2023-02-16T11:32:51.934Z
tags: 
editor: markdown
dateCreated: 2023-02-16T11:32:49.869Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [039: Constructors in Kotlin: Initializing Classes with Different Constructors***English** document is available*](/en/Knowledge-base/Kotlin/Learning/039-constructors-in-kotlin-initializing-classes-with-different-constructors)
{.links-list}


# 039：Kotlin 中的构造函数：使用不同的构造函数初始化类

在初始化类方面，Kotlin 提供了多种选择。在这篇文章中，我们将了解 Kotlin 中的构造函数，以及如何使用它们来初始化具有不同值的类。

构造函数是用于初始化类的特殊函数。在 Kotlin 中，有两种类型的构造函数：主要构造函数和次要构造函数。主构造函数是在第一次创建类时用于初始化类的构造函数。它在类的顶部声明，在类的主体之前。

二级构造函数用于用不同的值初始化类。它们在类的主体内声明。

类可以有多个次构造函数，但它们都必须调用主构造函数。这确保该类始终至少使用默认值进行初始化。

要创建具有主构造函数的类，我们使用关键字“class”后跟类名。然后我们在括号内声明主构造函数。在主构造函数中，我们可以声明任意数量的参数。这些参数可以是 val 或 var。

```kotlin
class MyClass(val param1: String, var param2: Int) {

}
```

在上面的例子中，我们创建了一个名为 MyClass 的类，它有一个带有两个参数的主构造函数。第一个参数是 `val`，第二个是 `var`。

我们也可以创建一个没有主构造函数的类。在这种情况下，类将使用每个参数的默认值进行初始化。

```kotlin
class MyClass {

}
```

要创建辅助构造函数，我们使用关键字“constructor”，后跟括号内的参数。然后我们可以在二级构造函数的主体中用不同的值初始化类。

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

}
```

在上面的示例中，我们创建了一个带有单个参数的辅助构造函数。该构造函数调用主构造函数并传入第二个参数的默认值。

我们还可以创建一个具有多个二级构造函数的类。在这种情况下，每个辅助构造函数必须调用不同的辅助构造函数。

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

    constructor(param1: String, param2: Int, param3: Boolean) : this(param1, param2)

}
```

在上面的示例中，我们创建了一个具有两个辅助构造函数的类。第一个构造函数调用主构造函数，第二个构造函数调用第一个辅助构造函数。

我们还可以创建一个具有主构造函数和多个辅助构造函数的类。在这种情况下，每个辅助构造函数都必须调用主构造函数。

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

    constructor(param1: String, param2: Int, param3: Boolean) : this(param1, param2)

}
```

在上面的示例中，我们创建了一个具有主构造函数和两个辅助构造函数的类。第一个辅助构造函数调用主构造函数，第二个辅助构造函数调用第一个辅助构造函数。

我们还可以创建一个具有主构造函数和多个辅助构造函数的类。在这种情况下，每个辅助构造函数必须调用不同的辅助构造函数。

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

    constructor(param1: String, param2: Int, param3: Boolean) : this(param1, param2)

}
```

在上面的示例中，我们创建了一个具有主构造函数和两个辅助构造函数的类。第一个辅助构造函数调用主构造函数，第二个辅助构造函数调用第一个辅助构造函数。

我们还可以创建一个具有主构造函数和多个辅助构造函数的类。在这种情况下，每个辅助构造函数都必须调用主构造函数。

```kotlin
class MyClass(val param1: String, var param2: Int) {

    constructor(param1: String) : this(param1, 0)

    constructor(param1: String, param2: Int, param3: Boolean) : this(param1, param2)

}
```

在上面的示例中，我们创建了一个具有主构造函数和两个辅助构造函数的类。第一个辅助构造函数调用主构造函数，第二个辅助构造函数调用第一个辅助构造函数。