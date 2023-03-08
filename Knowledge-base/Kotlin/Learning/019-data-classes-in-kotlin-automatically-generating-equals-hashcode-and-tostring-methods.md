---
title: 019: Kotlin의 데이터 클래스: Equals, HashCode 및 ToString 메서드 자동 생성
description: 
published: true
date: 2023-02-12T01:55:23.374Z
tags: 
editor: markdown
dateCreated: 2023-02-12T01:55:21.799Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [019: Data Classes in Kotlin: Automatically Generating Equals, HashCode, and ToString Methods***English** document is available*](/en/Knowledge-base/Kotlin/Learning/019-data-classes-in-kotlin-automatically-generating-equals-hashcode-and-tostring-methods)
{.links-list}


# Kotlin의 데이터 클래스: Equals, HashCode 및 ToString 메서드 자동 생성

Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어입니다. 간결하고 안전하며 상호 운용이 가능하도록 설계된 범용 언어입니다.

Kotlin을 돋보이게 만드는 기능 중 하나는 데이터 클래스 지원입니다. 데이터 클래스는 데이터를 보유하도록 설계된 클래스입니다. Kotlin에서 데이터 클래스에는 equals(), hashCode() 및 toString() 메서드를 자동으로 생성하는 기능을 포함하여 많은 내장 기능이 있습니다.

이 게시물에서는 Kotlin에서 데이터 클래스를 사용하는 방법과 equals(), hashCode() 및 toString() 메서드를 자동으로 생성하는 방법을 살펴보겠습니다.

## 데이터 클래스 만들기

데이터 클래스를 생성하기 위해 키워드 data를 사용합니다.

```kotlin
data class User(val name: String, val age: Int)
```

이렇게 하면 name과 age라는 두 가지 속성이 있는 데이터 클래스가 생성됩니다. 변경 가능한 속성으로 데이터 클래스를 만들 수도 있습니다.

```kotlin
data class User(var name: String, var age: Int)
```

데이터 클래스에는 보조 생성자가 있을 수도 있습니다.

```kotlin
data class User(val name: String, val age: Int) {
    constructor(name: String) : this(name, 0)
}
```

## Equals 및 HashCode 메서드 생성

기본적으로 Kotlin의 데이터 클래스는 equals() 및 hashCode() 메서드를 생성합니다. 이러한 메서드는 두 데이터 클래스의 데이터를 비교하고 같으면 true를 반환합니다.

다음은 equals() 메서드의 작동 방식에 대한 예입니다.

```kotlin
val user1 = User("John", 30)
val user2 = User("John", 30)

println(user1 == user2) // true
```

이 예에는 이름과 연령 속성이 동일한 두 개의 데이터 클래스가 있습니다. == 연산자를 사용하여 비교하면 equals() 메서드가 호출되어 true를 반환합니다.

속성 중 하나를 변경하면 equals() 메서드는 false를 반환합니다.

```kotlin
val user1 = User("John", 30)
val user2 = User("John", 31)

println(user1 == user2) // false
```

## toString() 메서드 생성

Kotlin의 데이터 클래스도 toString() 메서드를 생성합니다. 이 메서드는 데이터 클래스의 데이터를 문자열로 변환하는 데 사용됩니다.

다음은 toString() 메서드의 작동 방식에 대한 예입니다.

```kotlin
val user = User("John", 30)

println(user.toString()) // User(name=John, age=30)
```

보시다시피 toString() 메서드는 데이터 클래스의 데이터를 읽을 수 있는 형식으로 출력합니다.

## 결론

이 게시물에서는 Kotlin의 데이터 클래스와 equals(), hashCode() 및 toString() 메서드를 자동으로 생성하는 방법을 살펴보았습니다. 데이터 클래스는 간결하고 안전한 코드를 만드는 좋은 방법입니다.