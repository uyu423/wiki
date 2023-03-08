---
title: 062: Spring Boot로 REST API 구축
description: 
published: true
date: 2023-02-03T02:57:30.042Z
tags: 
editor: markdown
dateCreated: 2023-02-03T02:57:28.427Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [062: Building a REST API with Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/062-building-a-rest-api-with-spring-boot)
{.links-list}


# 062: Spring Boot로 REST API 구축하기

이번 포스트에서는 Spring Boot로 REST API를 빌드하는 방법에 대해 알아보겠습니다.

새로운 Spring Boot 프로젝트를 생성하는 것으로 시작하겠습니다. 그런 다음 REST API를 만들 수 있도록 프로젝트에 종속성을 추가합니다.

다음으로 API에 대한 HTTP 요청을 처리할 컨트롤러를 만듭니다. 마지막으로 Postman을 사용하여 API를 테스트합니다.

## 스프링 부트 프로젝트 생성

먼저 새로운 Spring Boot 프로젝트를 생성해야 합니다. Spring Initializr를 사용하여 이를 수행할 수 있습니다.

다음 정보를 지정해야 합니다.

- 그룹: com.example
- 아티팩트: 데모
- 이름: DemoApplication
- 설명 : 062 데모 프로젝트
- 패키지 이름: com.example.demo
- 포장: 항아리
- 자바 버전: 8
- 언어: Kotlin
- 부트 버전: 2.1.5

![spring-initializr](https://i.imgur.com/eU0mhVv.png)

양식을 작성하면 "프로젝트 생성"을 클릭할 수 있습니다. 그러면 프로젝트가 포함된 ZIP 파일이 다운로드됩니다.

## 종속성 추가

다음으로 프로젝트에 종속성을 추가해야 합니다. 이 종속성을 통해 REST API를 만들 수 있습니다.

build.gradle 파일에 다음을 추가하면 됩니다.

```groovy
dependencies {
    ...
    compile("org.springframework.boot:spring-boot-starter-web")
}
```

## 컨트롤러 만들기

이제 프로젝트가 설정되었으므로 API 생성을 시작할 수 있습니다.

컨트롤러를 만드는 것부터 시작하겠습니다. 이 컨트롤러는 API에 대한 HTTP 요청을 처리합니다.

com.example.demo 패키지에 DemoController.kt라는 새 Kotlin 파일을 생성하여 이를 수행할 수 있습니다.

```kotlin
package com.example.demo

import org.springframework.web.bind.annotation.GetMapping
import org.springframework.web.bind.annotation.RestController

@RestController
class DemoController {

    @GetMapping("/")
    fun index(): String {
        return "Hello, world!"
    }
}
```

이 파일에서 단일 끝점이 있는 컨트롤러를 만들었습니다. 이 끝점은 "Hello, world!"라는 문자열을 반환합니다. 액세스할 때.

## API 테스트

이제 API를 만들었으므로 예상대로 작동하는지 테스트할 수 있습니다.

Postman을 사용하여 이 작업을 수행할 수 있습니다. Postman은 API에 HTTP 요청을 보낼 수 있는 도구입니다.

먼저 애플리케이션을 시작해야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
./gradlew bootRun
```

애플리케이션이 시작되면 "/" 끝점에 HTTP GET 요청을 보낼 수 있습니다. "Hello, world!"라는 문자열이 표시되어야 합니다. 응답 본문에서.

![우체부](https://i.imgur.com/zgWVLCg.png)

## 결론

이번 포스트에서는 Spring Boot로 REST API를 빌드하는 방법에 대해 알아보았습니다. 새 프로젝트를 만들고, 종속성을 추가하고, 컨트롤러를 만들고, API를 테스트했습니다.