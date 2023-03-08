---
title: Kotlin 및 Spring Boot: RESTful 웹 서비스 구축
description: 
published: true
date: 2023-02-01T08:36:41.362Z
tags: 
editor: markdown
dateCreated: 2023-02-01T08:36:39.898Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Kotlin and Spring Boot: Building a RESTful Web Service***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-spring-boot-building-a-restful-web-service)
{.links-list}


  Kotlin은 JVM(Java Virtual Machine)에서 실행되는 최신 프로그래밍 언어이며 광범위한 도메인에서 애플리케이션을 구축하는 데 사용할 수 있습니다. Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있는 프레임워크입니다.

이 기사에서는 Kotlin과 Spring Boot를 사용하여 간단한 RESTful 웹 서비스를 빌드하는 방법을 살펴봅니다. Spring Initializr를 사용하여 Kotlin 프로젝트를 만드는 것으로 시작하겠습니다. 그런 다음 빌드 파일에 몇 가지 종속성을 추가합니다. 다음으로 HTTP 요청을 처리하는 간단한 컨트롤러를 작성합니다. 마지막으로 애플리케이션을 실행하고 웹 서비스를 테스트합니다.

코틀린 프로젝트 생성

Spring Initializr를 사용하여 Kotlin 프로젝트를 만드는 것으로 시작하겠습니다. Spring Initializr 웹사이트로 이동하여 양식을 작성하여 새 프로젝트를 생성합니다. Kotlin을 언어로 선택하고 Web 및 Lombok 종속 항목을 선택해야 합니다. Lombok은 상용구 코드를 줄이는 데 사용할 수 있는 라이브러리입니다.

![스프링 이니셜라이저](https://spring.io/images/spring-initializr.png)

양식을 작성했으면 프로젝트 생성을 클릭하여 프로젝트가 포함된 zip 파일을 다운로드합니다. zip 파일을 추출하고 선호하는 IDE에서 프로젝트를 엽니다.

종속성 추가

다음으로 빌드 파일에 몇 가지 종속성을 추가합니다. 먼저 Kotlin 표준 라이브러리가 필요합니다. build.gradle 파일의 종속성 섹션에 다음 종속성을 추가합니다.

```kotlin
implementation("org.jetbrains.kotlin:kotlin-stdlib-jdk8")
```

다음으로 Spring Boot Web starter를 추가합니다. 이 스타터는 Spring Boot로 웹 애플리케이션을 구축하는 데 필요한 모든 것을 제공합니다. build.gradle 파일의 종속성 섹션에 다음 종속성을 추가합니다.

```kotlin
implementation("org.springframework.boot:spring-boot-starter-web")
```

마지막으로 Lombok 라이브러리를 추가합니다. 이 라이브러리는 상용구 코드를 줄이는 데 도움이 됩니다. build.gradle 파일의 종속성 섹션에 다음 종속성을 추가합니다.

```kotlin
implementation("org.projectlombok:lombok")
```

컨트롤러 작성

다음으로 HTTP 요청을 처리하는 간단한 컨트롤러를 작성합니다. 먼저 src/main/kotlin/com/example/helloworld 디렉터리에 HelloController.kt라는 Kotlin 파일을 생성합니다.

이 파일에서 HelloController라는 컨트롤러 클래스를 정의합니다. 이 클래스에는 hello()라는 단일 메서드가 있습니다. 이 메서드는 HTTP 요청을 받고 문자열을 반환합니다. HelloController.kt 파일에 다음 코드를 추가합니다.

```kotlin
package com.example.helloworld

import org.springframework.web.bind.annotation.GetMapping
import org.springframework.web.bind.annotation.RestController

@RestController
class HelloController {

    @GetMapping("/hello")
    fun hello(): String {
        return "Hello, World!"
    }

}
```

이 코드에서는 HelloController 클래스에 @RestController 주석을 추가했습니다. 이 주석은 이 클래스가 컨트롤러임을 Spring에 알려줍니다. 또한 @GetMapping 주석을 사용하여 hello() 메서드에 주석을 추가했습니다. 이 주석은 hello() 메서드를 /hello URL에 매핑합니다.

애플리케이션 실행

이제 컨트롤러를 작성했으므로 애플리케이션을 실행할 준비가 되었습니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```kotlin
./gradlew bootRun
```

이 명령은 포트 8080에서 웹 서버를 시작합니다. 웹 브라우저에서 http://localhost:8080/hello로 이동하여 웹 서비스에 액세스할 수 있습니다. 다음 출력이 표시됩니다.

안녕, 세계!

웹 서비스 테스트

curl 명령을 사용하여 웹 서비스를 테스트할 수도 있습니다. 다음 명령을 실행하여 웹 서비스에 GET 요청을 보냅니다.

```kotlin
curl -i http://localhost:8080/hello
```

이 명령은 다음 출력을 반환해야 합니다.

안녕, 세계!

결론

이 기사에서는 Kotlin과 Spring Boot를 사용하여 간단한 RESTful 웹 서비스를 빌드하는 방법을 살펴보았습니다. Spring Initializr를 사용하여 Kotlin 프로젝트를 만드는 것으로 시작했습니다. 그런 다음 빌드 파일에 몇 가지 종속성을 추가했습니다. 다음으로 HTTP 요청을 처리하는 간단한 컨트롤러를 작성했습니다. 마지막으로 애플리케이션을 실행하고 웹 서비스를 테스트했습니다.