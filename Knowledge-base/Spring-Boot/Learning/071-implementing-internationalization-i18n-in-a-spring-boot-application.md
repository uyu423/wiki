---
title: 071: Spring Boot 애플리케이션에서 국제화(i18n) 구현
description: 
published: true
date: 2023-02-01T22:36:37.345Z
tags: 
editor: markdown
dateCreated: 2023-02-01T22:36:35.788Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [071: Implementing Internationalization (i18n) in a Spring Boot Application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/071-implementing-internationalization-i18n-in-a-spring-boot-application)
{.links-list}


# Spring Boot 애플리케이션에서 국제화(i18n) 구현

국제화(i18n)는 애플리케이션이 여러 언어를 지원하도록 만드는 과정입니다. 이는 복잡한 작업이 될 수 있지만 Spring Boot를 사용하면 훨씬 쉬워집니다. 이 게시물에서는 Spring Boot 애플리케이션에서 i18n을 구현하는 방법을 살펴보겠습니다.

## i18n이 무엇인가요?

국제화(i18n)는 애플리케이션이 여러 언어를 지원하도록 만드는 프로세스입니다. 이는 복잡한 작업이 될 수 있지만 Spring Boot를 사용하면 훨씬 쉬워집니다.

## i18n을 사용하는 이유는 무엇입니까?

응용 프로그램에 i18n 지원을 추가하려는 이유는 많습니다. 전 세계에 사용자가 있고 그들에게 현지화된 경험을 제공하고 싶을 수도 있습니다. 또는 개인 프로젝트를 구축 중이고 i18n 지원을 추가하는 방법을 배우고 싶을 수도 있습니다. 이유가 무엇이든 i18n은 가지고 있어야 할 귀중한 기술입니다.

## Spring Boot에서 i18n을 구현하는 방법

Spring Boot를 사용하면 애플리케이션에 i18n 지원을 쉽게 추가할 수 있습니다. 이 섹션에서는 이를 수행하는 방법을 살펴보겠습니다.

### 1. i18n 종속성 추가

먼저 `pom.xml` 파일에 i18n 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

### 2. i18n 속성 구성

다음으로 `application.properties` 파일에서 i18n 속성을 구성해야 합니다.

```properties
spring.mvc.locale=en
spring.messages.basename=i18n/messages
```

### 3. i18n 파일 생성

이제 i18n 파일을 만들어야 합니다. 이 파일에는 애플리케이션에 대한 번역된 메시지가 포함됩니다. `src/main/resources/i18n`에서 이러한 파일을 만들 수 있습니다.

예를 들어 영어와 프랑스어를 지원하고 싶다고 가정해 보겠습니다. 다음 파일을 생성합니다.

- `messages_en.properties`
- `messages_fr.properties`

이 파일에서 애플리케이션에 대해 번역된 메시지를 정의합니다. 예를 들어:

```properties
# messages_en.properties

greeting=Hello
```

```properties
# messages_fr.properties

greeting=Bonjour
```

### 4. 코드에서 i18n 메시지 사용

이제 i18n 파일을 구성했으므로 코드에서 번역된 메시지를 사용할 수 있습니다. 예를 들어 다음과 같은 메서드를 가진 컨트롤러가 있다고 가정해 보겠습니다.

```java
@RequestMapping("/greeting")
public String greeting(Model model) {
    model.addAttribute("message", "greeting");
    return "greeting";
}
```

이 메소드는 i18n 파일에서 `greeting` 키로 설정된 `message` 속성을 사용하여 `greeting.ftl` 템플릿을 렌더링합니다. 따라서 `spring.mvc.locale` 속성이 `en`으로 설정되면 `message` 속성은 `Hello`로 설정됩니다. `spring.mvc.locale` 속성이 `fr`로 설정되면 `message` 속성은 `Bonjour`로 설정됩니다.

## 결론

이 게시물에서는 Spring Boot 애플리케이션에 i18n 지원을 추가하는 방법을 살펴보았습니다. i18n은 복잡한 작업이 될 수 있지만 Spring Boot를 사용하면 훨씬 쉬워집니다. 이 게시물의 단계를 따르면 애플리케이션에 i18n 지원을 쉽게 추가할 수 있습니다.