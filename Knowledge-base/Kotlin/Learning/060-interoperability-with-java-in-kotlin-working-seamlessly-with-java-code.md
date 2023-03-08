---
title: 060: Kotlin에서 Java와의 상호 운용성: Java 코드로 원활하게 작업
description: 
published: true
date: 2023-02-16T21:32:43.993Z
tags: 
editor: markdown
dateCreated: 2023-02-16T21:32:41.771Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [060: Interoperability with Java in Kotlin: Working Seamlessly with Java Code***English** document is available*](/en/Knowledge-base/Kotlin/Learning/060-interoperability-with-java-in-kotlin-working-seamlessly-with-java-code)
{.links-list}


# Kotlin에서 Java와의 상호 운용성: Java 코드와 원활하게 작업

Android용 공식 프로그래밍 언어인 Java는 많은 개발자가 선택했습니다. 그러나 Kotlin은 프로그래밍 언어의 세계에서 떠오르는 별이며 Java를 대체할 수 있는 많은 기능을 제공합니다.

Kotlin의 가장 큰 장점 중 하나는 Java와의 상호 운용성입니다. 즉, 기존 Java 코드와 함께 Kotlin을 쉽게 사용할 수 있으며 그 반대도 가능합니다. 이 게시물에서는 Kotlin에서 Java 코드와 상호 운용하는 방법과 이것이 제공하는 몇 가지 이점을 살펴보겠습니다.

## Kotlin에서 Java 코드 호출

가장 일반적인 시나리오 중 하나는 Kotlin에서 Java 코드를 호출하는 것입니다. Kotlin은 Java와 잘 작동하도록 설계되었기 때문에 일반적으로 간단합니다.

예를 들어 다음과 같은 Java 클래스가 있다고 가정해 보겠습니다.

```java
public class MyJavaClass {
    public static void doSomething() {
        System.out.println("Doing something in Java!");
    }
}
```

다음과 같이 Kotlin에서 `doSomething` 메서드를 호출할 수 있습니다.

```kotlin
MyJavaClass.doSomething()
```

또한 Kotlin을 사용하면 제네릭을 사용하는 Java 코드를 쉽게 호출할 수 있습니다. 예를 들어 다음과 같은 Java 메서드가 있다고 가정해 보겠습니다.

```java
public static <T> T getValue(T defaultValue) {
    return defaultValue;
}
```

다음과 같이 Kotlin에서 이 메서드를 호출할 수 있습니다.

```kotlin
val result = getValue("Hello, world!")
```

Kotlin은 또한 Java의 varargs 기능을 지원하여 메소드가 다양한 수의 인수를 허용할 수 있습니다. 예를 들어 다음과 같은 Java 메서드가 있다고 가정해 보겠습니다.

```java
public static void printValues(String... values) {
    for (String value : values) {
        System.out.println(value);
    }
}
```

다음과 같이 Kotlin에서 이 메서드를 호출할 수 있습니다.

```kotlin
printValues("Hello", "world", "!")
```

## Java에서 Kotlin 코드 호출

Java에서 Kotlin 코드를 호출하는 것도 가능합니다. Kotlin 코드는 Java 바이트코드로 컴파일되므로 다른 Java 코드처럼 사용할 수 있습니다.

예를 들어 다음과 같은 Kotlin 클래스가 있다고 가정해 보겠습니다.

```kotlin
class MyKotlinClass {
    fun doSomething() {
        println("Doing something in Kotlin!")
    }
}
```

다음과 같이 Java에서 `doSomething` 메서드를 호출할 수 있습니다.

```java
MyKotlinClass kotlinClass = new MyKotlinClass();
kotlinClass.doSomething();
```

Kotlin은 Java에서 호출할 수 있는 제네릭, null 안전 및 람다와 같은 기능도 지원합니다.

## 상호 운용성의 이점

Kotlin과 Java 간의 상호 운용성에는 많은 이점이 있습니다.

가장 큰 이점 중 하나는 개발자가 전체 코드베이스를 다시 작성하지 않고도 Java에서 Kotlin으로 천천히 마이그레이션할 수 있다는 것입니다. 이는 레거시 Java 코드가 많은 프로젝트에 큰 이점이 될 수 있습니다.

또 다른 이점은 개발자가 두 언어의 장점을 모두 사용할 수 있다는 것입니다. Kotlin과 Java에는 유사한 기능이 많이 있지만 몇 가지 중요한 차이점도 있습니다. 두 언어를 모두 사용함으로써 개발자는 필요에 가장 적합한 각 언어의 기능을 활용할 수 있습니다.

## 결론

이 게시물에서는 Kotlin이 Java와 상호 운용되는 방식을 살펴보았습니다. Java에서 Kotlin 코드를 호출하는 방법과 Kotlin에서 Java 코드를 호출하는 방법을 살펴보았습니다. 우리는 또한 이것이 제공하는 몇 가지 이점을 보았습니다.

Kotlin에 대해 자세히 알아보려면 아래 리소스를 확인하세요.

## 추가 정보

* [Java 개발자를 위한 Kotlin](https://kotlinlang.org/docs/reference/java-to-kotlin-interop.html)
* [자바 상호 운용성](https://kotlinlang.org/docs/reference/java-interop.html)