---
title: Spring Boot Actuator로 모니터링
description: 
published: true
date: 2023-02-07T01:32:46.891Z
tags: 
editor: markdown
dateCreated: 2023-02-07T01:32:45.194Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Monitoring with Spring Boot Actuator***English** document is available*](/en/Knowledge-base/Spring-Boot/monitoring-with-spring-boot-actuator)
{.links-list}



# Spring Boot Actuator로 모니터링

Spring Boot Actuator는 애플리케이션을 모니터링하고 관리하는 데 도움이 되는 프로덕션 준비 기능을 제공하는 Spring Boot 프레임워크의 하위 프로젝트입니다. 또한 애플리케이션에 대한 정보를 감사하고 건강하게 만드는 데 도움이 됩니다. Spring Boot Actuator는 기본적으로 활성화되어 있지 않습니다. 활성화하려면 `@EnableAutoConfiguration` 또는 `@SpringBootApplication` 주석을 사용해야 합니다.

## 스프링 부트 액추에이터 활성화

Spring Boot 애플리케이션에서 Spring Boot Actuator를 활성화하려면 `pom.xml` 파일에 `spring-boot-starter-actuator` 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

`application.properties` 파일에 다음 속성을 추가하여 애플리케이션에서 Spring Boot Actuator를 활성화할 수도 있습니다.

```properties
management.endpoints.web.exposure.include=*
management.endpoint.health.show-details=always
```

## Spring Boot Actuator로 모니터링

Spring Boot Actuator는 애플리케이션을 모니터링하고 관리하는 데 사용할 수 있는 프로덕션 준비 엔드포인트를 제공합니다. 다음 표에는 가장 중요한 엔드포인트가 나열되어 있습니다.

| 끝점 | 설명 |
| --- | --- |
| `/건강` | 애플리케이션 상태 정보를 표시합니다(기본값은 'UP'). |
| `/정보` | 임의의 응용 프로그램 정보를 표시합니다. |
| `/측정항목` | 애플리케이션 메트릭 정보를 표시합니다. |
| `/추적` | 애플리케이션 추적 정보를 표시합니다. |
| `/덤프` | 스레드 덤프를 수행합니다. |
| `/졸로키아` | HTTP를 통해 JMX 빈을 노출합니다(`jolokia-core` 필요). |
| `/로그파일` | 로그 파일의 내용을 반환합니다(로깅이 구성된 경우). |
| `/새로고침` | 애플리케이션 및 구성 캐시를 새로 고칩니다. |
| `/이동경로` | 적용된 모든 Flyway 데이터베이스 마이그레이션을 표시합니다. |
| `/리퀴베이스` | 적용된 모든 Liquibase 데이터베이스 마이그레이션을 표시합니다. |

`/health` 및 `/info` 엔드포인트는 기본적으로 보호됩니다. 공개적으로 액세스할 수 있도록 하려면 `application.properties` 파일에 다음 속성을 추가해야 합니다.

```properties
management.security.enabled=false
```

## 스프링 부트 액추에이터 커스터마이징

Spring Boot Actuator는 동작을 사용자 정의할 수 있는 다양한 방법을 제공합니다.

### 관리 서버 포트 변경

기본적으로 Spring Boot Actuator는 관리 서버에 포트 '8080'을 사용합니다. `application.properties` 파일에 다음 속성을 추가하여 이를 변경할 수 있습니다.

```properties
management.server.port=<port>
```

### 관리 서버 경로 변경

기본적으로 Spring Boot Actuator는 관리 서버에 `/actuator` 경로를 사용합니다. `application.properties` 파일에 다음 속성을 추가하여 이를 변경할 수 있습니다.

```properties
management.server.servlet.path=/<path>
```

### 엔드포인트 ID 변경

기본적으로 Spring Boot Actuator는 위 표의 엔드포인트 ID를 사용합니다. `application.properties` 파일에 다음 속성을 추가하여 이를 변경할 수 있습니다.

```properties
management.endpoints.web.exposure.include=<endpoint1>,<endpoint2>,...
```

### 끝점 경로 변경

기본적으로 Spring Boot Actuator는 위 표의 엔드포인트 경로를 사용합니다. `application.properties` 파일에 다음 속성을 추가하여 이를 변경할 수 있습니다.

```properties
management.endpoint.<endpoint>.path=/<path>
```

### 엔드포인트 민감 정보 변경

기본적으로 Spring Boot Actuator는 엔드포인트 응답 본문에 민감한 정보를 노출합니다. `application.properties` 파일에 다음 속성을 추가하여 이를 변경할 수 있습니다.

```properties
management.endpoint.health.show-details=<value>
```

여기서 `<값>`은 다음 중 하나일 수 있습니다.

| 가치 | 설명 |
| --- | --- |
| `항상` | 항상 세부 정보를 표시합니다. |
| '절대' | 세부 정보를 표시하지 마십시오. |
| `when_authorized` | 사용자가 승인되면 세부 정보를 표시합니다. |

### 엔드포인트 보안 변경

기본적으로 Spring Boot Actuator는 끝점에 대해 HTTP 기본 인증을 사용합니다. `application.properties` 파일에 다음 속성을 추가하여 이를 변경할 수 있습니다.

```properties
management.security.enabled=false
```

### 엔드포인트 사용자 이름 및 비밀번호 변경

기본적으로 Spring Boot Actuator는 엔드포인트에 사용자 이름 'user'와 비밀번호 'password'를 사용합니다. `application.properties` 파일에 다음 속성을 추가하여 이를 변경할 수 있습니다.

```properties
management.security.user.name=<username>
management.security.user.password=<password>
```

## 결론

이 기사에서는 Spring Boot Actuator를 사용하여 애플리케이션을 모니터링하고 관리하는 방법을 살펴보았습니다. 액추에이터의 동작을 사용자 정의하는 방법도 살펴보았습니다.