---
title: Kotlin에서 봉인된 클래스 사용
description: 
published: true
date: 2023-02-15T10:55:47.964Z
tags: 
editor: markdown
dateCreated: 2023-02-15T10:55:40.099Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Using Sealed Classes in Kotlin***English** document is available*](/en/Knowledge-base/Kotlin/using-sealed-classes-in-kotlin)
{.links-list}


# Kotlin에서 봉인된 클래스 사용하기

Kotlin의 봉인된 클래스는 클래스의 상속을 제한하는 좋은 방법입니다. 클래스를 봉인하면 클래스에서 상속할 수 있는 다른 클래스를 제어할 수 있습니다. 이것은 우발적인 상속을 방지하고 보다 안전한 형식의 코드를 생성하는 등 여러 가지 이유로 유용할 수 있습니다.

봉인된 클래스는 `sealed` 키워드를 사용하여 정의됩니다.

```kotlin
sealed class MySealedClass
```

봉인된 클래스는 하위 클래스를 가질 수 있지만 이러한 하위 클래스는 봉인된 클래스와 동일한 파일에서 선언되어야 합니다. 이는 파일 외부에서 실수로 상속되는 것을 방지하기 위한 것입니다. 예를 들어 다음은 허용되지 않습니다.

```kotlin
// MySealedClass.kt

sealed class MySealedClass

// MySubclass.kt

class MySubclass: MySealedClass // Error: MySubclass is not a member of the sealed class
```

이 문제를 해결하려면 `MySubclass`를 `MySealedClass`와 동일한 파일로 이동할 수 있습니다.

```kotlin
// MySealedClass.kt

sealed class MySealedClass

class MySubclass: MySealedClass // Ok
```

봉인된 클래스를 `inner`로 선언할 수도 있습니다.

```kotlin
class MyClass {
    sealed class MySealedClass
}
```

이 경우 하위 클래스는 `MyClass` 내부에 선언되어야 합니다.

```kotlin
class MyClass {
    sealed class MySealedClass

    class MySubclass: MySealedClass // Ok
}

class MySubclass: MyClass.MySealedClass // Error: MySubclass is not a member of MyClass
```

봉인된 클래스는 형식이 안전한 코드를 만드는 데 유용합니다. 예를 들어 다음의 봉인된 클래스 계층 구조를 고려하십시오.

```kotlin
sealed class Shape {
    class Circle(val radius: Double): Shape()
    class Rectangle(val width: Double, val height: Double): Shape()
}
```

when 식을 사용하여 형식이 안전한 방식으로 `Shape`의 다양한 하위 클래스를 처리할 수 있습니다.

```kotlin
fun getArea(shape: Shape): Double = when(shape) {
    is Shape.Circle -> Math.PI * shape.radius * shape.radius
    is Shape.Rectangle -> shape.width * shape.height
}
```

이 예에서 컴파일러는 `shape` 변수가 `Circle` 또는 `Rectangle` 유형만 될 수 있음을 결정할 수 있으므로 `else` 분기가 필요하지 않습니다.

봉인된 클래스는 변수 유형을 제한하는 데에도 유용합니다. 예를 들어 다음의 봉인된 클래스 계층 구조를 고려하십시오.

```kotlin
sealed class Pet {
    class Dog: Pet()
    class Cat: Pet()
}
```

봉인된 클래스를 사용하여 변수의 유형을 특정 하위 클래스로 제한할 수 있습니다.

```kotlin
fun getPet(name: String): Pet? = when(name) {
    "Bob" -> Pet.Dog()
    "Mary" -> Pet.Cat()
    else -> null
}

val pet: Pet = getPet("Bob") // Ok
val pet: Pet = getPet("Mary") // Ok
val pet: Pet = getPet("John") // Error: Type mismatch: inferred type is Pet? but Pet was expected
```

이 예에서 `getPet()` 함수는 `name` 매개변수가 "Bob"이면 `Dog`를 반환하고 `name` 매개변수가 "Mary"이면 `Cat`을 반환합니다. `name` 매개변수가 "Bob"도 "Mary"도 아닌 경우 `getPet()`은 `null`을 반환합니다.

`pet` 변수는 `Pet` 유형으로 선언되고 `getPet()`의 반환 값이 할당됩니다. 이는 컴파일러가 `getPet()`의 반환 값이 `Dog`, `Cat` 또는 `null`일 수 있다는 것을 알고 있기 때문에 유효합니다. `getPet()`이 `Pet`의 하위 클래스를 반환할 수 있는 경우 할당이 유효하지 않습니다.

## 참조

- [Kotlin 봉인 클래스](https://kotlinlang.org/docs/reference/sealed-classes.html)
- [Kotlin의 봉인된 클래스](https://medium.com/@BladeCoder/sealed-classes-in-kotlin-67861b4bfe7d)
- [봉인 클래스](https://antonioleiva.com/sealed-classes/)