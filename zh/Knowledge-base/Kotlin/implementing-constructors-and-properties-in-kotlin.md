---
title: 在 Kotlin 中实现构造函数和属性
description: 
published: true
date: 2023-02-02T02:18:21.114Z
tags: 
editor: markdown
dateCreated: 2023-02-02T02:18:19.491Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Implementing Constructors and Properties in Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/implementing-constructors-and-properties-in-kotlin)
{.links-list}


# 在 Kotlin 中实现构造函数和属性

Kotlin 是一种相对较新的编程语言，在开发社区中越来越受欢迎。它是一种静态类型的、面向对象的语言，运行在 Java 虚拟机上。 Kotlin 与所有现有的 Java 库和框架兼容，可用于广泛的开发任务。

Kotlin 的主要特性之一是它支持基于构造函数的编程。在 Kotlin 中，类可以有一个或多个构造函数。主构造函数定义在类头中，次构造函数定义在类主体中。

构造函数用于初始化类的对象。它们可用于设置变量的初始值、调用方法等。在 Kotlin 中，如果类没有任何初始化器，则不需要构造器。但是，如果一个类确实有初始值设定项，则必须至少定义一个构造函数。

以下是具有一个主构造函数和两个辅助构造函数的 Kotlin 类的简单示例：

```kotlin
class Person(val name: String) {
  
    var age: Int = 0
    
    constructor(name: String, age: Int) : this(name) {
        this.age = age
    }
    
    constructor(name: String, age: Int, gender: String) : this(name, age) {
        // ...
    }
}
```

在上面的示例中，主构造函数采用单个参数 name。二级构造函数分别采用两个和三个参数。所有构造函数都使用 this 关键字调用主构造函数。

构造函数也可用于初始化类的属性。在上面的示例中，name 属性由主构造函数初始化，age 属性由辅助构造函数初始化。

Kotlin 的另一个特性是它对属性的支持。属性是与类关联的变量。它们可以在类头或类主体中声明。

以下是具有两个属性 name 和 age 的 Kotlin 类的简单示例：

```kotlin
class Person {
  
    var name: String = ""
    
    var age: Int = 0
}
```

在上面的示例中，name 和 age 属性在类标头中声明。它们都分别使用默认值 "" 和 0 进行初始化。

属性也可以用非默认值初始化。在以下示例中，name 属性初始化为值“John”，age 属性初始化为值 30：

```kotlin
class Person {
  
    var name: String = "John"
    
    var age: Int = 30
}
```

Kotlin 还支持属性的惰性初始化。惰性初始化是一种将属性的初始化延迟到首次访问之前的技术。在 Kotlin 中，惰性初始化是使用 by 关键字完成的。

以下是具有延迟初始化属性 name 的 Kotlin 类的简单示例：

```kotlin
class Person {
  
    val name: String by lazy {
        // ...
    }
}
```

在上面的示例中，name 属性被声明为 val（不可变）并延迟初始化。初始值设定项是一个 lambda 表达式，在首次访问属性时调用。

Kotlin 还支持委托属性。委托属性是由委托对象实现的属性。在 Kotlin 中，委托属性是使用 by 关键字声明的。

下面是一个带有委托属性 name 的 Kotlin 类的简单示例：

```kotlin
class Person(val name: String) {
  
    val nameDelegate: Delegate by lazy {
        Delegate(name)
    }
}
```

在上面的示例中，名称属性由委托对象实现。委托对象由 lambda 表达式延迟初始化。

Kotlin 还支持扩展属性。扩展属性是声明为类扩展的属性。在 Kotlin 中，扩展属性是使用 by 关键字声明的。

以下是具有扩展属性名称的 Kotlin 类的简单示例：

```kotlin
class Person(val name: String) {
  
    val nameExtension: String by lazy {
        name.extension()
    }
}
```

在上面的示例中，name 属性由调用 extension() 方法的惰性 lambda 表达式扩展。

Kotlin 还支持后期初始化的属性。延迟初始化的属性是在首次访问之前未初始化的属性。在 Kotlin 中，延迟初始化的属性是使用 by 关键字声明的。

以下是具有延迟初始化属性名称的 Kotlin 类的简单示例：

```kotlin
class Person {
  
    lateinit var name: String
    
    fun init() {
        name = "John"
    }
}
```

在上面的示例中，name 属性被声明为 lateinit var（可变）。在调用 init() 方法之前，它不会被初始化。

