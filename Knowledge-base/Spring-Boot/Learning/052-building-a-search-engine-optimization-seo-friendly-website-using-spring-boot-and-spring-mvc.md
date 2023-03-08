---
title: 052: Spring Boot 및 Spring MVC를 사용하여 검색 엔진 최적화(SEO) 친화적인 웹 사이트 구축
description: 
published: true
date: 2023-02-02T18:57:28.123Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:57:26.475Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [052: Building a search engine optimization (SEO) friendly website using Spring Boot and Spring MVC***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/052-building-a-search-engine-optimization-seo-friendly-website-using-spring-boot-and-spring-mvc)
{.links-list}


## 소개

검색 엔진 최적화(SEO)는 검색 엔진에서 웹 사이트의 순위를 높이는 방법입니다. 순위가 높을수록 사람들이 웹사이트를 찾을 확률이 높아집니다.

콘텐츠의 품질, 웹사이트의 구조 및 웹사이트 코딩 방식을 포함하여 웹사이트 순위에 기여하는 많은 요소가 있습니다.

이번 포스팅에서는 검색엔진에 친화적인 Spring Boot와 Spring MVC를 이용하여 웹사이트를 코딩하는 방법에 대해 집중적으로 다루도록 하겠습니다.

## 스프링부트란?

Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있는 프레임워크입니다.

Spring Boot에는 다음을 포함하여 웹 애플리케이션을 쉽게 만들고 실행할 수 있는 여러 기능이 포함되어 있습니다.

- 임베디드 Tomcat 또는 Jetty 서버
- Thymeleaf, FreeMarker 및 기타 템플릿 엔진 지원
- 자동 구성
- 프로젝트 문서 자동 생성

## 스프링 MVC란?

Spring MVC는 웹 애플리케이션을 구축하기 위한 프레임워크입니다. Spring 프레임워크 위에 구축되었으며 웹 애플리케이션 개발에 대한 통합 접근 방식을 제공합니다.

Spring MVC에는 다음을 포함하여 웹 애플리케이션을 쉽게 개발할 수 있도록 하는 여러 기능이 포함되어 있습니다.

- 요청 및 응답 처리를 위한 단순하고 일관된 모델
- 유연한 뷰 해상도 메커니즘
- 다중 뷰 기술 지원
- 플러그형 현지화 메커니즘

## 스프링 부트 웹 애플리케이션 만들기

Spring Initializr를 사용하여 Spring Boot 웹 애플리케이션을 생성합니다.

Spring Initializr 웹 사이트(https://start.spring.io/)로 이동하여 양식을 작성하여 새 프로젝트를 생성합니다.

![스프링 이니셜라이저](https://i.imgur.com/hm3Y6uq.png)

다음 옵션을 선택합니다.

- 프로젝트: Gradle 프로젝트
- 언어: 자바
- 스프링 부트 버전: 2.1.4

"프로젝트 생성"을 클릭하여 프로젝트를 다운로드합니다.

## 프로젝트를 Eclipse로 가져오기

프로젝트를 Gradle 프로젝트로 Eclipse에 가져옵니다.

## 컨트롤러 만들기

컨트롤러는 Spring MVC 애플리케이션의 핵심입니다. 그들은 요청과 응답을 처리할 책임이 있습니다.

이 예제에서는 "/" URL에 대한 요청을 처리하는 컨트롤러를 생성합니다.

com.example.demo 패키지에 새 클래스를 만들고 이름을 "HelloController.java"로 지정합니다.

클래스에 다음 코드를 추가합니다.

```java
package com.example.demo;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class HelloController {

    @RequestMapping("/")
    @ResponseBody
    public String index() {
        return "Hello, world!";
    }

}
```

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Hello, world!</title>
    </head>
    <body>
        <p>Hello, world!</p>
    </body>
</html>
```@RequestMapping``` 주석은 "/" URL에 대한 요청을 index() 메서드에 매핑합니다.

```properties
spring.thymeleaf.prefix=classpath:/templates/
spring.thymeleaf.suffix=.html
spring.thymeleaf.mode=HTML5
spring.thymeleaf.encoding=UTF-8
spring.thymeleaf.content-type=text/html
spring.thymeleaf.cache=false
```html
<!DOCTYPE html>
<html>
    <헤드>
        <title>안녕하세요!</title>
    </헤드>
    <몸>
        <p>안녕하세요!</p>
    </body>
</html>
```
./gradlew bootRun
```속성
spring.thymeleaf.prefix=클래스 경로:/템플릿/
spring.thymeleaf.suffix=.html
spring.thymeleaf.mode=HTML5
spring.thymeleaf.encoding=UTF-8
spring.thymeleaf.content-type=텍스트/html
spring.thymeleaf.cache=거짓
```
curl http://localhost:8080/
```
./gradlew bootRun
```

Eclipse에서 애플리케이션을 실행하려면 프로젝트를 마우스 오른쪽 버튼으로 클릭하고 "Run As -> Spring Boot App"을 선택합니다.

## 애플리케이션 테스트

"/" URL로 요청을 전송하여 애플리케이션을 테스트할 수 있습니다.

명령줄에서 애플리케이션을 테스트하려면 curl 명령을 사용할 수 있습니다.

```
컬 http://localhost:8080/
```

Eclipse에서 애플리케이션을 테스트하기 위해 내장 브라우저를 사용할 수 있습니다.

HelloController.java 파일을 마우스 오른쪽 버튼으로 클릭하고 "Run As -> Spring Boot App"을 선택합니다.

애플리케이션이 시작되고 "/" URL이 브라우저에서 열립니다.

## 결론

이번 포스트에서는 Spring Boot와 Spring MVC를 사용하여 검색 엔진 최적화(SEO) 친화적인 웹 사이트를 만드는 방법을 살펴보았습니다.

요청 및 응답을 처리하는 컨트롤러를 만드는 방법과 템플릿 엔진에서 처리하는 보기를 만드는 방법을 살펴보았습니다.

속성 파일을 사용하여 애플리케이션을 구성하는 방법도 살펴보았습니다.