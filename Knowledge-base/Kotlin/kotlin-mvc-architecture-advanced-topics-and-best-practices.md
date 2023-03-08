---
title: Kotlin MVC 아키텍처: 고급 주제 및 모범 사례
description: 
published: true
date: 2023-02-08T05:18:01.735Z
tags: 
editor: markdown
dateCreated: 2023-02-08T05:18:00.292Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin MVC Architecture: Advanced Topics and Best Practices***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-mvc-architecture-advanced-topics-and-best-practices)
{.links-list}


# Kotlin MVC 아키텍처: 고급 주제 및 모범 사례

이 문서에서는 Kotlin MVC 아키텍처에 대한 몇 가지 고급 주제와 모범 사례에 대해 논의합니다. 또한 이러한 개념을 설명하기 위해 몇 가지 코드 예제를 제공할 것입니다.

## 요청 처리

Kotlin MVC 아키텍처의 가장 중요한 측면 중 하나는 요청을 올바르게 처리하는 방법입니다. 이를 수행하는 두 가지 방법이 있습니다. 필터와 핸들러를 사용하는 것입니다.

### 필터

필터는 핸들러에서 요청을 처리하기 전에 요청을 사전 처리하는 데 사용됩니다. 이는 인증 및 권한 부여, 입력 유효성 검사 및 로깅과 같은 작업에 유용합니다.

필터는 애플리케이션의 ```configuration``` 파일에 등록됩니다.

```kotlin
// Register a filter for all requests
configuration.addFilter("MyFilter", "/*") {
    // ...
}

// Register a filter for specific requests
configuration.addFilter("MyFilter", "/my-path") {
    // ...
}
```

필터가 등록되면 일치하는 모든 요청에 대해 호출됩니다. 필터는 요청의 ```Parameters```, ```Headers``` 및 ```Body```에 액세스할 수 있습니다. 또한 핸들러에서 사용할 수 있는 요청에 ```Headers``` 및 ```Attributes```를 설정할 수 있습니다.

#### 필터 예

다음은 모든 요청을 기록하는 필터의 간단한 예입니다.

```kotlin
class RequestLoggingFilter : Filter {
    override fun invoke(call: Call, next: Next) {
        val request = call.request
        val path = request.path
        val method = request.method
        val query = request.queryString
        val headers = request.headers.entries.joinToString { "${it.key}: ${it.value}" }
        val body = request.body.asText()
        
        val log = "$method $path $query $headers $body"
        println(log)
        
        // Invoke the next filter or handler in the chain
        next(call)
    }
}
```

이 필터는 요청 방법, 경로, 쿼리 문자열, 헤더 및 본문을 콘솔에 기록합니다.

### 핸들러

핸들러는 요청을 처리하고 응답을 생성하는 데 사용됩니다. 요청의 ```Parameters```, ```Headers```, ```Attributes``` 및 ```Body```에 액세스할 수 있습니다.

핸들러는 애플리케이션의 ```configuration``` 파일에 등록됩니다.

```kotlin
// Register a handler for all requests
configuration.addHandler("MyHandler", "/*") {
    // ...
}

// Register a handler for specific requests
configuration.addHandler("MyHandler", "/my-path") {
    // ...
}
```

핸들러가 등록되면 일치하는 모든 요청에 대해 호출됩니다. 핸들러는 필터 및 기타 핸들러에서 사용할 수 있는 응답에 ```Headers``` 및 ```Attributes```를 설정할 수 있습니다.

#### 핸들러 예제

다음은 "Hello, World!"를 반환하는 처리기의 간단한 예입니다. 응답:

```kotlin
class HelloWorldHandler : Handler {
    override fun invoke(call: Call) {
        val response = call.response
        response.status = Status.OK
        response.body = "Hello, World!"
    }
}
```

이 핸들러는 응답 상태를 ```200 OK```로 설정하고 본문을 "Hello, World!"로 설정합니다.

## 라우팅

라우팅은 요청을 처리기에 매핑하는 데 사용됩니다. 이를 수행하는 방법에는 구성과 코드를 통한 두 가지 방법이 있습니다.

### 구성

애플리케이션의 ```configuration``` 파일에서 라우팅을 구성할 수 있습니다.

```kotlin
configuration.addRoute("MyRoute", "/my-path") {
    // ...
}
```

경로가 등록되면 일치하는 모든 요청에 대해 호출됩니다. 경로는 요청의 ```Parameters```, ```Headers``` 및 ```Body```에 액세스할 수 있습니다. 또한 필터 및 핸들러에서 사용할 수 있는 요청에 ```Headers``` 및 ```Attributes```를 설정할 수 있습니다.

#### 경로 예

다음은 요청을 "Hello, World!"에 매핑하는 경로의 간단한 예입니다. 매니저:

```kotlin
class HelloWorldRoute : Route {
    override fun invoke(call: Call, next: Next) {
        val request = call.request
        val path = request.path
        
        if (path == "/hello-world") {
            val handler = HelloWorldHandler()
            handler(call)
        } else {
            // Invoke the next route in the chain
            next(call)
        }
    }
}
```

이 경로는 요청 경로를 확인합니다. "/hello-world"이면 "Hello, World!" 매니저. 그렇지 않으면 체인의 다음 경로를 호출합니다.

### 코드

라우팅은 코드에서도 수행할 수 있습니다.

```kotlin
val route = Route {
    // ...
}

configuration.addRoute(route)
```

경로가 등록되면 일치하는 모든 요청에 대해 호출됩니다. 경로는 요청의 ```Parameters```, ```Headers``` 및 ```Body```에 액세스할 수 있습니다. 또한 필터 및 핸들러에서 사용할 수 있는 요청에 ```Headers``` 및 ```Attributes```를 설정할 수 있습니다.

#### 경로 예시

다음은 요청을 "Hello, World!"에 매핑하는 경로의 간단한 예입니다. 매니저:

```kotlin
val route = Route {
    val request = it.request
    val path = request.path
    
    if (path == "/hello-world") {
        val handler = HelloWorldHandler()
        handler(it)
    } else {
        // Invoke the next route in the chain
        it.next()
    }
}
```

이 경로는 요청 경로를 확인합니다. "/hello-world"이면 "Hello, World!" 매니저. 그렇지 않으면 체인의 다음 경로를 호출합니다.

## 모범 사례

다음은 Kotlin MVC 아키텍처로 작업할 때 염두에 두어야 할 몇 가지 일반적인 모범 사례입니다.

- 인증, 권한 부여, 입력 유효성 검사 및 로깅과 같은 전처리 작업에 필터를 사용합니다.
- 핸들러를 사용하여 요청을 처리하고 응답을 생성합니다.
- 요청을 핸들러에 매핑하기 위해 경로를 사용합니다.
- 코드를 깨끗하고 간결하게 유지하십시오.
- 단일 책임 원칙을 따릅니다.
- DRY 원칙을 따릅니다.
- KISS 원칙을 따릅니다.

## 참조

- [코틀린 MVC 아키텍처](https://kotlinlang.org/docs/reference/mvc.html)
- [코틀린 MVC 프레임워크](https://kotlinlang.org/docs/reference/mvc-framework.html)
- [코틀린 MVC 튜토리얼](https://kotlinlang.org/docs/tutorials/kotlin-mvc.html)