Kotlin 还支持可空类型。可空类型是可以保存空值的类型。在 Kotlin 中，可空类型使用 ?操作员。

以下是具有可空属性名称的 Kotlin 类的简单示例：

```kotlin
class Person {
  
    var name: String? = null
}
```

在上面的示例中，name 属性被声明为可为 null 的类型。它可以保存值 null。

Kotlin 还支持不可变属性。不可变属性是在初始化后不能更改的属性。在 Kotlin 中，不可变属性是使用 val 关键字声明的。

以下是具有不可变属性 name 的 Kotlin 类的简单示例：

```kotlin
class Person(val name: String) {
  
}
```

在上面的示例中，name 属性被声明为 val（不可变）。初始化后不能更改。

Kotlin 还支持可变属性。可变属性是在初始化后可以更改的属性。在 Kotlin 中，可变属性是使用 var 关键字声明的。

以下是具有可变属性名称的 Kotlin 类的简单示例：

```kotlin
class Person {
  
    var name: String = ""
}
```

在上面的示例中，name 属性被声明为 var（可变）。它可以在初始化后更改。

Kotlin 还支持支持字段。支持字段是用于存储属性值的变量。在 Kotlin 中，支持字段是使用 field 关键字声明的。

以下是带有支持字段名称的 Kotlin 类的简单示例：

```kotlin
class Person {
  
    var name: String = ""
        private set
}
```

在上面的示例中，name 属性有一个支持字段。支持字段被声明为私有集，这意味着它只能由属性的设置者修改。

Kotlin 还支持委托属性。委托属性是由委托对象实现的属性。在 Kotlin 中，委托属性是使用 by 关键字声明的。

下面是一个带有委托属性 name 的 Kotlin 类的简单示例：

```kotlin
class Person(val name: String) {
  
    val nameDelegate: Delegate by lazy {
        Delegate(name)
    }
}
```

在上面的示例中，名称属性由委托对象实现。委托对象由 lambda 表达式延迟初始化。

Kotlin 还支持扩展属性。扩展属性是声明为类扩展的属性。在 Kotlin 中，扩展属性是使用 by 关键字声明的。

以下是具有扩展属性名称的 Kotlin 类的简单示例：

```kotlin
class Person(val name: String) {
  
    val nameExtension: String by lazy {
        name.extension()
    }
}
```

在上面的示例中，name 属性由调用 extension() 方法的惰性 lambda 表达式扩展。

Kotlin 还支持后期初始化的属性。延迟初始化的属性是在首次访问之前未初始化的属性。在 Kotlin 中，延迟初始化的属性是使用 by 关键字声明的。

以下是具有延迟初始化属性名称的 Kotlin 类的简单示例：

```kotlin
class Person {
  
    lateinit var name: String
    
    fun init() {
        name = "John"
    }
}
```

在上面的示例中，name 属性被声明为 lateinit var（可变）。在调用 init() 方法之前，它不会被初始化。

Kotlin 还支持可空类型。可空类型是可以保存空值的类型。在 Kotlin 中，可空类型使用 ?操作员。

以下是具有可空属性名称的 Kotlin 类的简单示例：

```kotlin
class Person {
  
    var name: String? = null
}
```

在上面的示例中，name 属性被声明为可为 null 的类型。它可以保存值 null。

Kotlin 还支持不可变属性。不可变属性是在初始化后不能更改的属性。在 Kotlin 中，不可变属性是使用 val 关键字声明的。

以下是具有不可变属性 name 的 Kotlin 类的简单示例：

```kotlin
class Person(val name: String) {
  
}
```

在上面的示例中，name 属性被声明为 val（不可变）。初始化后不能更改。

Kotlin 还支持可变属性。可变属性是在初始化后可以更改的属性。在 Kotlin 中，可变属性是使用 var 关键字声明的。

以下是具有可变属性名称的 Kotlin 类的简单示例：

```kotlin
class Person {
  
    var name: String = ""
}
```

在上面的示例中，name 属性被声明为 var（可变）。它可以在初始化后更改。

Kotlin 还支持支持字段。支持字段是用于存储属性值的变量。在 Kotlin 中，支持字段是使用 field 关键字声明的。

以下是带有支持字段名称的 Kotlin 类的简单示例：

```kotlin
class Person {
  
    var name: String = ""
        private set
}
```

