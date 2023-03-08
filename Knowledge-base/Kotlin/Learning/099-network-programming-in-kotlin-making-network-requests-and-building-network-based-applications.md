---
title: 099: Kotlin의 네트워크 프로그래밍: 네트워크 요청 및 네트워크 기반 애플리케이션 구축
description: 
published: true
date: 2023-02-16T09:17:45.425Z
tags: 
editor: markdown
dateCreated: 2023-02-16T09:17:43.380Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [099: Network Programming in Kotlin: Making Network Requests and Building Network-based Applications***English** document is available*](/en/Knowledge-base/Kotlin/Learning/099-network-programming-in-kotlin-making-network-requests-and-building-network-based-applications)
{.links-list}


# 099: Kotlin의 네트워크 프로그래밍: 네트워크 요청 및 네트워크 기반 애플리케이션 구축

Kotlin은 네트워크 기반 애플리케이션을 비롯한 다양한 애플리케이션을 구축하는 데 사용할 수 있는 강력한 프로그래밍 언어입니다. 이 게시물에서는 Kotlin을 사용하여 네트워크 요청을 수행하고 네트워크 기반 애플리케이션을 빌드하는 방법을 살펴보겠습니다.

## 네트워크 요청하기

네트워크 기반 애플리케이션으로 작업할 때 가장 일반적인 작업 중 하나는 네트워크 요청을 만드는 것입니다. Kotlin에서는 내장된 [`HttpURLConnection`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-http-url-connection/) 클래스를 사용하여 네트워크 요청을 쉽게 할 수 있습니다.

네트워크 요청을 하려면 먼저 `HttpURLConnection` 인스턴스를 생성해야 합니다. 요청하려는 리소스의 URL을 전달하여 이를 수행할 수 있습니다.

```kotlin
val url = "https://www.example.com"
val connection = HttpURLConnection(url)
```

`HttpURLConnection` 인스턴스가 있으면 [`setRequestMethod`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-http-url-connection/set-request- method.html) 메서드를 사용하여 요청 방법을 설정합니다. 요청 방법은 리소스에 대해 수행할 작업 유형을 결정합니다. 가장 일반적인 요청 방법은 `GET`, `POST`, `PUT` 및 `DELETE`입니다.

```kotlin
connection.setRequestMethod("GET")
```

[`setRequestProperty`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-http-url-connection/set-request-property.html) 메서드를 사용하여 요청을 설정할 수도 있습니다. 헤더. 요청 헤더는 요청 중인 콘텐츠 유형과 같은 요청에 대한 추가 정보를 제공하는 데 사용됩니다.

```kotlin
connection.setRequestProperty("Content-Type", "application/json")
```

`HttpURLConnection` 인스턴스를 구성하고 나면 [`getInputStream`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-http-url-connection/get-input -stream.html) 메서드를 사용하여 연결에 대한 입력 스트림을 가져옵니다. 입력 스트림을 사용하여 서버에서 응답을 읽을 수 있습니다.

```kotlin
val inputStream = connection.getInputStream()
```

## 네트워크 기반 애플리케이션 구축

네트워크 요청 외에도 Kotlin을 사용하여 네트워크 기반 애플리케이션을 구축할 수도 있습니다. Kotlin은 소켓 기반 애플리케이션을 만드는 데 사용할 수 있는 [`Socket`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-socket/) 클래스를 제공합니다.

소켓 기반 애플리케이션을 만들려면 먼저 `Socket` 인스턴스를 만들어야 합니다. 연결하려는 서버의 호스트 이름과 포트 번호를 전달하여 이를 수행할 수 있습니다.

```kotlin
val socket = Socket("www.example.com", 80)
```

`Socket` 인스턴스가 있으면 [`getInputStream`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-socket/get-input-stream.html)을 사용할 수 있습니다. 및 [`getOutputStream`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-socket/get-output-stream.html) 메서드를 사용하여 소켓의 입력 및 출력 스트림을 가져옵니다. 이러한 스트림은 소켓 연결을 통해 데이터를 보내고 받는 데 사용할 수 있습니다.

```kotlin
val inputStream = socket.getInputStream()
val outputStream = socket.getOutputStream()
```

입력 및 출력 스트림이 있으면 [`write`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-output-stream/write.html) 및 [ `read`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-input-stream/read.html) 메서드를 사용하여 소켓 연결을 통해 데이터를 보내고 받습니다.

```kotlin
outputStream.write("Hello, world!".toByteArray())

val response = inputStream.read()
```

마지막으로 [`close`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.io/-socket/close.html) 메서드를 사용하여 소켓 연결을 닫을 수 있습니다.

```kotlin
socket.close()
```

## 결론

이 게시물에서는 Kotlin을 사용하여 네트워크 요청을 수행하고 네트워크 기반 애플리케이션을 빌드하는 방법을 살펴보았습니다. Kotlin은 네트워크 프로그래밍을 지원하므로 다양한 애플리케이션을 구축하는 데 탁월한 선택입니다.