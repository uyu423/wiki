---
title: 060: Interoperability with Java in Kotlin: Working Seamlessly with Java Code
description: 
published: true
date: 2023-02-16T21:32:50.145Z
tags: 
editor: markdown
dateCreated: 2023-02-16T21:32:41.776Z
---

- [060: Interoperabilidad con Java en Kotlin: trabajar sin problemas con código Java***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/060-interoperability-with-java-in-kotlin-working-seamlessly-with-java-code)
{.links-list}
- [060：Kotlin 中与 Java 的互操作性：与 Java 代码无缝协作***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/060-interoperability-with-java-in-kotlin-working-seamlessly-with-java-code)
{.links-list}
- [060: Kotlin에서 Java와의 상호 운용성: Java 코드로 원활하게 작업***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/060-interoperability-with-java-in-kotlin-working-seamlessly-with-java-code)
{.links-list}


# Interoperability with Java in Kotlin: Working Seamlessly with Java Code

As the official programming language for Android, Java has been the go-to choice for many developers. However, Kotlin is a rising star in the world of programming languages, offering many features that make it a great alternative to Java.

One of the biggest advantages of Kotlin is its interoperability with Java. This means that you can easily use Kotlin with existing Java code, and vice versa. In this post, we'll take a look at how to interoperate with Java code in Kotlin, and some of the benefits that this offers.

## Calling Java code from Kotlin

One of the most common scenarios is calling Java code from Kotlin. This is usually straightforward, as Kotlin is designed to work well with Java.

For example, let's say we have a Java class like this:

```java
public class MyJavaClass {
    public static void doSomething() {
        System.out.println("Doing something in Java!");
    }
}
```

We can call the `doSomething` method from Kotlin like this:

```kotlin
MyJavaClass.doSomething()
```

Kotlin also makes it easy to call Java code that uses generics. For example, let's say we have a Java method like this:

```java
public static <T> T getValue(T defaultValue) {
    return defaultValue;
}
```

We can call this method from Kotlin like this:

```kotlin
val result = getValue("Hello, world!")
```

Kotlin also supports Java's varargs feature, which allows a method to accept a variable number of arguments. For example, let's say we have a Java method like this:

```java
public static void printValues(String... values) {
    for (String value : values) {
        System.out.println(value);
    }
}
```

We can call this method from Kotlin like this:

```kotlin
printValues("Hello", "world", "!")
```

## Calling Kotlin code from Java

It's also possible to call Kotlin code from Java. Kotlin code is compiled to Java bytecode, so it can be used just like any other Java code.

For example, let's say we have a Kotlin class like this:

```kotlin
class MyKotlinClass {
    fun doSomething() {
        println("Doing something in Kotlin!")
    }
}
```

We can call the `doSomething` method from Java like this:

```java
MyKotlinClass kotlinClass = new MyKotlinClass();
kotlinClass.doSomething();
```

Kotlin also supports features like generics, null safety, and lambdas, which can be called from Java.

## The benefits of interoperability

Interoperability between Kotlin and Java has many benefits.

One of the biggest benefits is that it allows developers to slowly migrate from Java to Kotlin, without having to rewrite their entire codebase. This can be a big advantage for projects with a lot of legacy Java code.

Another benefit is that it allows developers to use the best of both languages. Kotlin and Java have many features that are similar, but there are also some key differences. By using both languages, developers can take advantage of the features of each language that are most appropriate for their needs.

## Conclusion

In this post, we've looked at how Kotlin interoperates with Java. We've seen how Kotlin code can be called from Java, and how Java code can be called from Kotlin. We've also seen some of the benefits that this offers.

If you're interested in learning more about Kotlin, check out the resources below.

## Additional Information

* [Kotlin for Java Developers](https://kotlinlang.org/docs/reference/java-to-kotlin-interop.html)
* [Java Interop](https://kotlinlang.org/docs/reference/java-interop.html)