在上面的示例中，name 属性有一个支持字段。支持字段被声明为私有集，这意味着它只能由属性的设置者修改。

Kotlin 还支持委托属性。委托属性是由委托对象实现的属性。在 Kotlin 中，委托属性是使用 by 关键字声明的。

下面是一个带有委托属性 name 的 Kotlin 类的简单示例：

```kotlin
class Person(val name: String) {
  
    val nameDelegate: Delegate by lazy {
        Delegate(name)
    }
}
```

在上面的示例中，名称属性由委托对象实现。委托对象由 lambda 表达式延迟初始化。

Kotlin 还支持扩展属性。扩展属性是声明为类扩展的属性。在 Kotlin 中，扩展属性是使用 by 关键字声明的。

以下是具有扩展属性名称的 Kotlin 类的简单示例：

```kotlin
class Person(val name: String) {
  
    val nameExtension: String by lazy {
        name.extension()
    }
}
```

在上面的示例中，name 属性由调用 extension() 方法的惰性 lambda 表达式扩展。

Kotlin 还支持后期初始化的属性。延迟初始化的属性是在首次访问之前未初始化的属性。在 Kotlin 中，延迟初始化的属性是使用 by 关键字声明的。

以下是具有延迟初始化属性名称的 Kotlin 类的简单示例：

```kotlin
class Person {
  
    lateinit var name: String
    
    fun init() {
        name = "John"
    }
}
```

在上面的示例中，name 属性被声明为 lateinit var（可变）。在调用 init() 方法之前，它不会被初始化。

Kotlin 还支持可空类型。可空类型是可以保存空值的类型。在 Kotlin 中，可空类型使用 ?操作员。

以下是具有可空属性名称的 Kotlin 类的简单示例：

```kotlin
class Person {
  
    var name: String? = null
}
```

在上面的示例中，name 属性被声明为可为 null 的类型。它可以保存值 null。

Kotlin 还支持不可变属性。不可变属性是在初始化后不能更改的属性。在 Kotlin 中，不可变属性是使用 val 关键字声明的。

以下是具有不可变属性 name 的 Kotlin 类的简单示例：

```kotlin
class Person(val name: String) {
  
}
```

在上面的示例中，name 属性被声明为 val（不可变）。初始化后不能更改。

Kotlin 还支持可变属性。可变属性是在初始化后可以更改的属性。在 Kotlin 中，可变属性是使用 var 关键字声明的。

以下是具有可变属性名称的 Kotlin 类的简单示例：

```kotlin
class Person {
  
    var name: String = ""
}
```

在上面的示例中，name 属性被声明为 var（可变）。它可以在初始化后更改。

Kotlin 还支持支持字段。支持字段是用于存储属性值的变量。在 Kotlin 中，支持字段是使用 field 关键字声明的。

以下是带有支持字段名称的 Kotlin 类的简单示例：

```kotlin
class Person {
  
    var name: String = ""
        private set
}
```

在上面的示例中，name 属性有一个支持字段。支持字段被声明为私有集，这意味着它只能由属性的设置者修改。

Kotlin 还支持委托属性。委托属性是由委托对象实现的属性。在 Kotlin 中，委托属性是使用 by 关键字声明的。

下面是一个带有委托属性 name 的 Kotlin 类的简单示例：

```kotlin
class Person(val name: String) {
  
    val nameDelegate: Delegate by lazy {
        Delegate(name)
    }
}
```

在上面的示例中，名称属性由委托对象实现。委托对象由 lambda 表达式延迟初始化。

Kotlin 还支持扩展属性。扩展属性是声明为类扩展的属性。在 Kotlin 中，扩展属性是使用 by 关键字声明的。

以下是具有扩展属性名称的 Kotlin 类的简单示例：

```kotlin
class Person(val name: String) {
  
    val nameExtension: String by lazy {
        name.extension()
    }
}
```

在上面的示例中，name 属性由调用 extension() 方法的惰性 lambda 表达式扩展。

Kotlin 还支持后期初始化的属性。延迟初始化的属性是在首次访问之前未初始化的属性。在 Kotlin 中，延迟初始化的属性是使用 by 关键字声明的。

以下是具有延迟初始化属性名称的 Kotlin 类的简单示例：

```科特林
类人{
  
    lateinit 变量名称：字符串
    
    有趣的初始化（）{
        名字=“约翰”
    }
}
``