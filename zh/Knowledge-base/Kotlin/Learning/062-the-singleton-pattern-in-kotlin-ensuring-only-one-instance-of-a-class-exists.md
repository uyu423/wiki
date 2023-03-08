---
title: 062：Kotlin 中的单例模式：确保一个类的唯一实例存在
description: 
published: true
date: 2023-02-16T23:32:26.287Z
tags: 
editor: markdown
dateCreated: 2023-02-16T23:32:18.297Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [062: The Singleton Pattern in Kotlin: Ensuring Only One Instance of a Class Exists***English** document is available*](/en/Knowledge-base/Kotlin/Learning/062-the-singleton-pattern-in-kotlin-ensuring-only-one-instance-of-a-class-exists)
{.links-list}


# Kotlin 中的单例模式：确保一个类只存在一个实例

单例模式是一种软件设计模式，它将类的实例化限制为一个对象。当我们只需要一个类的一个实例用于应用程序时，这很有用，例如当我们需要管理共享资源、处理全局状态或协调整个系统的操作时。

在 Kotlin 中，我们可以通过对象声明来实现单例。对象声明是具有私有构造函数和用于存储实例的公共静态字段的常规类的语法糖。

这是 Kotlin 中单例类的一个简单示例：

```kotlin
object MySingleton {
    fun doSomething() {
        // ...
    }
}
```

我们可以使用对象的名称来访问单例实例：

```kotlin
MySingleton.doSomething()
```

如果我们需要用一些参数初始化单例，我们可以使用伴生对象：

```kotlin
class MySingleton private constructor(val param: String) {
    companion object {
        fun getInstance(param: String): MySingleton {
            return MySingleton(param)
        }
    }

    fun doSomething() {
        // ...
    }
}
```

然后我们可以使用伴随对象的名称访问单例实例：

```kotlin
MySingleton.getInstance("some param").doSomething()
```

重要的是要注意，在 Kotlin 中，对象声明不是线程安全的。如果我们需要确保只创建该类的一个实例，我们需要使用同步块：

```kotlin
object MySingleton {
    @Volatile
    private var instance: MySingleton? = null

    fun getInstance(): MySingleton {
        return instance ?: synchronized(this) {
            instance ?: MySingleton().also { instance = it }
        }
    }

    fun doSomething() {
        // ...
    }
}
```

然后我们可以使用对象的名称访问单例实例：

```kotlin
MySingleton.getInstance().doSomething()
```

单例模式是管理全局状态和资源的有用工具。但是，应该谨慎使用它，因为它会导致代码紧耦合和难以测试的代码。

## 附加信息

* [维基百科：单例模式](https://en.wikipedia.org/wiki/Singleton_pattern)
* [Kotlin 语言文档：对象](https://kotlinlang.org/docs/reference/objects.html)

## 进一步阅读的资源

* [Kotlin 中的设计模式：单例模式](https://antonioleiva.com/kotlin-singleton/)
* [领域：Kotlin 单例辩论](https://academy.realm.io/posts/kotlin-singleton-debate/)
* [Android 开发者：单例和内存泄漏](https://developer.android.com/training/articles/memory.html# LeakCanary)