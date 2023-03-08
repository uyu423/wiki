---
title: 026: Kotlin의 고급 제어 흐름: with 및 apply 함수 이해
description: 
published: true
date: 2023-02-14T06:55:55.415Z
tags: 
editor: markdown
dateCreated: 2023-02-14T06:55:48.273Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [026: Advanced Control Flow in Kotlin: Understanding the with and apply Functions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/026-advanced-control-flow-in-kotlin-understanding-the-with-and-apply-functions)
{.links-list}


# 026: Kotlin의 고급 제어 흐름: with 및 apply 함수 이해

Kotlin 프로그래머는 프로그램 흐름을 제어하는 다양한 방법을 이해하는 것이 중요합니다. 이번 포스트에서는 자주 함께 사용되는 두 가지 기능인 with와 apply에 대해 살펴보겠습니다. 언제 어떻게 사용하는지 배우고 코드를 개선하는 데 어떻게 사용할 수 있는지에 대한 몇 가지 예를 볼 것입니다.

## with와 apply 함수는 무엇인가요?

with 및 apply 함수는 모두 수신기를 인수로 사용하는 함수입니다. 수신자는 함수가 호출되는 객체입니다. with 함수는 리시버를 반환하고 apply 함수는 전달된 람다의 결과를 반환합니다.

## 언제 사용하고 적용해야 하나요?

동일한 객체에 대해 여러 작업을 수행하고 싶을 때마다 with 및 apply 함수를 사용할 수 있습니다. 일반 함수 호출을 사용하는 경우 더 자세한 코드를 간결하게 작성할 수 있기 때문에 함께 사용되는 경우가 많습니다.

예를 들어 여러 속성을 가진 User라는 클래스가 있다고 가정해 보겠습니다.

```kotlin
class User(
    val name: String,
    val age: Int,
    val address: String
)
```

그리고 이 클래스의 인스턴스가 있습니다.

```kotlin
val user = User("John", 30, "123 Main Street")
```

with 함수를 사용하여 사용자 개체에 대해 여러 작업을 수행할 수 있습니다.

```kotlin
with(user) {
    // do something with the user object
}
```

또한 사용자 개체에 대해 여러 작업을 수행하기 위해 적용 기능을 사용할 수 있습니다.

```kotlin
user.apply {
    // do something with the user object
}
```

## 사용 예 및 적용

코드를 개선하기 위해 어떻게 사용하고 적용할 수 있는지에 대한 몇 가지 예를 살펴보겠습니다.

### 1. 객체 생성 및 초기화

with 및 apply의 일반적인 사용 사례 중 하나는 개체를 만들고 초기화하는 것입니다. 몇 가지 속성을 가진 Car라는 클래스가 있다고 가정해 보겠습니다.

```kotlin
class Car(
    val make: String,
    val model: String,
    val year: Int,
    val color: String
)
```

with를 사용하여 이 클래스의 새 인스턴스를 만들고 해당 속성을 초기화할 수 있습니다.

```kotlin
val car = with(Car("Toyota", "Camry", 2020, "red")) {
    // do something with the car object
}
```

또한 적용을 사용하여 이 클래스의 새 인스턴스를 만들고 해당 속성을 초기화할 수 있습니다.

```kotlin
val car = Car("Toyota", "Camry", 2020, "red").apply {
    // do something with the car object
}
```

### 2. 속성 액세스 및 수정

with 및 apply의 또 다른 일반적인 사용 사례는 개체의 속성에 액세스하고 수정하는 것입니다. 몇 가지 속성을 가진 Person이라는 클래스가 있다고 가정해 보겠습니다.

```kotlin
class Person(
    var name: String,
    var age: Int,
    var address: String
)
```

그리고 이 클래스의 인스턴스가 있습니다.

```kotlin
val person = Person("John", 30, "123 Main Street")
```

with를 사용하여 person 객체의 속성에 액세스하고 수정할 수 있습니다.

```kotlin
with(person) {
    name = "Jane"
    age = 31
    address = "456 Main Street"
}
```

또한 apply를 사용하여 person 개체의 속성에 액세스하고 수정할 수 있습니다.

```kotlin
person.apply {
    name = "Jane"
    age = 31
    address = "456 Main Street"
}
```

### 삼. 개체에서 여러 메서드 호출

with 및 apply의 또 다른 일반적인 사용 사례는 동일한 개체에서 여러 메서드를 호출하는 것입니다. 여러 메서드가 있는 Employee라는 클래스가 있다고 가정해 보겠습니다.

```kotlin
class Employee(
    val name: String,
    val age: Int,
    val address: String
) {
    fun work() {
        // do some work
    }

    fun takeBreak() {
        // take a break
    }

    fun goHome() {
        // go home
    }
}
```

그리고 이 클래스의 인스턴스가 있습니다.

```kotlin
val employee = Employee("John", 30, "123 Main Street")
```

with를 사용하여 직원 개체에서 여러 메서드를 호출할 수 있습니다.

```kotlin
with(employee) {
    work()
    takeBreak()
    goHome()
}
```

직원 개체에 대해 여러 메서드를 호출하기 위해 apply를 사용할 수도 있습니다.

```kotlin
employee.apply {
    work()
    takeBreak()
    goHome()
}
```

## 추가 정보

다음은 with 및 apply 함수에 대해 자세히 알아볼 수 있는 몇 가지 추가 리소스입니다.

- with 함수는 Kotlin 표준 라이브러리 [여기](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-with/index.html)에 선언된 고차 함수입니다.
- 적용 함수는 [여기](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-any/apply.html)에 선언된 Any 클래스의 멤버 함수입니다.
- with 및 apply 함수는 Kotlin 설명서 [여기](https://kotlinlang.org/docs/reference/lambdas.html# with-and-apply)에 설명되어 있습니다.

## 결론

이번 포스팅에서는 with와 apply 함수에 대해 알아보았습니다. 우리는 그것들을 사용하는 시기와 방법을 보았고 그것들이 우리의 코드를 개선하기 위해 어떻게 사용될 수 있는지에 대한 몇 가지 예를 보았습니다.