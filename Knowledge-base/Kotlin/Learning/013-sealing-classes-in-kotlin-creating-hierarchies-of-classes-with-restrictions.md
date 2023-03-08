---
title: 013: Kotlin에서 클래스 봉인: 제한이 있는 클래스의 계층 구조 만들기
description: 
published: true
date: 2023-01-31T05:43:40.521Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:43:37.793Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [013: Sealing Classes in Kotlin: Creating Hierarchies of Classes with Restrictions***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/013-sealing-classes-in-kotlin-creating-hierarchies-of-classes-with-restrictions)
{.links-list}


Kotlin의 인기가 계속 높아짐에 따라 점점 더 많은 개발자가 프로젝트에서 Kotlin을 사용할 방법을 찾고 있습니다. Kotlin의 주요 기능 중 하나는 클래스를 봉인하는 기능으로 제한이 있는 클래스 계층을 생성할 수 있습니다.

이 기사에서는 봉인 클래스가 무엇이며 Kotlin 프로젝트에서 어떻게 사용할 수 있는지 살펴보겠습니다. 또한 실링 클래스가 실제로 어떻게 작동하는지 알아보기 위해 몇 가지 코드 예제를 살펴보겠습니다.

씰링 수업이란 무엇입니까?

봉인 클래스는 제한이 있는 클래스의 계층 구조를 만드는 방법입니다. 봉인된 클래스는 동일한 파일에서 선언된 클래스에 의해서만 서브클래싱될 수 있습니다. 이를 통해 클래스 계층 구조의 디자인을 보다 잘 제어할 수 있으며 보다 강력하고 안정적인 코드로 이어질 수 있습니다.

밀봉 클래스를 사용하는 이유는 무엇입니까?

Kotlin 코드에서 봉인 클래스를 사용하려는 몇 가지 이유가 있습니다.

* 봉인 클래스를 사용하여 액세스가 제한된 클래스의 계층 구조를 만들 수 있습니다. 이는 특정 클래스만 개발자가 액세스할 수 있도록 하려는 API 라이브러리를 만드는 데 유용할 수 있습니다.

* 봉인 클래스는 코드를 보다 강력하고 안정적으로 만들 수 있습니다. 클래스를 서브클래싱할 수 있는 방법을 제한하여 코드에서 예기치 않은 동작과 오류를 방지할 수 있습니다.

* 봉인 클래스는 코드를 더 간결하게 만들 수 있습니다. 클래스를 봉인하면 여러 하위 클래스에서 코드 반복을 피할 수 있습니다.

실링 클래스는 어떻게 사용하나요?

Kotlin 코드에서 봉인 클래스를 사용하려면 다음 두 가지 작업을 수행해야 합니다.

1. "sealed" 키워드를 사용하여 봉인된 클래스를 선언합니다.

```kotlin
sealed class Shape {
}
```

2. 봉인된 클래스와 동일한 파일에서 하위 클래스를 선언합니다.

```kotlin
class Circle: Shape() {
}
```

매개변수를 사용하여 봉인된 클래스를 선언할 수도 있습니다.

```kotlin
sealed class Shape(val name: String) {
}

class Circle: Shape("circle") {
}
```

다른 파일에서 봉인된 클래스의 하위 클래스를 선언하려고 하면 오류가 발생합니다.

```kotlin
// Error: Cannot subclass sealed class Shape

class Square: Shape() {
}
```

컴패니언 개체를 사용하여 이 문제를 해결할 수 있습니다.

```kotlin
class Square: Shape() {
    companion object : Shape() {
    }
}
```

봉인 클래스를 사용하는 또 다른 방법은 클래스를 추상으로 선언하는 것입니다.

```kotlin
abstract sealed class Shape {
}

class Circle: Shape() {
}

class Square: Shape() {
}
```

이를 통해 하위 클래스에서 구현되어야 하는 봉인된 클래스에서 추상 메서드를 정의할 수 있습니다.

```kotlin
abstract sealed class Shape {
    abstract fun getArea(): Double
}

class Circle(val radius: Double): Shape() {
    override fun getArea(): Double {
        return Math.PI * radius * radius
    }
}

class Square(val side: Double): Shape() {
    override fun getArea(): Double {
        return side * side
    }
}
```

봉인된 클래스를 사용하여 열거형을 만들 수도 있습니다.

```kotlin
sealed class Shape {
    class Circle(val radius: Double): Shape()
    class Square(val side: Double): Shape()
}

fun getArea(shape: Shape): Double {
    return when(shape) {
        is Shape.Circle -> Math.PI * shape.radius * shape.radius
        is Shape.Square -> shape.side * shape.side
    }
}
```

이렇게 하면 임의의 데이터로 열거형을 만들 수 있습니다.

```kotlin
enum class Shape(val name: String) {
    CIRCLE("circle"),
    SQUARE("square")
}
```

봉인된 클래스를 사용하여 봉인된 개체를 만들 수도 있습니다.

```kotlin
sealed class Shape {
    object Circle: Shape()
    object Square: Shape()
}

fun getArea(shape: Shape): Double {
    return when(shape) {
        is Shape.Circle -> Math.PI * 1.0 * 1.0
        is Shape.Square -> 1.0 * 1.0
    }
}
```

봉인된 개체는 싱글톤 유형으로, 메모리에 개체 인스턴스가 하나만 있을 수 있음을 의미합니다. 이는 캐시 또는 스레드 풀과 같은 항목을 만드는 데 유용할 수 있습니다.

봉인된 개체의 두 번째 인스턴스를 만들려고 하면 오류가 발생합니다.

```kotlin
// Error: Object 'Shape.Circle' has already been created

val circle = Shape.Circle
```

Kotlin 문서에서 봉인된 클래스에 대한 자세한 정보를 찾을 수 있습니다.

https://kotlinlang.org/docs/reference/sealed-classes.html

Kotlin 문서에서 싱글톤에 대한 자세한 정보를 찾을 수 있습니다.

https://kotlinlang.org/docs/reference/object-declarations.html#object-declarations

요약하면 봉인 클래스는 제한이 있는 클래스의 계층 구조를 만드는 방법입니다. 봉인 클래스는 특정 클래스만 개발자가 액세스할 수 있도록 하려는 API 라이브러리를 만드는 데 유용할 수 있습니다. 봉인 클래스는 또한 코드를 보다 강력하고 안정적으로 만들 수 있습니다.