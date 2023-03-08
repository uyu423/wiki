---
title: Using Type Aliases in Kotlin
description: 
published: true
date: 2023-02-08T12:17:21.544Z
tags: 
editor: markdown
dateCreated: 2023-02-08T12:17:15.701Z
---

- [Uso de alias de tipo en Kotlin***Spanish** document is available*](/es/Knowledge-base/Kotlin/using-type-aliases-in-kotlin)
{.links-list}
- [在 Kotlin 中使用类型别名***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/using-type-aliases-in-kotlin)
{.links-list}
- [Kotlin에서 유형 별칭 사용***Korean** document is available*](/ko/Knowledge-base/Kotlin/using-type-aliases-in-kotlin)
{.links-list}


# Using Type Aliases in Kotlin

Type aliases are a great way to improve the readability of your code, especially when working with long generic types. In Kotlin, you can use type aliases to create an alias for a type, which can then be used instead of the original type. This can be especially useful when working with generic types, as it can make your code much easier to read and understand.

To create a type alias, you use the keyword `typealias`, followed by the alias name and the type that you want to alias. For example, let's say we have a generic type `Person<T>`, where `T` is the type of the person's name. We could create a type alias for this type as follows:

```kotlin
typealias PersonName = Person<String>
```

Now, instead of using `Person<String>` everywhere in our code, we can just use `PersonName`. This can make our code much easier to read, as it's clear what `PersonName` refers to.

It's also worth noting that type aliases are not just limited to generic types. You can use them for any type, including regular classes, interfaces, and even other type aliases.

One final note on type aliases is that they are not interchangeable with the original types. This means that you cannot use a type alias where the original type is expected. For example, the following code will not compile:

```kotlin
fun main() {
    val list: List<String> = listOf("a", "b", "c")
    val personNameList: PersonNameList = list // Error: Type mismatch
}
```

This is because `List<String>` is not the same type as `PersonNameList`. If you want to be able to use a type alias where the original type is expected, you can use the `inline` keyword. This is outside the scope of this article, but you can read more about it [here](https://kotlinlang.org/docs/reference/inline-classes.html).

## References

- [Kotlin Type Aliases](https://kotlinlang.org/docs/reference/type-aliases.html)
- [Kotlin Inline Classes](https://kotlinlang.org/docs/reference/inline-classes.html)