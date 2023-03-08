---
title: 027: Kotlin의 Destructuring Declarations: 복잡한 개체를 변수로 분해
description: 
published: true
date: 2023-02-01T05:23:38.683Z
tags: 
editor: markdown
dateCreated: 2023-02-01T05:23:36.980Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [027: Destructuring Declarations in Kotlin: Breaking Down Complex Objects into Variables***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/027-destructuring-declarations-in-kotlin-breaking-down-complex-objects-into-variables)
{.links-list}


  # 027: Kotlin의 Destructuring Declarations: 복잡한 객체를 변수로 분해

복잡한 개체는 소프트웨어 개발에서 작업하기 어려울 수 있습니다. 여러 부분으로 구성될 수 있으므로 이해하고 사용하기 어렵습니다. Kotlin의 구조 분해 선언을 사용하면 복잡한 객체를 더 작고 관리하기 쉬운 조각으로 나눌 수 있으므로 복잡한 객체 작업이 더 쉬워집니다.

이 기사에서는 구조 분해 선언이 무엇이고 Kotlin에서 어떻게 작동하는지 살펴보겠습니다. 또한 복잡한 개체 작업을 단순화하는 데 어떻게 사용할 수 있는지 알아봅니다.

## Destructuring Declaration이 무엇인가요?

구조 분해 선언은 개체를 변수 집합으로 분해할 수 있는 Kotlin 언어 기능입니다. 이는 개체에서 사용할 수 있는 `component1()` ~ `componentN()` 함수를 사용하여 수행됩니다. 이러한 함수는 개체의 개별 부분을 반환하며, 이를 별도의 변수에 할당할 수 있습니다.

예를 들어 다음 `Person` 클래스를 고려하십시오.

```kotlin
class Person(val name: String, val age: Int)
```

이 클래스의 인스턴스를 생성하고 구조 분해 선언을 사용하여 두 변수로 분해할 수 있습니다.

```kotlin
val person = Person("John", 30)

val (name, age) = person

println("$name is $age years old")
```

그러면 다음이 인쇄됩니다.

```
John is 30 years old
```

보시다시피 `component1()` 및 `component2()` 함수를 사용하여 `person` 객체의 `name` 및 `age` 속성을 가져와서 별도의 변수에 할당할 수 있었습니다. 그런 다음 해당 변수를 독립적으로 사용할 수 있습니다.

## 데이터 클래스와 함께 Destructuring 선언 사용

데이터 클래스는 데이터를 보관하도록 설계된 Kotlin의 특수 유형 클래스입니다. 일반적으로 데이터베이스 또는 기타 스토리지 시스템의 데이터를 나타내는 데 사용됩니다.

데이터 클래스에는 몇 가지 특수 기능이 있으며 그 중 하나는 `componentN()` 함수를 통해 `component1()` 함수를 자동으로 생성한다는 것입니다. 따라서 구조 분해 선언과 함께 사용하기에 이상적입니다.

예를 들어 다음 데이터 클래스를 고려하십시오.

```kotlin
data class User(val id: Int, val name: String, val age: Int)
```

이 클래스의 인스턴스를 만들고 분해 선언을 사용하여 별도의 변수로 분해할 수 있습니다.

```kotlin
val user = User(1, "John", 30)

val (id, name, age) = user

println("$name (id=$id) is $age years old")
```

그러면 다음이 인쇄됩니다.

```
John (id=1) is 30 years old
```

보시다시피 `component1()`부터 `component3()` 함수를 사용하여 `user` 개체의 `id`, `name` 및 `age` 속성을 가져오고 할당할 수 있었습니다. 별도의 변수. 그런 다음 해당 변수를 독립적으로 사용할 수 있습니다.

## 지도로 선언을 파괴하기

맵은 소프트웨어 개발에서 공통적인 데이터 구조입니다. 키-값 쌍을 저장하는 데 사용되며 키는 해당 값을 찾는 데 사용됩니다.

Kotlin의 구조 분해 선언은 맵과 함께 사용되어 맵을 별도의 변수로 분해할 수 있습니다. 예를 들어 다음 맵을 고려하십시오.

```kotlin
val map = mapOf("id" to 1, "name" to "John", "age" to 30)
```

이 맵을 별도의 변수로 분해하기 위해 해체 선언을 사용할 수 있습니다.

```kotlin
val (id, name, age) = map

println("$name (id=$id) is $age years old")
```

그러면 다음이 인쇄됩니다.

```
John (id=1) is 30 years old
```

보시다시피 `component1()`부터 `component3()` 함수를 사용하여 맵에서 `id`, `name` 및 `age` 값을 가져와서 별도의 변수에 할당할 수 있었습니다. 그런 다음 해당 변수를 독립적으로 사용할 수 있습니다.

## 결론

이 기사에서는 Kotlin의 구조 분해 선언이 무엇인지, 복잡한 객체 작업을 단순화하는 데 어떻게 사용할 수 있는지 살펴보았습니다. 데이터 클래스 및 맵과 함께 사용하여 별도의 변수로 분해하는 방법을 살펴보았습니다.

Kotlin에 대해 자세히 알아보려면 [Kotlin 언어 웹사이트](https://kotlinlang.org/)를 확인하세요.