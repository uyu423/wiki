---
title: Kotlin과 실시간 커뮤니케이션: 채팅 및 알림 시스템 구축
description: 
published: true
date: 2023-01-31T19:44:36.589Z
tags: 
editor: markdown
dateCreated: 2023-01-31T19:44:32.799Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Kotlin and Real-time Communication: Building Chat and Notification Systems***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-real-time-communication-building-chat-and-notification-systems)
{.links-list}



# Kotlin과 실시간 커뮤니케이션: 채팅 및 알림 시스템 구축

JVM 언어로서 Kotlin의 부상은 혜성처럼 일어났습니다. 2010년 JetBrains에서 프로젝트로 처음 발표한 이후 꾸준히 인기를 얻어 2017년에는 [두 번째로 사랑받는](https://www.infoworld.com/article/3226274/application- development/kotlin-trumpets-its-way-to-second-most-loved-language-in-stack-overflow-developer-survey.html) 언어를 스택 오버플로 개발자 설문 조사에 포함합니다.

Kotlin이 인기 있는 주요 이유 중 하나는 Java와의 상호 운용성입니다. 즉, Kotlin 코드는 Java를 지원하는 모든 플랫폼에서 실행할 수 있으므로 다양한 기기를 대상으로 하려는 개발자에게 매력적인 옵션이 됩니다.

Kotlin이 인기 있는 또 다른 이유는 실시간 통신(RTC) 지원입니다. RTC는 둘 이상의 당사자 간에 즉각적인 통신을 가능하게 하는 기술입니다. 채팅, 화상 회의, 게임과 같은 애플리케이션에 사용됩니다.

Kotlin의 RTC 지원은 Java WebSocket API를 기반으로 합니다. WebSocket API는 브라우저와 서버 간에 통신하는 표준 방법을 제공합니다. 실시간 애플리케이션용으로 설계되었으며 모든 주요 브라우저에서 지원됩니다.

Kotlin의 RTC 지원은 채팅 및 알림 시스템 개발에 이상적인 선택입니다. 이 기사에서는 Kotlin을 사용하여 간단한 채팅 시스템을 개발하는 방법을 보여줍니다. 또한 Kotlin의 RTC 지원을 사용하여 간단한 알림 시스템을 개발하는 방법도 보여줍니다.

## Kotlin으로 채팅 시스템 개발

Kotlin으로 채팅 시스템을 개발하는 것은 간단합니다. IntelliJ IDEA IDE를 사용하여 새 Kotlin 프로젝트를 만드는 것부터 시작하겠습니다.

프로젝트 이름을 "KotlinChat"으로 지정하고 프로젝트의 기본 설정을 사용합니다.

프로젝트가 생성되면 build.gradle 파일에 다음 종속 항목을 추가해야 합니다.

```kotlin
implementation "org.jetbrains.kotlinx:kotlinx-coroutines-core:1.3.5"
implementation "org.jetbrains.kotlinx:kotlinx-coroutines-websockets:1.3.5"
```

첫 번째 종속성은 Kotlin의 코루틴 지원에 대한 것입니다. 코루틴은 동시 프로그래밍을 위한 강력한 도구입니다. 이를 통해 비동기 및 비차단 코드를 작성할 수 있습니다.

두 번째 종속성은 Kotlin의 WebSocket 지원에 대한 것입니다. WebSocket API를 사용하여 채팅 서버와 통신합니다.

종속성을 설정했으므로 이제 채팅 시스템용 코드 작성을 시작할 수 있습니다.

Main.kt라는 새 파일을 생성하여 시작하겠습니다. 이 파일에는 채팅 시스템의 진입점이 포함됩니다.

Main.kt에서 기본 기능을 정의합니다. 이 함수는 채팅 시스템이 시작될 때 호출됩니다.

```kotlin
fun main() {

}
```

기본 기능 내에서 ChatClient 클래스의 새 인스턴스를 만듭니다. 이 클래스는 채팅 서버에 대한 연결을 관리합니다.

```kotlin
fun main() {
    val chatClient = ChatClient()
}
```

다음으로 chatClient 인스턴스에서 connect 함수를 호출합니다. 이 기능은 채팅 서버에 대한 연결을 설정합니다.

```kotlin
fun main() {
    val chatClient = ChatClient()
    chatClient.connect()
}
```

연결 함수는 채팅 서버의 URL과 콜백 함수라는 두 가지 인수를 사용합니다. 콜백 함수는 채팅 서버에 연결되면 호출됩니다.

```kotlin
fun main() {
    val chatClient = ChatClient()
    chatClient.connect("ws://localhost:8080/chat", {
        println("Connected to chat server")
    })
}
```

연결이 설정되면 메시지 송수신을 시작할 수 있습니다.

메시지를 보내기 위해 chatClient 인스턴스에서 send 함수를 호출합니다. 이 함수는 보낼 메시지와 콜백 함수라는 두 가지 인수를 사용합니다. 메시지가 전송되면 콜백 함수가 호출됩니다.

```kotlin
fun main() {
    val chatClient = ChatClient()
    chatClient.connect("ws://localhost:8080/chat", {
        println("Connected to chat server")
        chatClient.send("Hello, world!", {
            println("Message sent")
        })
    })
}
```

메시지를 수신하기 위해 chatClient 인스턴스에서 수신 기능을 호출합니다. 이 함수는 콜백 함수를 인수로 사용합니다. 콜백 함수는 메시지가 수신되면 호출됩니다.

```kotlin
fun main() {
    val chatClient = ChatClient()
    chatClient.connect("ws://localhost:8080/chat", {
        println("Connected to chat server")
        chatClient.send("Hello, world!", {
            println("Message sent")
        })
        chatClient.receive {
            println("Message received: $it")
        }
    })
}
```

수신 함수는 수신된 메시지를 인수로 사용하여 콜백 함수를 호출합니다.

이제 메시지를 보내고 받는 방법을 살펴보았으므로 ChatClient 클래스를 살펴보겠습니다.

ChatClient 클래스에는 다음 코드가 포함되어 있습니다.

```kotlin
class ChatClient {

    private val websocket = WebSocket()

    fun connect(url: String, onConnect: () -> Unit) {
        websocket.connect(url) {
            onConnect()
        }
    }

    fun send(message: String, onSend: () -> Unit) {
        websocket.send(message) {
            onSend()
        }
    }

    fun receive(onReceive: (String) -> Unit) {
        websocket.receive {
            onReceive(it)
        }
    }
}
```

ChatClient 클래스에는 연결, 전송 및 수신의 세 가지 기능이 있습니다. 연결 및 전송 기능을 사용하는 방법은 이미 살펴보았습니다.

수신 기능은 송신 기능과 유사합니다. 콜백 함수를 인수로 사용합니다. 콜백 함수는 수신된 메시지를 인수로 사용하여 호출됩니다.

ChatClient 클래스에는 websocket 속성도 있습니다. 이 속성은 WebSocket 유형입니다. WebSocket 클래스는 Java WebSocket API를 둘러싼 Kotlin 래퍼입니다.

ChatClient 클래스는 WebSocket 클래스를 사용하여 채팅 서버와 통신합니다. 연결, 보내기 및 받기 기능은 모두 WebSocket 클래스의 해당 기능을 둘러싼 래퍼입니다.

## Kotlin으로 알림 시스템 개발하기

Kotlin으로 알림 시스템을 개발하는 것은 간단합니다. IntelliJ IDEA IDE를 사용하여 새 Kotlin 프로젝트를 만드는 것부터 시작하겠습니다.

프로젝트 이름을 "KotlinNotifications"로 지정하고 프로젝트의 기본 설정을 사용합니다.

프로젝트가 생성되면 build.gradle 파일에 다음 종속 항목을 추가해야 합니다.

```kotlin
implementation "org.jetbrains.kotlinx:kotlinx-coroutines-core:1.3.5"
implementation "org.jetbrains.kotlinx:kotlinx-coroutines-websockets:1.3.5"
```

첫 번째 종속성은 Kotlin의 코루틴 지원에 대한 것입니다. 코루틴은 동시 프로그래밍을 위한 강력한 도구입니다. 이를 통해 비동기 및 비차단 코드를 작성할 수 있습니다.

두 번째 종속성은 Kotlin의 WebSocket 지원에 대한 것입니다. WebSocket API를 사용하여 알림 서버와 통신합니다.

종속성이 설정되었으므로 알림 시스템에 대한 코드 작성을 시작할 수 있습니다.

Main.kt라는 새 파일을 생성하여 시작하겠습니다. 이 파일에는 알림 시스템의 진입점이 포함됩니다.

Main.kt에서 기본 기능을 정의합니다. 이 함수는 알림 시스템이 시작될 때 호출됩니다.

```kotlin
fun main() {

}
```

기본 기능 내에서 NotificationClient 클래스의 새 인스턴스를 만듭니다. 이 클래스는 알림 서버에 대한 연결을 관리합니다.

```kotlin
fun main() {
    val notificationClient = NotificationClient()
}
```

다음으로, notificationClient 인스턴스에서 연결 함수를 호출합니다. 이 기능은 알림 서버에 대한 연결을 설정합니다.

```kotlin
fun main() {
    val notificationClient = NotificationClient()
    notificationClient.connect()
}
```

연결 함수는 알림 서버의 URL과 콜백 함수라는 두 가지 인수를 사용합니다. 콜백 함수는 알림 서버에 대한 연결이 설정되면 호출됩니다.

```kotlin
fun main() {
    val notificationClient = NotificationClient()
    notificationClient.connect("ws://localhost:8080/notifications", {
        println("Connected to notification server")
    })
}
```

연결이 설정되면 메시지 송수신을 시작할 수 있습니다.

메시지를 보내기 위해 우리는 notificationClient 인스턴스에서 send 함수를 호출할 것입니다. 이 함수는 보낼 메시지와 콜백 함수라는 두 가지 인수를 사용합니다. 메시지가 전송되면 콜백 함수가 호출됩니다.

```kotlin
fun main() {
    val notificationClient = NotificationClient()
    notificationClient.connect("ws://localhost:8080/notifications", {
        println("Connected to notification server")
        notificationClient.send("Hello, world!", {
            println("Message sent")
        })
    })
}
```

메시지를 수신하려면 notificationClient 인스턴스에서 수신 기능을 호출합니다. 이 함수는 콜백 함수를 인수로 사용합니다. 콜백 함수는 메시지가 수신되면 호출됩니다.

```kotlin
fun main() {
    val notificationClient = NotificationClient()
    notificationClient.connect("ws://localhost:8080/notifications", {
        println("Connected to notification server")
        notificationClient.send("Hello, world!", {
            println("Message sent")
        })
        notificationClient.receive {
            println("Message received: $it")
        }
    })
}
```

수신 함수는 수신된 메시지를 인수로 사용하여 콜백 함수를 호출합니다.

이제 메시지를 보내고 받는 방법을 살펴보았으므로 NotificationClient 클래스를 살펴보겠습니다.

NotificationClient 클래스에는 다음 코드가 포함되어 있습니다.

```kotlin
class NotificationClient {

    private val websocket = WebSocket()

    fun connect(url: String, onConnect: () -> Unit) {
        websocket.connect(url) {
            onConnect()
        }
    }

    fun send(message: String, onSend: () -> Unit) {
        websocket.send(message) {
            onSend()
        }
    }

    fun receive(onReceive: (String) -> Unit) {
        websocket.receive {
            onReceive(it)
        }
    }
}
```

NotificationClient 클래스에는 연결, 전송 및 수신의 세 가지 기능이 있습니다. 연결 및 전송 기능을 사용하는 방법은 이미 살펴보았습니다.

수신 기능은 송신 기능과 유사합니다. 콜백 함수를 인수로 사용합니다. 콜백 함수는 수신된 메시지를 인수로 사용하여 호출됩니다.

NotificationClient 클래스에는 websocket 속성도 있습니다. 이 속성은 WebSocket 유형입니다. WebSocket 클래스는 Java WebSocket API를 둘러싼 Kotlin 래퍼입니다.

NotificationClient 클래스는 WebSocket 클래스를 사용하여 알림 서버와 통신합니다. 연결, 보내기 및 받기 기능은 모두 WebSocket 클래스의 해당 기능을 둘러싼 래퍼입니다.