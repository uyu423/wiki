---
title: 004: Spring Boot 및 Spring MVC로 REST API 구축
description: 
published: true
date: 2023-02-03T07:36:48.284Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:36:46.716Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [004: Building REST APIs with Spring Boot and Spring MVC***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/004-building-rest-apis-with-spring-boot-and-spring-mvc)
{.links-list}


# 004: Spring Boot와 Spring MVC로 REST API 만들기

이번 포스트에서는 Spring Boot와 Spring MVC로 REST API를 빌드하는 방법에 대해 알아보겠습니다.

간단한 Spring Boot 애플리케이션을 만드는 것부터 시작하겠습니다. 그런 다음 컨트롤러를 추가하여 일부 REST 끝점을 노출합니다. 마지막으로 Postman을 사용하여 API를 테스트합니다.

## 스프링 부트 애플리케이션 만들기

먼저 Spring Boot 애플리케이션을 만들어야 합니다. 이를 위해 Spring Initializr를 사용할 수 있습니다.

http://start.spring.io/로 이동하여 다음 옵션을 선택합니다.

- Java 및 Spring Boot 2.0으로 Maven 프로젝트 생성
- 포장: 항아리
- 자바 버전: 8
- 그룹: com.example
- 아티팩트: 데모
- 이름: DemoApplication
- 설명: Spring Boot REST API 데모
- 패키지 이름: com.example.demo

프로젝트 생성을 클릭하여 프로젝트를 다운로드합니다.

zip 파일을 추출하고 선호하는 IDE에서 프로젝트를 엽니다.

## 컨트롤러 추가

다음으로 컨트롤러를 추가하여 일부 REST 엔드포인트를 노출합니다.

먼저 `com.example.demo.controller`라는 새 패키지를 만듭니다. 그런 다음 해당 패키지 내에 `DemoController`라는 새 클래스를 만듭니다.

컨트롤러에는 다음 엔드포인트가 있습니다.

- `GET /`: 환영 메시지
- `GET /hello`: 인사말
- `POST /greeting`: 맞춤 메시지가 포함된 인사말

컨트롤러의 코드는 다음과 같습니다.

```java
package com.example.demo.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class DemoController {

    @GetMapping("/")
    public String index() {
        return "Welcome to the Spring Boot REST API!";
    }

    @GetMapping("/hello")
    public String hello() {
        return "Hello, Spring Boot!";
    }

    @PostMapping("/greeting")
    public String greeting(@RequestParam(value="name", defaultValue="World") String name) {
        return "Hello, " + name + "!";
    }

}
```

위의 코드에서 무슨 일이 일어나고 있는지 분석해 봅시다.

먼저 `@RestController` 주석을 사용하여 이 클래스를 컨트롤러로 지정합니다.

그런 다음 `@GetMapping` 및 `@PostMapping` 주석을 사용하여 HTTP GET 및 POST 요청을 컨트롤러의 특정 메서드에 매핑합니다.

마지막으로 `@RequestParam` 주석을 사용하여 요청에서 쿼리 매개변수를 추출합니다. 이 경우에는 `name` 매개변수를 추출합니다. `name` 매개변수가 지정되지 않은 경우 기본값인 `World`를 사용합니다.

## API 테스트

이제 컨트롤러를 설정했으므로 Postman을 사용하여 API를 테스트해 보겠습니다.

먼저 애플리케이션을 시작해야 합니다. Java 애플리케이션으로 `DemoApplication` 클래스를 실행하여 이를 수행할 수 있습니다.

애플리케이션이 시작되면 Postman을 사용하여 API에 요청을 보낼 수 있습니다.

`/` 엔드포인트에 GET 요청을 전송해 보겠습니다.

![요청 받기](https://i.imgur.com/LNcuFtD.png)

보시다시피 응답으로 환영 메시지를 받습니다.

`/hello` 엔드포인트에 GET 요청을 보내봅시다:

![hello-request](https://i.imgur.com/VywYbnK.png)

보다시피 응답으로 인사를 받습니다.

마지막으로 `/greeting` 엔드포인트에 POST 요청을 보내겠습니다.

![사후 요청](https://i.imgur.com/EC4nUg4.png)

보시다시피 응답으로 맞춤 메시지가 포함된 인사말을 받습니다.

## 결론

이번 포스트에서는 Spring Boot와 Spring MVC로 REST API를 빌드하는 방법을 배웠습니다.

우리는 간단한 Spring Boot 애플리케이션을 만드는 것부터 시작했습니다. 그런 다음 컨트롤러를 추가하여 일부 REST 끝점을 노출했습니다. 마지막으로 Postman을 사용하여 API를 테스트했습니다.