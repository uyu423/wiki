---
title: Spring Boot 애플리케이션 보안
description: 
published: true
date: 2023-02-17T18:01:26.508Z
tags: 
editor: markdown
dateCreated: 2023-01-30T01:30:49.787Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Securing Your Spring Boot Application***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/securing-your-spring-boot-application)
{.links-list}


## 소개

Java 개발자라면 Spring Framework에 익숙하지 않을 것입니다. Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있게 해주는 Spring Framework의 확장입니다.

Spring Boot 애플리케이션의 기본 구성은 일반적으로 대부분의 애플리케이션에 충분하지만 구성을 조정해야 하는 경우가 있습니다. 예를 들어 클라우드 환경에 배포할 마이크로서비스를 개발하는 경우 상태 비저장 환경에 더 적합한 세션 상태 비저장 모드를 사용하도록 애플리케이션을 구성할 수 있습니다.

이 게시물에서는 가장 일반적인 Spring Boot 구성 설정과 이를 구성하는 방법에 대해 살펴보겠습니다. 또한 Spring Boot 애플리케이션 보안을 위한 몇 가지 모범 사례를 살펴보겠습니다.

## 스프링 부트 설정

Spring Boot 애플리케이션은 일반적으로 `application.properties` 또는 `application.yml` 파일을 사용하여 구성됩니다. `application.properties` 파일은 간단한 속성에 사용되는 반면 `application.yml` 파일은 보다 복잡한 구성에 사용될 수 있습니다. `application.properties` 파일부터 시작하여 두 파일을 모두 살펴보겠습니다.

### 애플리케이션.속성

`application.properties` 파일은 `src/main/resources` 디렉토리에 있습니다. 이 파일에는 키-값 쌍 목록이 포함되어 있습니다. 여기서 키는 속성의 이름이고 값은 속성의 값입니다.

예를 들어 세션 상태 비저장 모드를 사용하도록 애플리케이션을 구성한다고 가정해 보겠습니다. `application.properties` 파일에 다음을 추가합니다.

```
spring.session.mode=stateless
```

마찬가지로 특정 데이터 소스를 사용하도록 애플리케이션을 구성하려는 경우 `application.properties` 파일에 다음을 추가할 수 있습니다.

```
spring.datasource.url=jdbc:mysql://localhost:3306/mydatabase
spring.datasource.username=myusername
spring.datasource.password=mypassword
```

### application.yml

`application.yml` 파일은 `src/main/resources` 디렉토리에 있습니다. 이 파일은 여러 데이터 소스 구성 또는 Spring Security 구성 측면 구성과 같은 보다 복잡한 구성에 사용할 수 있습니다.

예를 들어 여러 데이터 소스를 사용하도록 애플리케이션을 구성한다고 가정해 보겠습니다. `application.yml` 파일에 다음을 추가합니다.

```
spring:
  datasource:
    primary:
      url: jdbc:mysql://localhost:3306/mydatabase
      username: myusername
      password: mypassword
    secondary:
      url: jdbc:mysql://localhost:3306/myotherdatabase
      username: myotherusername
      password: myotherpassword
```

마찬가지로 특정 버전의 Hibernate JPA 공급자를 사용하도록 애플리케이션을 구성하려는 경우 `application.yml` 파일에 다음을 추가할 수 있습니다.

```
spring:
  jpa:
    hibernate:
      ddl-auto: validate
    properties:
      hibernate:
        jpa.provider: org.hibernate.jpa.HibernatePersistenceProvider
        jpa.properties.hibernate.dialect: org.hibernate.dialect.MySQL5Dialect
```

## Spring Boot 애플리케이션 보안

이제 Spring Boot 애플리케이션을 구성하는 방법을 살펴보았으므로 이를 보호하는 방법을 살펴보겠습니다.

Spring Boot는 애플리케이션을 쉽게 보호할 수 있는 여러 기능을 제공합니다. 예를 들어 Spring Boot는 프로젝트에서 `spring-boot-starter-security` 종속성을 감지하면 `SecurityProperties` 빈을 자동으로 구성합니다. 또한 Spring Boot는 애플리케이션의 보안을 쉽게 구성할 수 있는 여러 자동 구성 클래스를 제공합니다.

이 섹션에서는 가장 일반적인 Spring Boot 보안 기능과 이를 구성하는 방법을 살펴보겠습니다.

### HTTPS 사용

웹 애플리케이션의 가장 일반적인 보안 문제 중 하나는 데이터가 안전하게 전송되도록 하는 것입니다. HTTPS는 이를 달성하는 가장 일반적인 방법이며 Spring Boot를 사용하면 애플리케이션에 HTTPS를 쉽게 활성화할 수 있습니다.

