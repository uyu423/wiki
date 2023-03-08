---
title: 023: Type Aliases in Kotlin: Shortening Long Class Names
description: 
published: true
date: 2023-02-01T20:17:25.701Z
tags: 
editor: markdown
dateCreated: 2023-02-01T20:17:24.108Z
---

- [023: Tipo de alias en Kotlin: acortamiento de nombres de clase largos***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/023-type-aliases-in-kotlin-shortening-long-class-names)
{.links-list}
- [023：Kotlin 中的类型别名：缩短长类名***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/023-type-aliases-in-kotlin-shortening-long-class-names)
{.links-list}
- [023: Kotlin의 유형 별칭: 긴 클래스 이름 단축***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/023-type-aliases-in-kotlin-shortening-long-class-names)
{.links-list}


# 023: Type Aliases in Kotlin: Shortening Long Class Names

Kotlin has a great feature called type aliases that can be used to shorten long class names. For example, consider the following class name:

```kotlin
class MyVeryLongClassName {
    // ...
}
```

This class name is quite long and it would be nice if we could shorten it. We can do this using a type alias:

```kotlin
typealias MyClass = MyVeryLongClassName

class MyClass {
    // ...
}
```

Now, the `MyClass` alias can be used anywhere in our code instead of the long class name. This is especially useful when working with generic types:

```kotlin
typealias MyClass = MyVeryLongClassName

class MyClass<T> {
    // ...
}

fun main() {
    val myClass: MyClass<String> = MyClass()
}
```

In the example above, we have defined a type alias for the `MyVeryLongClassName` class. We can then use this alias when declaring variables of the generic type. This can make our code much easier to read and understand.

There are a few things to keep in mind when using type aliases:

- Type aliases are not the same as classes. They are simply a way to give a different name to a type.
- Type aliases cannot be used to create new types. They can only be used to give an existing type a new name.
- Type aliases cannot be used to change the type of a variable. They can only be used when declaring a new variable.

Overall, type aliases are a great way to shorten long class names and make our code more readable. They are especially useful when working with generic types.