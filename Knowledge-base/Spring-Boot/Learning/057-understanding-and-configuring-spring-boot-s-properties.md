---
title: 057: Spring Boot의 속성 이해 및 구성
description: 
published: true
date: 2023-02-04T20:32:18.686Z
tags: 
editor: markdown
dateCreated: 2023-02-04T20:32:17.134Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [057: Understanding and Configuring Spring Boot's Properties***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/057-understanding-and-configuring-spring-boot-s-properties)
{.links-list}


# 스프링 부트 속성

이번 포스팅에서는 Spring Boot 속성에 대해 알아보겠습니다. 우리는 그것들이 무엇인지, 그것들을 구성하는 방법, Spring Boot 애플리케이션의 동작을 사용자 정의하는 데 어떻게 사용할 수 있는지 배울 것입니다.

## 스프링 부트 속성이 무엇인가요?

Spring Boot 속성은 Spring Boot 애플리케이션을 구성하는 데 사용됩니다. 애플리케이션 이름, 서버 포트 등과 같은 다양한 Spring Boot 설정에 대한 값을 설정하는 데 사용할 수 있습니다.

속성은 속성 파일, 환경 변수를 통해 또는 프로그래밍 방식과 같은 다양한 방법으로 구성할 수 있습니다.

## Spring Boot 속성을 구성하는 방법

Spring Boot 속성은 여러 가지 방법으로 구성할 수 있습니다.

가장 일반적인 방법은 속성 파일을 사용하는 것입니다. Spring Boot는 클래스 경로에서 `application.properties`라는 파일을 찾습니다. 이 파일은 기본 Spring Boot 속성을 재정의하는 데 사용할 수 있습니다.

예를 들어 다음 `application.properties` 파일은 서버 포트를 8080으로 설정합니다.

```
server.port=8080
```

Spring Boot 속성을 구성하는 또 다른 방법은 환경 변수를 사용하는 것입니다. Spring Boot는 `spring.`으로 시작하는 환경 변수를 찾고 해당 속성을 재정의하는 데 사용합니다.

예를 들어 다음 환경 변수는 서버 포트를 8080으로 설정합니다.

```
spring.server.port=8080
```

마지막으로 Spring Boot 속성을 프로그래밍 방식으로 구성할 수도 있습니다. 이는 `@Configuration` 클래스를 만들고 `@ConfigurationProperties` 주석을 사용하여 수행할 수 있습니다.

예를 들어 다음 `@Configuration` 클래스는 `server.port` 속성을 `serverPort` 필드에 매핑합니다.

```java
@Configuration
@ConfigurationProperties(prefix="server")
public class ServerConfig {

    private int port;

    public int getPort() {
        return port;
    }

    public void setPort(int port) {
        this.port = port;
    }

}
```

## 스프링 부트 애플리케이션 커스터마이징

Spring Boot 속성을 사용하여 Spring Boot 애플리케이션의 동작을 사용자 지정할 수 있습니다.

예를 들어, `spring.main.banner-mode` 속성을 사용하여 Spring Boot 배너를 비활성화할 수 있습니다.

```
spring.main.banner-mode=off
```

`spring.jpa.show-sql` 속성을 사용하여 JPA에 대한 SQL 로깅을 활성화할 수 있습니다.

```
spring.jpa.show-sql=true
```

`spring.thymeleaf.cache` 속성을 사용하여 Thymeleaf 템플릿 캐싱을 활성화할 수 있습니다.

```
spring.thymeleaf.cache=true
```

등등.

## 결론

이번 포스팅에서는 Spring Boot 속성에 대해 알아보았습니다. 구성 방법, Spring Boot 애플리케이션의 동작을 사용자 지정하는 데 사용할 수 있는 방법 및 이에 대한 추가 정보를 찾을 수 있는 위치를 살펴보았습니다.