HTTPS를 활성화하려면 먼저 키 저장소를 구성해야 합니다. 키 저장소는 애플리케이션의 SSL/TLS 인증서와 개인 키가 포함된 파일입니다. Java `keytool` 유틸리티를 사용하여 자체 서명된 키 저장소를 생성할 수 있습니다. 예를 들어 `mykeystore.jks` 파일 이름으로 키 저장소를 생성하려면 다음 명령을 사용할 수 있습니다.

```
keytool -genkeypair -alias myalias -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore mykeystore.jks -validity 365
```

키 저장소를 생성한 후에는 `application.properties` 파일에 다음을 추가하여 이를 사용하도록 Spring Boot를 구성할 수 있습니다.

```
server.ssl.key-store: mykeystore.jks
server.ssl.key-store-password: mypassword
server.ssl.keyAlias: myalias
```

또는 `application.yml` 파일에 다음을 추가하여 HTTPS를 사용하도록 Spring Boot를 구성할 수 있습니다.

```
server:
  ssl:
    key-store: mykeystore.jks
    key-store-password: mypassword
    keyAlias: myalias
```

### 데이터베이스 인증 공급자 사용

사용자를 인증하는 가장 일반적인 방법 중 하나는 데이터베이스 인증 공급자를 사용하는 것입니다. 데이터베이스 인증 공급자는 일반적으로 데이터베이스 테이블을 사용하여 사용자 이름 및 암호 해시 값을 저장합니다. 사용자가 로그인을 시도하면 인증 공급자는 일치하는 사용자 이름과 암호 해시가 있는지 데이터베이스에 쿼리합니다. 일치하는 항목이 있으면 사용자가 인증됩니다.

데이터베이스 인증 공급자를 구성하려면 먼저 사용자 이름 및 암호 해시 값을 저장할 데이터베이스 테이블을 생성해야 합니다. 다음 SQL을 사용하여 데이터베이스 테이블을 생성할 수 있습니다.

```
CREATE TABLE users (
    username VARCHAR(255) NOT NULL,
    password VARCHAR(255) NOT NULL,
    PRIMARY KEY (username)
);
```

데이터베이스 테이블을 생성한 후에는 `application.properties` 파일에 다음을 추가하여 이를 사용하도록 Spring Boot를 구성할 수 있습니다.

```
spring.security.user.name=myusername
spring.security.user.password=mypassword
```

또는 `application.yml` 파일에 다음을 추가하여 데이터베이스 인증 공급자를 사용하도록 Spring Boot를 구성할 수 있습니다.

```
spring:
  security:
    user:
      name: myusername
      password: mypassword
```

### 스프링 보안 설정

Spring Boot는 애플리케이션에 대한 Spring Security를 쉽게 구성할 수 있는 여러 자동 구성 클래스를 제공합니다. 예를 들어 Spring Boot는 프로젝트에서 `spring-boot-starter-security` 종속성을 감지하면 `WebSecurityConfigurerAdapter`를 자동으로 구성합니다.

`WebSecurityConfigurerAdapter`는 애플리케이션에 대한 Spring Security를 구성하는 데 사용할 수 있는 여러 메소드를 제공합니다. 예를 들어 `configure(HttpSecurity)` 메서드를 사용하여 웹 리소스 보안 방식을 구성할 수 있습니다.

또한 Spring Boot는 웹 리소스에 대한 액세스를 제한하는 데 사용할 수 있는 여러 HASmatcher를 제공합니다. 예를 들어 `hasIpAddress()` 매처를 사용하여 웹 리소스에 대한 액세스를 특정 IP 주소를 가진 클라이언트로만 제한할 수 있습니다.

Spring Boot 애플리케이션용 Spring Security 구성에 대해 자세히 알아보려면 [Spring Boot Security Reference Guide](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features- security.html).

## 결론

이 게시물에서는 Spring Boot 애플리케이션을 구성하는 방법을 살펴보았습니다. Spring Boot 애플리케이션을 보호하는 방법도 살펴보았습니다.

Spring Boot 애플리케이션의 기본 구성은 일반적으로 대부분의 애플리케이션에 충분하지만 구성을 조정해야 하는 경우가 있습니다. 예를 들어 클라우드 환경에 배포할 마이크로서비스를 개발하는 경우 상태 비저장 환경에 더 적합한 세션 상태 비저장 모드를 사용하도록 애플리케이션을 구성할 수 있습니다.

또한 Spring Boot는 애플리케이션을 쉽게 보호할 수 있는 여러 기능을 제공합니다. 예를 들어 Spring Boot는 프로젝트에서 `spring-boot-starter-security` 종속성을 감지하면 `SecurityProperties` 빈을 자동으로 구성합니다. 또한 Spring Boot는 애플리케이션의 보안을 쉽게 구성할 수 있는 여러 자동 구성 클래스를 제공합니다.