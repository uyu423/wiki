---
title: 072: Kotlin의 중재자 패턴: 개체 통신 캡슐화
description: 
published: true
date: 2023-02-03T15:17:29.745Z
tags: 
editor: markdown
dateCreated: 2023-02-03T15:17:28.150Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [072: The Mediator Pattern in Kotlin: Encapsulating Object Communication***English** document is available*](/en/Knowledge-base/Kotlin/Learning/072-the-mediator-pattern-in-kotlin-encapsulating-object-communication)
{.links-list}


# 072: Kotlin의 중재자 패턴: 객체 통신 캡슐화

중재자 패턴은 서로를 인식할 필요 없이 개체 간의 통신을 가능하게 하는 동작 소프트웨어 디자인 패턴입니다. 이는 제어를 중앙 집중화하거나 개체 간의 종속성을 줄여야 하는 상황에서 유용할 수 있습니다.

이번 포스트에서는 중재자 패턴을 Kotlin에서 구현하는 방법을 살펴보겠습니다. 패턴을 사용하여 개체를 분리하는 방법에 대한 간단한 예를 살펴보는 것으로 시작하겠습니다. 그런 다음 Kotlin 표준 라이브러리를 사용하는 보다 현실적인 예를 살펴보겠습니다.

## 간단한 예

대화방을 나타내는 클래스가 있다고 가정합니다.

```kotlin
class ChatRoom {
    fun showMessage(user: User, message: String) {
        println("${user.name}: $message")
    }
}
```

그리고 사용자를 나타내는 클래스:

```kotlin
class User(val name: String) {
    fun sendMessage(message: String) {
        ChatRoom.showMessage(this, message)
    }
}
```

이 간단한 예에서 `ChatRoom` 클래스는 `User` 개체 간의 중재자 역할을 합니다. `User` 개체는 서로를 인식하지 못하고 `ChatRoom` 개체에 대해서만 알고 있습니다.

## 좀 더 현실적인 예

보다 현실적인 예에서는 `ChatRoom` 클래스에서 `User` 클래스를 분리할 수 있습니다. 중재자 패턴을 사용하여 이를 수행할 수 있습니다.

먼저 `ChatRoom` 인터페이스를 만듭니다.

```kotlin
interface ChatRoom {
    fun showMessage(user: User, message: String)
}
```

그런 다음 `User` 인터페이스를 만듭니다.

```kotlin
interface User {
    fun sendMessage(message: String)
}
```

이제 `ChatRoom` 구현을 만들 수 있습니다.

```kotlin
class DefaultChatRoom : ChatRoom {
    override fun showMessage(user: User, message: String) {
        println("${user.name}: $message")
    }
}
```

그리고 `User` 구현:

```kotlin
class DefaultUser(override val name: String) : User {
    override fun sendMessage(message: String) {
        DefaultChatRoom.showMessage(this, message)
    }
}
```

이 예에서 `DefaultChatRoom` 및 `DefaultUser` 클래스는 서로 분리됩니다. 그들은 구현하는 인터페이스를 통해서만 서로에 대해 알고 있습니다.

## 결론

중재자 패턴은 개체를 서로 분리하는 데 유용한 패턴입니다. 개체 간의 제어를 중앙 집중화하거나 종속성을 줄이는 데 사용할 수 있습니다. Kotlin에서는 인터페이스를 사용하여 패턴을 구현할 수 있습니다.