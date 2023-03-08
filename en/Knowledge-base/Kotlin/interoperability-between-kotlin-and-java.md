---
title: Interoperability Between Kotlin and Java
description: 
published: true
date: 2023-02-09T08:55:21.728Z
tags: 
editor: markdown
dateCreated: 2023-02-09T08:55:20.015Z
---

- [Interoperabilidad entre Kotlin y Java***Spanish** document is available*](/es/Knowledge-base/Kotlin/interoperability-between-kotlin-and-java)
{.links-list}
- [Kotlin 和 Java 之间的互操作性***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/interoperability-between-kotlin-and-java)
{.links-list}
- [Kotlin과 Java 간의 상호 운용성***Korean** document is available*](/ko/Knowledge-base/Kotlin/interoperability-between-kotlin-and-java)
{.links-list}



# Interoperability Between Kotlin and Java

Java and Kotlin are two popular programming languages used for developing Android apps. While Kotlin is a newer language, it is fully interoperable with Java. This means that you can use Kotlin and Java together in the same project, and that you can call Kotlin code from Java and vice versa. In this article, we will take a look at how Kotlin and Java interoperate and how you can use both languages in your Android app development.

## Calling Kotlin from Java

Calling Kotlin from Java is seamless and straightforward. You can call any Kotlin code from your Java code, and vice versa. There is no need to add any special annotations or configuration.

To call Kotlin code from Java, simply use the fully qualified name of the Kotlin class, method, or property. For example, to call the `foo()` function in the `Foo` class from Java, you would use the following code:

```java
FooKt.foo();
```

To call Java code from Kotlin, use the `@JvmName` annotation. This annotation allows you to specify the name of the Kotlin function or property that will be used when calling it from Java. For example, the following Kotlin code:

```kotlin
@JvmName("bar")
fun foo() {
    // ...
}
```

Can be called from Java using the following code:

```java
FooKt.bar();
```

## Working with Nullable and Non-Null Types

Kotlin has nullable and non-null types, which help to prevent null pointer exceptions. In Kotlin, any type can be made nullable by adding a `?` after the type name. For example, the following Kotlin code defines a nullable `String`:

```kotlin
var s: String? = null
```

When calling Kotlin code from Java, all nullable types are automatically converted to their non-null counterparts. For example, the following Kotlin code:

```kotlin
fun foo(s: String?) {
    // ...
}
```

Can be called from Java using the following code:

```java
foo("Hello");
```

## Working with Java Collections

Kotlin and Java have very different approaches to collections. In Kotlin, all collections are immutable by default, while in Java they are mutable. This can trip up developers who are used to working with Java collections.

Fortunately, Kotlin provides easy ways to convert between Kotlin and Java collections. To convert a Java collection to a Kotlin one, you can use the `toMutableList()` or `toList()` functions. For example, the following Java code:

```java
List<String> list = Arrays.asList("a", "b", "c");
```

Can be converted to a Kotlin `List` using the `toList()` function:

```kotlin
val list = list.toList()
```

To convert a Kotlin collection to a Java one, you can use the `toJavaList()` or `toJavaSet()` functions. For example, the following Kotlin code:

```kotlin
val list = listOf("a", "b", "c")
```

Can be converted to a Java `List` using the `toJavaList()` function:

```java
List<String> list = list.toJavaList();
```

## Conclusion

Kotlin and Java are two popular programming languages that are fully interoperable. This means that you can use Kotlin and Java together in the same project, and that you can call Kotlin code from Java and vice versa. In this article, we have taken a look at how Kotlin and Java interoperate and how you can use both languages in your Android app development.