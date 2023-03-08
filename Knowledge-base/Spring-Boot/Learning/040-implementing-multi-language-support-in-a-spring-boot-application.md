---
title: 040: Spring Boot 애플리케이션에서 다국어 지원 구현
description: 
published: true
date: 2023-02-02T04:04:27.159Z
tags: 
editor: markdown
dateCreated: 2023-02-02T04:04:25.498Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [040: Implementing multi-language support in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/040-implementing-multi-language-support-in-a-spring-boot-application)
{.links-list}



# Spring Boot 애플리케이션에서 다국어 지원 구현

국제화(i18n)는 현지화(l10n)로 알려진 프로세스인 특정 현지 언어 및 문화에 적용할 수 있는 제품 또는 서비스를 개발하는 프로세스입니다.

Spring Boot를 사용하면 `spring-boot-starter-data-jpa` 및 `spring-boot-starter-thymeleaf` 스타터의 도움으로 애플리케이션에 i18n 지원을 쉽게 추가할 수 있습니다.

이 게시물에서는 Spring Boot 애플리케이션에 i18n 지원을 추가하는 방법을 살펴보겠습니다. 다음 주제를 다룹니다.

* i18n용 스프링 부트 구성
* 언어별 메시지 파일 생성
* 보기에 현지화된 메시지 표시
* 애플리케이션에서 언어 전환

## i18n용 스프링 부트 구성

먼저 `pom.xml`에 `spring-boot-starter-data-jpa` 및 `spring-boot-starter-thymeleaf` 스타터를 추가해야 합니다.

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-thymeleaf</artifactId>
    </dependency>
</dependencies>
```

다음으로 `application.properties` 파일에서 `MessageSource` 빈을 구성해야 합니다.

```properties
spring.messages.basename=messages
```

`MessageSource` 빈은 메시지 파일에서 메시지를 해석하는 역할을 합니다. 기본적으로 Spring Boot는 `src/main/resources` 디렉토리에서 메시지 파일을 찾습니다.

## 언어별 메시지 파일 생성

다음으로 지원하려는 각 언어에 대한 메시지 파일을 만들어야 합니다. 메시지 파일의 이름은 `messages_[lang].properties`여야 합니다. 여기서 `[lang]`은 해당 언어의 [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) 코드입니다. .

예를 들어 영어와 프랑스어를 지원하려는 경우 다음 메시지 파일을 만듭니다.

* `messages_en.properties`
* `messages_fr.properties`

각 메시지 파일에는 `MessageSource` 빈에서 확인할 수 있는 각 메시지에 대한 키-값 쌍이 포함됩니다. 예를 들어 `messages_en.properties` 파일은 다음과 같습니다.

```properties
greeting=Hello, world!
```

그리고 `messages_fr.properties` 파일은 다음과 같습니다.

```properties
greeting=Bonjour, monde!
```

## 보기에 현지화된 메시지 표시

이제 메시지 파일이 설정되었으므로 보기에 지역화된 메시지 표시를 시작할 수 있습니다.

Thymeleaf에서는 `# {...}` 구문을 사용하여 메시지 파일에서 메시지를 확인할 수 있습니다. 예를 들어 `messages_en.properties` 파일에서 `인사말` 메시지를 표시하려면 다음을 수행할 수 있습니다.

```html
<p th:text="#{greeting}">Hello, world!</p>
```

`messages_fr.properties` 파일에서 `인사말` 메시지를 표시하려면 다음을 수행할 수 있습니다.

```html
<p th:text="#{greeting}">Bonjour, monde!</p>
```

## 애플리케이션에서 언어 전환

이제 보기에 지역화된 메시지를 표시할 수 있으므로 언어를 전환하는 방법이 필요합니다.

이를 수행하는 방법에는 여러 가지가 있지만 한 가지 간단한 방법은 애플리케이션의 `queryString`에 `lang` 매개변수를 추가하는 것입니다. 예를 들어 프랑스어로 전환하려는 경우 다음을 수행할 수 있습니다.

```
http://localhost:8080/?lang=fr
```

그런 다음 `lang` 매개변수를 사용하여 `LocaleResolver` 빈에서 `Locale`을 설정할 수 있습니다. 예를 들어 `application.properties` 파일에 다음을 추가할 수 있습니다.

```properties
spring.mvc.locale-resolver=org.springframework.web.servlet.i18n.SessionLocaleResolver
```

그런 다음 `LocaleResolver` 빈에 다음을 추가합니다.

```java
@Bean
public LocaleResolver localeResolver() {
    SessionLocaleResolver localeResolver = new SessionLocaleResolver();
    localeResolver.setDefaultLocale(Locale.ENGLISH);
    return localeResolver;
}
```

이제 `http://localhost:8080/?lang=fr`을 방문하면 응용 프로그램이 프랑스어로 전환되고 `messages_fr.properties` 파일의 `인사말` 메시지가 표시됩니다.

## 결론

이 게시물에서는 Spring Boot 애플리케이션에 i18n 지원을 추가하는 방법을 다루었습니다. i18n용 Spring Boot를 구성하는 방법, 언어별 메시지 파일을 만드는 방법, 보기에 지역화된 메시지를 표시하는 방법 및 애플리케이션에서 언어를 전환하는 방법을 살펴보았습니다.