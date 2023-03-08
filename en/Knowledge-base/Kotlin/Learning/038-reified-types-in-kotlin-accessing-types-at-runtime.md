---
title: 038: Reified Types in Kotlin: Accessing Types at Runtime
description: 
published: true
date: 2023-02-02T01:57:42.766Z
tags: 
editor: markdown
dateCreated: 2023-02-02T01:57:37.407Z
---

- [038: Tipos cosificados en Kotlin: Acceso a tipos en tiempo de ejecución***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/038-reified-types-in-kotlin-accessing-types-at-runtime)
{.links-list}
- [038：Kotlin 中的具体类型：在运行时访问类型***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/038-reified-types-in-kotlin-accessing-types-at-runtime)
{.links-list}
- [038: Kotlin의 구체화된 유형: 런타임에 유형에 액세스***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/038-reified-types-in-kotlin-accessing-types-at-runtime)
{.links-list}


# Introduction

Kotlin is a statically typed language that runs on the JVM. It has excellent interoperability with Java and is a great choice for developing Android applications.

One of Kotlin's most powerful features is its support for reified types. This allows you to access types at runtime, which is not possible in Java.

In this post, we'll take a look at what reified types are and how they can be used in Kotlin. We'll also see some examples of how reified types can be used to make development easier.

# What are reified types?

Reified types are types that can be accessed at runtime. This is not possible in Java, where types are only available at compile time.

Reified types are very useful for working with reflection. Reflection is a way of dynamically accessing classes and their members at runtime. It's often used in frameworks and libraries.

In Kotlin, reified types are declared with the keyword `reified`. For example, we can declare a reified type like this:

```kotlin
reified val myType: String = "Hello, world!"
```

Now we can access the type of `myType` at runtime:

```kotlin
val type = myType::class
```

The `type` variable will contain the `String` class.

We can also access the type of a generic type:

```kotlin
reified val myList: List<String> = listOf("Hello", "world!")

val type = myList::class
```

The `type` variable will contain the `List` class.

# How can reified types be used?

Reified types can be used in a number of ways. We'll look at some of the most common use cases.

## Working with reflection

As we've seen, reified types are very useful for working with reflection. Reflection is a way of dynamically accessing classes and their members at runtime.

In Java, reflection is often used in frameworks and libraries. For example, the Spring framework uses reflection to dynamically create objects.

In Kotlin, we can use reflection to access the members of a class:

```kotlin
reified val myClass: MyClass = MyClass()

val members = myClass::class.members
```

The `members` variable will contain a list of all the members of the `MyClass` class.

We can also use reflection to access the annotations of a class:

```kotlin
reified val myClass: MyClass = MyClass()

val annotations = myClass::class.annotations
```

The `annotations` variable will contain a list of all the annotations of the `MyClass` class.

## Working with generic types

Reified types are also very useful for working with generic types. In Java, it's not possible to access the type of a generic type at runtime. This can make it difficult to work with generic types.

In Kotlin, we can use reified types to access the type of a generic type:

```kotlin
reified val myList: List<String> = listOf("Hello", "world!")

val type = myList::class
```

The `type` variable will contain the `List` class.

We can also use reified types to create generic types:

```kotlin
inline fun <reified T> createList(): List<T> {
    return listOf()
}

val myList = createList<String>()
```

The `myList` variable will contain an empty `List<String>`.

## Working with Kotlin reflection

Kotlin reflection is a way of dynamically accessing Kotlin classes and their members at runtime. It's very similar to Java reflection, but it's much easier to use.

In Kotlin, we can use reified types to access the members of a class:

```kotlin
reified val myClass: MyClass = MyClass()

val members = myClass::class.members
```

The `members` variable will contain a list of all the members of the `MyClass` class.

We can also use reified types to access the annotations of a class:

```kotlin
reified val myClass: MyClass = MyClass()

val annotations = myClass::class.annotations
```

The `annotations` variable will contain a list of all the annotations of the `MyClass` class.

# Conclusion

In this post, we've seen what reified types are and how they can be used in Kotlin. We've also seen some examples of how reified types can be used to make development easier.

Reified types are a powerful feature of Kotlin that can be used in a variety of ways. If you're working with reflection or generic types, reified types can be a great help.