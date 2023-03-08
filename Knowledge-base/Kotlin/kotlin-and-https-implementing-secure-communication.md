---
title: Kotlin 및 HTTPS: 보안 통신 구현
description: 
published: true
date: 2023-02-03T05:23:55.043Z
tags: 
editor: markdown
dateCreated: 2023-02-03T05:23:53.393Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and HTTPS: Implementing Secure Communication***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-https-implementing-secure-communication)
{.links-list}


# Kotlin과 HTTPS: 보안 통신 구현

Kotlin은 자바 가상 머신에서 실행되고 Android 앱을 개발하는 데 사용할 수 있는 정적으로 유형이 지정된 프로그래밍 언어입니다. Kotlin의 구문은 Java와 매우 유사하지만 Java와 호환되지 않습니다. Kotlin은 인기 있는 IntelliJ IDEA Java IDE의 배후에 있는 회사인 JetBrains에서 개발한 상용 제품입니다.

Kotlin은 Java만큼 널리 사용되지는 않지만 특히 Android 개발자 사이에서 인기를 얻고 있습니다. 2019년 5월 Google은 이제 Kotlin이 Android 앱 개발에 선호되는 언어라고 발표했습니다.

Kotlin의 주요 장점 중 하나는 Java보다 더 간결한 언어라는 점입니다. Kotlin 코드는 종종 동등한 Java 코드보다 훨씬 짧습니다. 이렇게 하면 유지 관리할 코드가 줄어들고 버그가 줄어듭니다.

Kotlin은 또한 Java보다 더 표현력이 풍부한 언어입니다. null 안전 및 람다(익명 함수)와 같은 기능을 지원합니다. 이러한 기능을 통해 Kotlin 코드를 더 읽기 쉽고 이해하기 쉽게 만들 수 있습니다.

## 코틀린과 HTTPS

HTTPS(Hypertext Transfer Protocol Secure)는 웹 브라우저와 웹 서버 간의 통신을 위한 프로토콜입니다. HTTPS는 통신을 암호화 및 해독하여 제3자가 정보를 가로채거나 수정하지 못하도록 보호합니다.

Kotlin은 HTTPS를 잘 지원합니다. Kotlin에서 HTTPS 연결은 HttpsURLConnection 클래스를 사용하여 이루어집니다. 이 클래스는 Java 표준 라이브러리의 일부이므로 추가 종속성 없이 Kotlin을 사용할 때 사용할 수 있습니다.

HttpsURLConnection 클래스는 SSLContext 및 HostnameVerifier 설정과 같이 HTTPS 연결을 구성하기 위한 다양한 방법을 제공합니다. SSLContext는 사용할 TLS 프로토콜 버전 및 암호 제품군을 지정하는 데 사용할 수 있습니다. HostnameVerifier는 서버의 호스트 이름을 확인하는 데 사용할 수 있습니다.

통신이 안전한지 확인하려면 HTTPS 연결을 올바르게 구성하는 것이 중요합니다. 특히 강력한 암호화 제품군만 사용되도록 하는 것이 중요합니다.

다음 코드는 Kotlin에서 HTTPS 연결을 구성하는 방법을 보여줍니다.

```kotlin
val url = URL("https://example.com")
val connection = url.openConnection() as HttpsURLConnection
connection.sslContext = SSLContext.getInstance("TLSv1.2")
connection.setCipherSuites(arrayOf("TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256", "TLS_DHE_RSA_WITH_AES_128_GCM_SHA256"))
connection.hostnameVerifier = HostnameVerifier { hostname, _ -> hostname == "example.com" }
```

위의 코드에서 먼저 연결하려는 HTTPS URL에 대한 URL 개체를 만듭니다. 그런 다음 openConnection() 메서드를 사용하여 URL에 대한 연결을 엽니다. HTTPS 관련 메서드에 액세스할 수 있도록 연결을 HttpsURLConnection으로 캐스팅합니다.

그런 다음 TLSv1.2를 사용하도록 SSLContext를 설정하고 사용할 암호화 제품군을 지정합니다. 또한 호스트 이름 확인기를 설정하여 서버의 호스트 이름이 "example.com"인지 확인합니다.

Java 시스템 속성을 사용하여 HTTPS 연결을 구성할 수도 있습니다. 다음 Java 시스템 속성을 사용하여 Kotlin에서 HTTPS 연결을 구성할 수 있습니다.

- javax.net.ssl.trustStore
- javax.net.ssl.trustStorePassword
- javax.net.ssl.keyStore
- javax.net.ssl.keyStorePassword

## 코틀린과 HTTP/2

HTTP/2는 HTTP 프로토콜의 최신 버전입니다. HTTP/2는 이전 버전의 HTTP 프로토콜(HTTP/1.1)보다 더 효율적인 바이너리 프로토콜입니다. HTTP/2는 대기 시간을 줄이고 처리량을 개선하도록 설계되었습니다.

Kotlin은 HTTP/2를 잘 지원합니다. HttpsURLConnection 클래스는 HTTP/2 설정 지정 및 푸시 약속 활성화와 같이 HTTP/2 연결을 구성하기 위한 여러 메서드를 제공합니다.

다음 코드는 Kotlin에서 HTTP/2 연결을 구성하는 방법을 보여줍니다.

```kotlin
val url = URL("https://example.com")
val connection = url.openConnection() as HttpsURLConnection
connection.protocol = "h2"
connection.setHttp2Settings(Http2Settings.builder().pushEnabled(true).build())
```

위의 코드에서 먼저 연결하려는 HTTPS URL에 대한 URL 개체를 만듭니다. 그런 다음 openConnection() 메서드를 사용하여 URL에 대한 연결을 엽니다. HTTPS 관련 메서드에 액세스할 수 있도록 연결을 HttpsURLConnection으로 캐스팅합니다.

그런 다음 프로토콜을 "h2"로 설정하여 HTTP/2를 사용하고자 함을 나타냅니다. 푸시 약속도 활성화합니다.

Java 시스템 속성을 사용하여 HTTP/2 연결을 구성할 수도 있습니다. 다음 Java 시스템 속성을 사용하여 Kotlin에서 HTTP/2 연결을 구성할 수 있습니다.

- http.http2.활성화
- http.http2.settings.header-table-size
- http.http2.settings.initial-window-size
- http.http2.settings.max-concurrent-streams

## 결론

Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어입니다. Kotlin은 JetBrains에서 개발한 상용 제품입니다. Kotlin은 Java보다 간결한 언어이며 null 안전 및 람다와 같은 기능을 지원합니다.

Kotlin은 HTTPS를 잘 지원합니다. Kotlin에서 HTTPS 연결은 HttpsURLConnection 클래스를 사용하여 이루어집니다. HttpsURLConnection 클래스는 HTTPS 연결을 구성하기 위한 다양한 방법을 제공합니다. 통신이 안전한지 확인하려면 HTTPS 연결을 올바르게 구성하는 것이 중요합니다.

Kotlin은 또한 HTTP/2를 잘 지원합니다. HttpsURLConnection 클래스는 HTTP/2 연결을 구성하기 위한 여러 메서드를 제공합니다. HTTP/2는 이전 버전의 HTTP 프로토콜(HTTP/1.1)보다 더 효율적인 바이너리 프로토콜입니다.