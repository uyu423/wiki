---
title: 058: Kotlin의 데이터 클래스: 자동 메서드로 개체 선언 간소화
description: 
published: true
date: 2023-02-15T21:55:37.988Z
tags: 
editor: markdown
dateCreated: 2023-02-15T21:55:36.351Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [058: Data Classes in Kotlin: Simplifying Object Declaration with Automatic Methods***English** document is available*](/en/Knowledge-base/Kotlin/Learning/058-data-classes-in-kotlin-simplifying-object-declaration-with-automatic-methods)
{.links-list}


# Kotlin의 데이터 클래스: 자동 메서드로 개체 선언 간소화

Kotlin은 Java에 대한 보다 간결하고 실용적인 대안을 목표로 하는 JVM 언어입니다. 여기에는 Java 개발자가 친숙하게 느낄 수 있는 많은 기능과 더 빠르고 쉽게 개발할 수 있는 몇 가지 새로운 기능이 있습니다.

이러한 기능 중 하나는 데이터 클래스입니다. Kotlin에서 데이터 클래스는 데이터를 보관하도록 설계된 클래스입니다. 데이터 클래스에는 일반 클래스와 다른 몇 가지 특정 기능이 있습니다.

- 추상적이거나, 개방적이거나, 봉인되었거나, 내면적일 수 없습니다.
- 기본 생성자에서 선언된 속성 이외의 속성을 가질 수 없습니다.
- 최대 26개의 매개변수가 있는 하나의 기본 생성자를 가질 수 있습니다.
- 모든 기본 생성자 매개변수는 val 또는 var로 표시되어야 합니다.
- 데이터 클래스는 일반일 수 없습니다.

데이터 클래스는 여러 메서드를 자동으로 생성하므로 유용합니다. 이러한 방법에는 다음이 포함됩니다.

- ```toString()```: 개체의 문자열 표현을 반환합니다.
- ```equals()```: 이 개체와 지정된 개체가 같은지 비교합니다.
- ```hashCode()```: 개체의 해시 코드 값을 반환합니다.
- ```copy()```: 개체의 복사본을 만듭니다.

또한 데이터 클래스는 클래스의 각 속성에 대해 ```componentN()`` 함수를 생성할 수도 있습니다. 이 함수는 보다 간결한 방식으로 데이터 클래스의 속성에 액세스하는 데 사용할 수 있습니다.

데이터 클래스를 만들려면 ```data``` 키워드를 사용합니다.

```kotlin
data class User(val id: Long, val name: String, val email: String)
```

이렇게 하면 ```id```, ```name``` 및 ```email```의 세 가지 속성이 있는 데이터 클래스가 생성됩니다. 모든 속성은 ```val```로 표시되어 있으며 이는 변경할 수 없음을 의미합니다. 속성을 변경 가능하다는 의미인 ```var```로 표시할 수도 있습니다.

데이터 클래스를 만든 후에는 일반적인 구문을 사용하여 해당 클래스의 개체를 만들 수 있습니다.

```kotlin
val user = User(1, "John", "john@example.com")
```

그런 다음 생성된 ```componentN()``` 함수를 사용하여 개체의 속성에 액세스할 수 있습니다.

```kotlin
println(user.id) // 1
println(user.name) // John
println(user.email) // john@example.com
```

생성된 ```toString()```, ```equals()``` 및 ```hashCode()``` 함수를 사용할 수도 있습니다.

```kotlin
println(user.toString()) // User(id=1, name=John, email=john@example.com)

val anotherUser = User(1, "John", "john@example.com")
println(user == anotherUser) // true

val yetAnotherUser = User(2, "John", "john@example.com")
println(user == yetAnotherUser) // false

println(user.hashCode()) // 367910362
println(anotherUser.hashCode()) // 367910362
println(yetAnotherUser.hashCode()) // 367586981
```

마지막으로 ```copy()``` 함수를 사용하여 일부 또는 모든 속성이 변경된 개체의 복사본을 만들 수 있습니다.

```kotlin
val user2 = user.copy(id = 2)
println(user2.id) // 2
println(user2.name) // John
println(user2.email) // john@example.com

val user3 = user.copy(name = "Jane")
println(user3.id) // 1
println(user3.name) // Jane
println(user3.email) // john@example.com

val user4 = user.copy(id = 2, name = "Jane", email = "jane@example.com")
println(user4.id) // 2
println(user4.name) // Jane
println(user4.email) // jane@example.com
```

보시다시피 데이터 클래스는 Kotlin에서 객체를 생성하고 작업하는 데 매우 편리한 방법이 될 수 있습니다. 많은 상용구 코드를 작성하지 않아도 될 뿐만 아니라 여러 가지 유용한 방법을 무료로 제공합니다.