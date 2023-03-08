---
title: 046: SAM (Single Abstract Method) Interfaces in Kotlin: Converting Java Interfaces to Kotlin Interfaces
description: 
published: true
date: 2023-02-05T21:55:22.009Z
tags: 
editor: markdown
dateCreated: 2023-02-05T21:55:16.378Z
---

- [046: Interfaces SAM (método abstracto único) en Kotlin: conversión de interfaces Java a interfaces Kotlin***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/046-sam-single-abstract-method-interfaces-in-kotlin-converting-java-interfaces-to-kotlin-interfaces)
{.links-list}
- [046：Kotlin 中的 SAM（单一抽象方法）接口：将 Java 接口转换为 Kotlin 接口***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/046-sam-single-abstract-method-interfaces-in-kotlin-converting-java-interfaces-to-kotlin-interfaces)
{.links-list}
- [046: Kotlin의 SAM(Single Abstract Method) 인터페이스: Java 인터페이스를 Kotlin 인터페이스로 변환***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/046-sam-single-abstract-method-interfaces-in-kotlin-converting-java-interfaces-to-kotlin-interfaces)
{.links-list}


# 046: SAM (Single Abstract Method) Interfaces in Kotlin: Converting Java Interfaces to Kotlin Interfaces

As Kotlin is a JVM language, it is fully compatible with Java. This means that you can take any Java interface and convert it to a Kotlin interface without any problems.

However, there is one caveat: Kotlin does not support SAM (Single Abstract Method) interfaces. This means that you cannot take a Java interface with a single abstract method and convert it to a Kotlin interface.

The reason for this is that Kotlin's type system is different from Java's. In Kotlin, every interface must have at least one abstract method, even if it is just a dummy method with no body.

This is not a problem if you are converting a Java interface with multiple abstract methods to Kotlin. However, if you are converting a SAM interface, you will need to add an abstract method to the Kotlin interface.

There is no easy way to do this, so you will need to add the abstract method manually. The best way to do this is to add a dummy method with no body. This will ensure that the Kotlin interface is compatible with the Java interface.

Here is an example of a Java SAM interface:

```java
public interface Runnable {
     public void run();
}
```

And here is the equivalent Kotlin interface:

```kotlin
interface Runnable {
    fun run()
}
```

As you can see, the Kotlin interface has an extra abstract method, ```run()```, which is required by the Kotlin type system.

If you are converting a Java interface to Kotlin, you should always check whether the interface is a SAM interface. If it is, you will need to add an extra abstract method to the Kotlin interface.