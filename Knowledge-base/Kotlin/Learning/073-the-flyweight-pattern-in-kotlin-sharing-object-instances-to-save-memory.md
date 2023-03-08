---
title: 073: Kotlin의 Flyweight 패턴: 객체 인스턴스를 공유하여 메모리 절약
description: 
published: true
date: 2023-02-07T06:55:43.481Z
tags: 
editor: markdown
dateCreated: 2023-02-07T06:55:41.858Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [073: The Flyweight Pattern in Kotlin: Sharing Object Instances to Save Memory***English** document is available*](/en/Knowledge-base/Kotlin/Learning/073-the-flyweight-pattern-in-kotlin-sharing-object-instances-to-save-memory)
{.links-list}


# Kotlin의 플라이웨이트 패턴: 객체 인스턴스를 공유하여 메모리 절약하기

소프트웨어를 개발할 때 중요한 고려 사항 중 하나는 메모리를 효율적으로 사용하는 방법입니다. 메모리 사용량을 최적화하는 한 가지 방법은 플라이웨이트 패턴을 사용하는 것입니다.

플라이웨이트 패턴은 개체 인스턴스를 공유하여 메모리 절약에 도움이 되는 디자인 패턴입니다. 이것은 유사한 상태를 공유하는 많은 수의 객체가 있을 때 특히 유용합니다.

이번 포스팅에서는 코틀린에서 플라이웨이트 패턴을 어떻게 사용하는지 알아보겠습니다. 플라이급 패턴이 무엇이며 어떻게 작동하는지 살펴보는 것으로 시작하겠습니다. 그런 다음 Kotlin에서 플라이웨이트 패턴을 사용하는 방법에 대한 몇 가지 예를 살펴보겠습니다.

## 플라이급 패턴이란?

플라이웨이트 패턴은 개체 인스턴스를 공유하여 메모리 절약에 도움이 되는 디자인 패턴입니다. 이것은 유사한 상태를 공유하는 많은 수의 객체가 있을 때 특히 유용합니다.

플라이급 패턴에서 개체의 상태는 두 부분으로 나뉩니다.

* **고유 상태**: 동일한 유형의 모든 객체가 공유하는 상태입니다.
* **외부 상태**: 이것은 각 개체에 고유한 상태입니다.

본질적인 상태는 flyweight 개체에 저장됩니다. 외부 상태는 플라이급 개체 외부의 클라이언트 개체에 저장됩니다.

클라이언트 개체가 flyweight 개체에 액세스해야 하는 경우 외부 상태를 인수로 전달합니다. 그런 다음 flyweight 개체는 외부 상태를 사용하여 올바른 결과를 반환합니다.

## 플라이급 패턴은 어떻게 작동하나요?

플라이웨이트 패턴은 개체 인스턴스를 공유하여 작동합니다. 이것은 유사한 상태를 공유하는 많은 수의 객체가 있을 때 특히 유용합니다.

플라이급 패턴에서 개체의 상태는 두 부분으로 나뉩니다.

* **고유 상태**: 동일한 유형의 모든 객체가 공유하는 상태입니다.
* **외부 상태**: 이것은 각 개체에 고유한 상태입니다.

본질적인 상태는 flyweight 개체에 저장됩니다. 외부 상태는 플라이급 개체 외부의 클라이언트 개체에 저장됩니다.

클라이언트 개체가 flyweight 개체에 액세스해야 하는 경우 외부 상태를 인수로 전달합니다. 그런 다음 flyweight 개체는 외부 상태를 사용하여 올바른 결과를 반환합니다.

## 플라이급 패턴의 예

플라이웨이트 패턴의 작동 방식을 살펴보았으므로 이제 Kotlin에서 플라이웨이트 패턴을 사용하는 방법에 대한 몇 가지 예를 살펴보겠습니다.

### 예제 1: 플라이웨이트 개체 만들기

이 예제에서는 사용자의 고유한 상태를 저장하는 flyweight 개체를 만듭니다.


```kotlin
// The flyweight object
class User(val name: String) {

}

// The client object
class UserClient(val user: User) {

    fun doSomething() {
        // Use the user object
    }
}

// Create a flyweight object
val user = User("John Smith")

// Create a client object
val userClient = UserClient(user)

// Use the client object
userClient.doSomething()
```

이 예제에서는 사용자의 고유한 상태를 저장하는 flyweight 개체를 만들었습니다. flyweight 개체를 사용하는 클라이언트 개체도 만들었습니다.

### 예시 2: 외부 상태로 전달

이 예제에서는 사용자의 고유한 상태를 저장하는 flyweight 개체를 만듭니다. 또한 flyweight 개체를 사용하는 클라이언트 개체를 만듭니다.

클라이언트 개체가 flyweight 개체를 사용해야 하는 경우 외부 상태를 인수로 전달합니다.


```kotlin
// The flyweight object
class User(val name: String) {

    fun doSomething(state: String) {
        // Use the user object
    }
}

// The client object
class UserClient(val user: User) {

    fun doSomething() {
        // Pass in the extrinsic state
        user.doSomething("John Smith")
    }
}

// Create a flyweight object
val user = User("John Smith")

// Create a client object
val userClient = UserClient(user)

// Use the client object
userClient.doSomething()
```

이 예제에서는 사용자의 고유한 상태를 저장하는 flyweight 개체를 만들었습니다. flyweight 개체를 사용하는 클라이언트 개체도 만들었습니다.

클라이언트 개체가 flyweight 개체를 사용해야 하는 경우 외부 상태를 인수로 전달합니다.