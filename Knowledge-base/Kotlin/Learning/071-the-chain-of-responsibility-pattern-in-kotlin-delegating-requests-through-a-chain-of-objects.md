---
title: 071: Kotlin의 책임 사슬 패턴: 개체 사슬을 통한 요청 위임
description: 
published: true
date: 2023-02-17T04:33:28.381Z
tags: 
editor: markdown
dateCreated: 2023-02-17T04:32:36.349Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [071: The Chain of Responsibility Pattern in Kotlin: Delegating Requests Through a Chain of Objects***English** document is available*](/en/Knowledge-base/Kotlin/Learning/071-the-chain-of-responsibility-pattern-in-kotlin-delegating-requests-through-a-chain-of-objects)
{.links-list}


## 소개

책임 체인 패턴은 적절한 핸들러를 찾기 위해 객체 체인을 따라 요청을 전달하는 디자인 패턴입니다. 이 패턴은 종종 데코레이터 및 명령 패턴과 함께 사용됩니다.

## 문제

요청을 처리할 수 있는 여러 개체가 있는 시스템이 있다고 가정합니다. 각 개체에는 특정 책임이 있으며 요청을 처리하거나 체인의 다음 개체로 전달할 수 있습니다.

문제는 어떤 개체가 특정 요청을 처리해야 하는지 결정하기 어려울 수 있다는 것입니다. 또한 요청하는 코드를 변경하지 않고도 체인에서 객체를 추가하거나 제거할 수 있습니다.

## 해결책

책임 체인 패턴은 요청을 처리할 수 있는 개체 체인을 생성하여 이러한 문제를 해결합니다. 개체는 서로 연결되어 있으며 요청은 처리될 때까지 한 개체에서 다음 개체로 전달됩니다.

## 구현

Kotlin에서 책임 체인 패턴을 구현하는 방법을 살펴보겠습니다.

요청에 대한 클래스를 생성하여 시작하겠습니다.

```kotlin
class Request(val data: String)
```

다음으로 처리기에 대한 클래스를 만듭니다. 각 핸들러는 체인의 다음 핸들러에 대한 참조를 갖습니다.

```kotlin
abstract class Handler(protected var next: Handler?) {

    fun handle(request: Request) {
        if (canHandle(request)) {
            doHandle(request)
        } else {
            next?.handle(request)
        }
    }

    abstract fun canHandle(request: Request): Boolean

    abstract fun doHandle(request: Request)
}
```

마지막으로 핸들러를 위한 몇 가지 구체적인 클래스를 만듭니다.

```kotlin
class FirstHandler : Handler(null) {

    override fun canHandle(request: Request): Boolean {
        return request.data.startsWith("first")
    }

    override fun doHandle(request: Request) {
        println("First handler handling request: ${request.data}")
    }
}

class SecondHandler : Handler(null) {

    override fun canHandle(request: Request): Boolean {
        return request.data.startsWith("second")
    }

    override fun doHandle(request: Request) {
        println("Second handler handling request: ${request.data}")
    }
}

class ThirdHandler : Handler(null) {

    override fun canHandle(request: Request): Boolean {
        return request.data.startsWith("third")
    }

    override fun doHandle(request: Request) {
        println("Third handler handling request: ${request.data}")
    }
}
```

이제 핸들러 체인을 만들고 체인을 통해 요청을 전달할 수 있습니다.

```kotlin
val firstHandler = FirstHandler()
val secondHandler = SecondHandler()
val thirdHandler = ThirdHandler()

firstHandler.next = secondHandler
secondHandler.next = thirdHandler

val request = Request("first request")
firstHandler.handle(request)

val request2 = Request("second request")
firstHandler.handle(request2)

val request3 = Request("third request")
firstHandler.handle(request3)
```

## 장점

책임 체인 패턴의 주요 이점은 요청을 보낸 사람과 받는 사람을 분리할 수 있다는 것입니다. 보낸 사람은 받는 사람이 누구인지 또는 요청이 어떻게 처리되는지 알 필요가 없습니다.

또 다른 이점은 요청하는 코드를 변경하지 않고도 체인에서 핸들러를 동적으로 추가하거나 제거할 수 있다는 것입니다.

## 단점

책임 체인 패턴의 한 가지 단점은 요청이 처리되는 위치를 결정하기 어려울 수 있기 때문에 디버그하기 어려울 수 있다는 것입니다.

또 다른 단점은 책임 패턴의 체인이 유지 관리하기 어려운 코드로 이어질 수 있다는 것입니다.

## 결론

이번 포스트에서는 Kotlin에서 Chain of Responsibility 패턴을 구현하는 방법을 살펴보았습니다. 이 패턴은 요청의 발신자를 수신자로부터 분리하고 체인에서 핸들러를 동적으로 추가하거나 제거하는 데 유용할 수 있습니다.