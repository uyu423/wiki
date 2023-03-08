---
title: 017: Generics in Kotlin: Writing Reusable Code with Type Parameters
description: 
published: true
date: 2023-02-02T02:57:47.656Z
tags: 
editor: markdown
dateCreated: 2023-02-02T02:57:43.267Z
---

- [017: Genéricos en Kotlin: escribir código reutilizable con parámetros de tipo***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/017-generics-in-kotlin-writing-reusable-code-with-type-parameters)
{.links-list}
- [017：Kotlin 中的泛型：使用类型参数编写可重用代码***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/017-generics-in-kotlin-writing-reusable-code-with-type-parameters)
{.links-list}
- [017: Kotlin의 제네릭: 유형 매개변수로 재사용 가능한 코드 작성***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/017-generics-in-kotlin-writing-reusable-code-with-type-parameters)
{.links-list}


# Generics in Kotlin: Writing Reusable Code with Type Parameters

Kotlin's type system is designed to help you get more done with less code. One of the ways it does this is by allowing you to write code that is generic, or reusable across a range of types. In this post, we'll take a look at how generics work in Kotlin and how you can use them to write more concise and expressive code.

## What are Generics?

Generics are a feature of many programming languages that allow you to write code that can work with multiple types. This is opposed to code that is specific to one type, like an `Int` or a `String`.

One of the most common examples of generics is the `List` type. A `List` can contain elements of any type, so it is said to be _generic_. In Kotlin, we can create a `List` of `Int`s like this:

```kotlin
val list: List<Int> = listOf(1, 2, 3)
```

We can also create a `List` of `String`s:

```kotlin
val list: List<String> = listOf("a", "b", "c")
```

As you can see, the only thing that changes between these two `List`s is the type of the elements they contain. The `List` type itself is generic.

## Why Use Generics?

Generics are useful because they allow you to write code that can be used with multiple types. This can make your code more concise and expressive.

For example, consider the following code that prints out the elements of a `List`:

```kotlin
fun printList(list: List<Any>) {
    for (element in list) {
        println(element)
    }
}
```

This code will work with any `List`, regardless of the type of its elements. We can use it to print out a `List` of `Int`s:

```kotlin
val list: List<Int> = listOf(1, 2, 3)
printList(list)
```

And we can use it to print out a `List` of `String`s:

```kotlin
val list: List<String> = listOf("a", "b", "c")
printList(list)
```

If we didn't use generics, we would have to write two different functions, one for `List`s of `Int`s and one for `List`s of `String`s. Generics allow us to write one function that can be used with multiple types.

## How Do Generics Work?

Generics in Kotlin are implemented using _type parameters_. A type parameter is a placeholder for a specific type. When you create a generic type, you specify one or more type parameters. For example, the `List` type has a type parameter called `T`.

When you create an instance of a generic type, you specify the type that the type parameter should be replaced with. For example, when we create a `List<Int>`, we are specifying that the type parameter `T` should be replaced with the type `Int`.

## Using Type Parameters

Type parameters can be used in a number of ways. The most common is to specify the type of the elements in a collection. For example, the `List` type has a type parameter that specifies the type of the elements in the `List`.

We've already seen how to use type parameters to specify the type of the elements in a `List`. We can also use type parameters to specify the type of the keys and values in a `Map`:

```kotlin
val map: Map<String, Int> = mapOf("a" to 1, "b" to 2, "c" to 3)
```

In this example, we've specified that the type of the keys in the `Map` should be `String` and the type of the values should be `Int`.

Type parameters can also be used to specify the type of the values in a `Nullable` type:

```kotlin
val nullable: String? = null
```

In this example, we've specified that the type of the value in the `Nullable` type should be `String`.

## Declaring Type Parameters

When you create a generic type, you specify one or more type parameters. For example, the `List` type has a type parameter called `T`.

You can declare type parameters by using the `typeparam` keyword. For example, we can create a generic type called `MyType` with a type parameter called `T` like this:

```kotlin
typealias MyType<T> = T
```

## Bounds

Sometimes you may want to restrict the types that can be used as a type parameter. For example, you may want to specify that the type parameter must be a subtype of `Any`. Kotlin calls this a _upper bound_.

You can specify an upper bound by using the `where` keyword. For example, we can create a generic type called `MyType` with a type parameter called `T` that has an upper bound of `Any` like this:

```kotlin
typealias MyType<T> where T : Any
```

In this example, we've specified that the type parameter `T` must be a subtype of `Any`. This means that we can use any type as the type parameter `T`, including `Int`, `String`, `List`, and so on.

We can also specify a lower bound by using the `where` keyword. For example, we can create a generic type called `MyType` with a type parameter called `T` that has a lower bound of `Any` like this:

```kotlin
typealias MyType<T> where T : Any
```

In this example, we've specified that the type parameter `T` must be a supertype of `Any`. This means that we can use any type as the type parameter `T`, including `Any`, `Any?`, and so on.

## Wildcards

Sometimes you may want to use a type parameter without specifying its type. For example, you may want to create a function that can print out the elements of any `List`.

In Kotlin, you can use a _wildcard_ to specify that a type parameter can be any type. For example, we can create a function that prints out the elements of any `List` like this:

```kotlin
fun printList(list: List<*>) {
    for (element in list) {
        println(element)
    }
}
```

In this example, we've used a wildcard to specify that the type parameter `T` can be any type. This means that we can use the `printList` function with any `List`, regardless of the type of its elements.

## Conclusion

In this post, we've taken a look at how generics work in Kotlin. We've seen how to use type parameters to write more concise and expressive code. We've also seen how to declare type parameters and how to use bounds and wildcards.