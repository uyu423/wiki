---
title: 044: Kotlin의 익명 내부 클래스: 이름 없이 클래스 만들기
description: 
published: true
date: 2023-02-15T10:17:49.350Z
tags: 
editor: markdown
dateCreated: 2023-02-15T10:17:47.749Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [044: Anonymous Inner Classes in Kotlin: Creating Classes Without Names***English** document is available*](/en/Knowledge-base/Kotlin/Learning/044-anonymous-inner-classes-in-kotlin-creating-classes-without-names)
{.links-list}


# Kotlin의 익명 내부 클래스: 이름 없이 클래스 만들기

Kotlin에서는 이름을 지정하지 않고 익명의 내부 클래스를 만들 수 있습니다. 이러한 클래스는 일회성 개체를 만들어야 하거나 제한된 범위에서만 사용되는 개체가 필요할 때 자주 사용됩니다.

익명 내부 클래스는 `object` 키워드를 사용하여 선언됩니다.

```kotlin
object: SomeClass() {
    // Body of the anonymous inner class
}
```

`object` 키워드를 사용하여 익명 내부 클래스의 상위 유형을 지정할 수도 있습니다.

```kotlin
object: SomeInterface {
    // Body of the anonymous inner class
}
```

## 클래스를 확장하는 익명의 내부 클래스 만들기

`Animal` 클래스를 확장하는 익명의 내부 클래스를 만들어 봅시다. `makeNoise` 메서드가 있는 `Animal` 클래스를 만듭니다. 이 메서드는 익명 내부 클래스에서 재정의됩니다.

```kotlin
open class Animal {
    open fun makeNoise() {
        println("Some noise")
    }
}

val animal = object: Animal() {
    override fun makeNoise() {
        println("Bark")
    }
}

animal.makeNoise() // Prints "Bark"
```

위의 코드에서 우리는 `Animal` 클래스와 이를 확장하는 익명 내부 클래스를 만들었습니다. 익명의 내부 클래스에서 `makeNoise` 메서드를 재정의합니다. `animal` 개체에서 `makeNoise` 메서드를 호출하면 "Bark"가 인쇄됩니다.

## 인터페이스를 구현하는 익명 내부 클래스 만들기

인터페이스를 구현하는 익명 내부 클래스를 만들 수도 있습니다. `makeNoise` 메서드로 `Animal` 인터페이스를 만들어 봅시다. 우리는 이 인터페이스를 구현하는 익명의 내부 클래스를 만들 것입니다.

```kotlin
interface Animal {
    fun makeNoise()
}

val animal = object: Animal {
    override fun makeNoise() {
        println("Some noise")
    }
}

animal.makeNoise() // Prints "Some noise"
```

위의 코드에서 우리는 `Animal` 인터페이스와 이를 구현하는 익명의 내부 클래스를 만들었습니다. 익명의 내부 클래스에서 `makeNoise` 메서드를 재정의합니다. `animal` 개체에서 `makeNoise` 메서드를 호출하면 "Some noise"가 인쇄됩니다.

## 클래스를 확장하고 인터페이스를 구현하는 익명 내부 클래스 만들기

클래스를 확장하고 인터페이스를 구현하는 익명의 내부 클래스를 만들 수도 있습니다. `makeNoise` 메서드로 `Animal` 인터페이스를 만들어 봅시다. 또한 `makeNoise` 메서드가 있는 `Animal` 클래스도 생성합니다. 우리는 `Animal` 클래스를 확장하고 `Animal` 인터페이스를 구현하는 익명의 내부 클래스를 만들 것입니다.

```kotlin
interface Animal {
    fun makeNoise()
}

open class Animal {
    open fun makeNoise() {
        println("Some noise")
    }
}

val animal = object: Animal(), Animal {
    override fun makeNoise() {
        println("Bark")
    }
}

animal.makeNoise() // Prints "Bark"
```

위의 코드에서 `Animal` 클래스와 `Animal` 인터페이스를 만들었습니다. 우리는 `Animal` 클래스를 확장하고 `Animal` 인터페이스를 구현하는 익명의 내부 클래스를 만들었습니다. 익명의 내부 클래스에서 `makeNoise` 메서드를 재정의합니다. `animal` 개체에서 `makeNoise` 메서드를 호출하면 "Bark"가 인쇄됩니다.

## 익명 내부 클래스의 객체 생성

익명 내부 클래스를 생성하면 해당 클래스의 객체도 생성됩니다. `object` 키워드를 사용하여 이 객체에 액세스할 수 있습니다.

```kotlin
interface Animal {
    fun makeNoise()
}

open class Animal {
    open fun makeNoise() {
        println("Some noise")
    }
}

val animal = object: Animal(), Animal {
    override fun makeNoise() {
        println("Bark")
    }
}

println(animal.javaClass) // Prints "class com.example.Animal$1"
```

위의 코드에서 `Animal` 클래스와 `Animal` 인터페이스를 만들었습니다. 우리는 `Animal` 클래스를 확장하고 `Animal` 인터페이스를 구현하는 익명의 내부 클래스를 만들었습니다. `javaClass` 속성을 사용하여 `animal` 개체의 클래스를 인쇄했습니다. 보시다시피 `animal` 객체는 익명 내부 클래스의 인스턴스입니다.

## 정적 중첩 클래스 만들기

Kotlin에서 정적 중첩 클래스를 만들 수도 있습니다. 정적 중첩 클래스는 `static` 키워드를 사용하여 선언됩니다.

```kotlin
class OuterClass {
    class NestedClass
}
```

정적 중첩 클래스는 외부 클래스의 멤버에 액세스할 수 있습니다. 또한 '추상' 또는 '봉인'으로 선언할 수도 있습니다.

```kotlin
class OuterClass {
    class NestedClass {
        fun someMethod() {
            println("Some method")
        }
    }
}

val nestedClass = OuterClass.NestedClass()
nestedClass.someMethod() // Prints "Some method"
```

위의 코드에서 정적 중첩 클래스와 해당 클래스의 인스턴스를 만들었습니다. `nestedClass` 개체에서 `someMethod` 메서드를 호출했습니다.

## 내부 클래스 만들기

내부 클래스는 비정적 중첩 클래스입니다. 내부 클래스는 외부 클래스의 멤버에 액세스할 수 있습니다. 또한 '추상' 또는 '봉인'으로 선언할 수도 있습니다.

```kotlin
class OuterClass {
    inner class InnerClass {
        fun someMethod() {
            println("Some method")
        }
    }
}

val outerClass = OuterClass()
val innerClass = outerClass.InnerClass()
innerClass.someMethod() // Prints "Some method"
```

위의 코드에서 내부 클래스와 해당 클래스의 인스턴스를 만들었습니다. `innerClass` 개체에서 `someMethod` 메서드를 호출했습니다.

## 결론

이번 포스트에서는 Kotlin의 익명 내부 클래스에 대해 알아보았습니다. 클래스를 확장하고, 인터페이스를 구현하고, 클래스를 확장하고 인터페이스를 구현하는 익명의 내부 클래스를 만드는 방법을 살펴보았습니다. 정적 중첩 클래스와 내부 클래스를 만드는 방법도 살펴보았습니다.