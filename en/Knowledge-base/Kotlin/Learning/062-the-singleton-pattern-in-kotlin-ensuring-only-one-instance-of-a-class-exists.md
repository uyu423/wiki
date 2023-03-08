---
title: 062: The Singleton Pattern in Kotlin: Ensuring Only One Instance of a Class Exists
description: 
published: true
date: 2023-02-16T23:32:20.281Z
tags: 
editor: markdown
dateCreated: 2023-02-16T23:32:18.302Z
---

- [062: El patrón Singleton en Kotlin: garantizar que solo exista una instancia de una clase***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/062-the-singleton-pattern-in-kotlin-ensuring-only-one-instance-of-a-class-exists)
{.links-list}
- [062：Kotlin 中的单例模式：确保一个类的唯一实例存在***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/062-the-singleton-pattern-in-kotlin-ensuring-only-one-instance-of-a-class-exists)
{.links-list}
- [062: Kotlin의 싱글톤 패턴: 클래스의 인스턴스가 하나만 존재하도록 보장***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/062-the-singleton-pattern-in-kotlin-ensuring-only-one-instance-of-a-class-exists)
{.links-list}


# The Singleton Pattern in Kotlin: Ensuring Only One Instance of a Class Exists

The singleton pattern is a software design pattern that restricts the instantiation of a class to one object. This is useful when we need to have only one instance of a class for the application, such as when we need to manage a shared resource, handle a global state, or coordinate actions across the system.

In Kotlin, we can implement a singleton by using an object declaration. An object declaration is a syntactic sugar for a regular class with a private constructor and a public static field for storing the instance.

Here's a simple example of a singleton class in Kotlin:

```kotlin
object MySingleton {
    fun doSomething() {
        // ...
    }
}
```

We can access the singleton instance by using the name of the object:

```kotlin
MySingleton.doSomething()
```

If we need to initialize the singleton with some parameters, we can use a companion object:

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

We can then access the singleton instance by using the name of the companion object:

```kotlin
MySingleton.getInstance("some param").doSomething()
```

It's important to note that, in Kotlin, the object declaration is not thread-safe. If we need to ensure that only one instance of the class is created, we need to use a synchronized block:

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

We can then access the singleton instance by using the name of the object:

```kotlin
MySingleton.getInstance().doSomething()
```

The singleton pattern is a useful tool for managing global state and resources. However, it should be used with caution, as it can lead to tightly coupled code and difficult-to-test code.

## Additional Information

* [Wikipedia: Singleton Pattern](https://en.wikipedia.org/wiki/Singleton_pattern)
* [Kotlin Language Documentation: Objects](https://kotlinlang.org/docs/reference/objects.html)

## Resources for Further Reading

* [Design Patterns in Kotlin: The Singleton Pattern](https://antonioleiva.com/kotlin-singleton/)
* [Realm: The Kotlin Singleton Debate](https://academy.realm.io/posts/kotlin-singleton-debate/)
* [Android Developers: Singletons and Memory Leaks](https://developer.android.com/training/articles/memory.html#LeakCanary)