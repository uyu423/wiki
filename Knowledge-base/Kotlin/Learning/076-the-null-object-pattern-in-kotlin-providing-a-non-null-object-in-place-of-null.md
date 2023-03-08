---
title: 076: Kotlin의 Null 개체 패턴: Null 대신 Null이 아닌 개체 제공
description: 
published: true
date: 2023-02-17T05:32:33.308Z
tags: 
editor: markdown
dateCreated: 2023-02-17T05:32:25.016Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [076: The Null Object Pattern in Kotlin: Providing a Non-Null Object in Place of Null***English** document is available*](/en/Knowledge-base/Kotlin/Learning/076-the-null-object-pattern-in-kotlin-providing-a-non-null-object-in-place-of-null)
{.links-list}


# Kotlin의 Null 객체 패턴: Null 대신 Null이 아닌 객체 제공

Kotlin의 유형 시스템은 null 값이 필요하지 않도록 설계되었습니다. 그러나 Java로 작성된 레거시 코드와 인터페이스할 때와 같이 null 값이 필요한 경우가 있습니다. 이러한 경우 null 개체 패턴을 사용하여 null 값 대신 null이 아닌 개체를 제공할 수 있습니다.

## Null 객체 패턴이란 무엇입니까?

null 개체 패턴은 null 값의 필요성을 제거하는 것을 목표로 하는 디자인 패턴입니다. null 값 대신 null이 아닌 개체를 제공하여 이를 수행합니다. 이 null이 아닌 개체는 값이 없음을 나타내는 데 사용할 수 있습니다.

## Null 개체 패턴은 어떻게 작동합니까?

null 객체 패턴은 값이 없음을 나타내는 객체를 생성하여 작동합니다. 이 개체는 null 값 대신 사용할 수 있습니다. 개체에 빈 문자열과 같은 기본값을 지정하거나 상황에 적합한 동작을 지정할 수 있습니다.

## Null 객체 패턴은 언제 사용해야 합니까?

Java로 작성된 레거시 코드와 인터페이스할 때와 같이 null 값이 필요한 경우 null 객체 패턴을 사용해야 합니다.

## Null 객체 패턴의 이점은 무엇입니까?

null 개체 패턴에는 다음과 같은 몇 가지 이점이 있습니다.

- null 값이 필요하지 않습니다.
- 코드를 더 읽기 쉽게 만듭니다.
- 코드를 유지 관리하기 쉽게 만듭니다.
- 코드를 더 확장 가능하게 만듭니다.

## Null 객체 패턴의 단점은 무엇인가요?

null 개체 패턴에는 한 가지 단점이 있습니다.

- 코드가 복잡해질 수 있습니다.

## 코틀린 구현

다음 단계를 사용하여 Kotlin에서 null 객체 패턴을 구현할 수 있습니다.

1. 개체에 대한 인터페이스를 만듭니다.
2. 인터페이스를 구현하는 클래스를 만듭니다.
3. 값이 없음을 나타내는 개체를 만듭니다.

### 1단계: 개체에 대한 인터페이스 만들기

첫 번째 단계는 개체에 대한 인터페이스를 만드는 것입니다. 이 인터페이스는 개체에 대한 계약을 정의합니다.

```kotlin
interface MyInterface {
    fun doSomething()
}
```

### 2단계: 인터페이스를 구현하는 클래스 만들기

두 번째 단계는 인터페이스를 구현하는 클래스를 만드는 것입니다. 이 클래스는 개체에 대한 구현을 제공합니다.

```kotlin
class MyClass : MyInterface {
    override fun doSomething() {
        // do something
    }
}
```

### 3단계: 값이 없음을 나타내는 개체 만들기

세 번째 단계는 값이 없음을 나타내는 개체를 만드는 것입니다. 이 개체는 null 값 대신 사용할 수 있습니다.

```kotlin
object MyObject : MyInterface {
    override fun doSomething() {
        // do something
    }
}
```

## 용법

null 개체 패턴은 다음과 같이 사용할 수 있습니다.

```kotlin
fun doSomething(myInterface: MyInterface?) {
    if (myInterface != null) {
        myInterface.doSomething()
    }
}

fun main() {
    val myClass: MyClass? = MyClass()
    val myObject: MyObject? = MyObject()

    doSomething(myClass)
    doSomething(myObject)
}
```

## 추가 정보

- null 개체 패턴은 더미 개체 패턴이라고도 합니다.

## 경고

- null 개체 패턴은 null 값이 필요한 경우에만 사용해야 합니다.

## 위험

- null 개체 패턴은 코드에 복잡성을 추가할 수 있습니다.