---
title: Swagger를 사용한 Spring Boot RESTful 서비스
description: 
published: true
date: 2023-02-03T18:17:24.879Z
tags: 
editor: markdown
dateCreated: 2023-02-03T18:17:23.317Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot RESTful Services with Swagger***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-restful-services-with-swagger)
{.links-list}


# Swagger를 사용한 Spring Boot RESTful 서비스

마이크로서비스의 인기가 계속 증가함에 따라 서비스가 서로 통신할 수 있는 것이 중요합니다. 마이크로서비스 아키텍처에서 각 서비스는 통신을 위해 REST API를 노출하는 자체 포함 단위입니다.

Swagger는 이러한 REST API를 만들고 문서화하는 데 도움이 되는 도구입니다. 코드를 기반으로 문서를 자동으로 생성할 수 있는 여러 기능이 함께 제공되기 때문에 Spring Boot 기반 애플리케이션에 특히 유용합니다.

이 기사에서는 Spring Boot 애플리케이션에 Swagger 2를 사용하여 REST API를 문서화하는 방법을 살펴보겠습니다.

## 스웨거란?

Swagger는 REST API를 만들고 문서화하는 데 도움이 되는 도구입니다. 코드를 기반으로 문서를 자동으로 생성할 수 있는 여러 기능이 함께 제공되기 때문에 Spring Boot 기반 애플리케이션에 특히 유용합니다.

Swagger2는 RESTful API를 설명하고 문서화하는 데 사용되는 오픈 소스 프로젝트입니다. 원래 Swagger 도구(현재는 Swagger 1.0이라고 함) 뒤에 있는 팀에서 만들었습니다.

Swagger2는 소위 "OpenAPI 사양"(이전에는 "Swagger 사양"이라고 함)을 사용하여 REST API에 대한 언어 독립적인 표준 인터페이스를 정의합니다. 그런 다음 이 인터페이스를 다양한 도구에서 사용하여 문서화, 클라이언트 코드 생성 및 서버 스텁 생성과 같은 기능을 활성화할 수 있습니다.

## Spring Boot에서 Swagger를 사용하는 방법은 무엇입니까?

Springfox는 Spring 기반 애플리케이션을 위한 자동화된 JSON API 문서를 제공하는 도구입니다. Spring에서 작성된 RESTful 서비스에 대한 문서를 작성하는 데 사용됩니다.

Springfox는 스프링 구성, 클래스 구조 및 다양한 주석을 기반으로 API 시맨틱을 추론하기 위해 런타임에 애플리케이션을 한 번 검사하여 작동합니다. 그런 다음 JSON 또는 YAML 형식으로 문서를 생성하고 문서를 찾아볼 수 있는 UI를 제공합니다.

Spring Boot 애플리케이션에서 Springfox를 사용하려면 `pom.xml`에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
  <groupId>io.springfox</groupId>
  <artifactId>springfox-boot-starter</artifactId>
  <version>2.9.2</version>
</dependency>
```

또한 `@Configuration` 클래스를 생성하고 `@EnableSwagger2`로 주석을 달아 Springfox를 구성해야 합니다. 예를 들어:

```java
@Configuration
@EnableSwagger2
public class SwaggerConfig {
}
```

이렇게 하면 Swagger가 활성화되고 UI는 `http://localhost:8080/swagger-ui.html`에서 사용할 수 있습니다.

## 스웨거 UI

Swagger UI는 서비스에 의해 노출된 API를 찾아보고 테스트하는 데 사용할 수 있는 사용자 인터페이스입니다. OpenAPI 사양에서 자동으로 생성되며 코드를 작성하지 않고도 API와 상호 작용할 수 있는 방법을 제공합니다.

UI는 애플리케이션을 실행할 때 `http://localhost:8080/swagger-ui.html`에서 사용할 수 있습니다.

![Swagger UI](https://i.imgur.com/5GgUjNu.png)

## Swagger UI 사용자 정의

Swagger UI는 `index.html` 파일에 쿼리 매개변수를 추가하여 사용자 정의할 수 있습니다. 예를 들어 API의 URL을 변경하려면 `url` 쿼리 매개변수를 추가하면 됩니다.

`http://localhost:8080/swagger-ui.html?url=http://localhost:8080/v2/api-docs`

API 키를 변경하려면 `apiKey` 쿼리 매개변수를 추가하면 됩니다.

`http://localhost:8080/swagger-ui.html?apiKey=XXXXXXXXXXXXXXXXXXXXXXXX`

## OpenAPI 사양 사용자 지정

OpenAPI 사양은 `Docket` 유형의 `@Configuration` 빈을 제공하여 사용자 정의할 수 있습니다. 예를 들어 API의 경로를 변경하려면 다음을 수행할 수 있습니다.

```java
@Bean
public Docket api() {
    return new Docket(DocumentationType.SWAGGER_2)
        .select()
        .apis(RequestHandlerSelectors.any())
        .paths(PathSelectors.any())
        .build()
        .pathMapping("/");
}
```

이렇게 하면 API의 경로가 `/v2/api-docs`에서 `/api-docs`로 변경됩니다.

API의 호스트를 변경하려면 다음을 수행할 수 있습니다.

```java
@Bean
public Docket api() {
    return new Docket(DocumentationType.SWAGGER_2)
        .host("example.com")
        .select()
        .apis(RequestHandlerSelectors.any())
        .paths(PathSelectors.any())
        .build();
}
```

## 결론

이 기사에서는 Spring Boot 애플리케이션에 Swagger 2를 사용하여 REST API를 문서화하는 방법을 살펴보았습니다. 또한 Swagger UI 및 OpenAPI 사양을 사용자 지정하는 방법도 살펴보았습니다.