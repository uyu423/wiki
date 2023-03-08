---
title: 019: Spring Boot에서 사용자 정의 구성 생성 및 사용
description: 
published: true
date: 2023-02-03T11:32:32.493Z
tags: 
editor: markdown
dateCreated: 2023-02-03T11:32:30.802Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [019: Creating and using custom configurations in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/019-creating-and-using-custom-configurations-in-spring-boot)
{.links-list}


# Spring Boot에서 사용자 정의 구성 생성 및 사용

Spring Boot 애플리케이션을 개발할 때 사용자 지정 구성을 만들고 사용해야 할 수 있습니다. 이는 `src/main/resources` 폴더에 `application.yml`이라는 파일을 생성하여 수행할 수 있습니다.

이 파일에서 사용자 지정 구성 값을 지정할 수 있습니다. 예를 들어 애플리케이션이 실행될 포트를 지정할 수 있습니다.

```yaml
server:
  port: 8080
```

단일 키 아래에 여러 구성 값을 지정할 수도 있습니다. 예를 들어 포트와 컨텍스트 경로를 모두 지정할 수 있습니다.

```yaml
server:
  port: 8080
  context-path: /myapp
```

둘 이상의 구성 파일을 사용해야 하는 경우 `spring.config.location` 속성을 사용하여 로드할 파일을 지정할 수 있습니다.

```yaml
spring:
  config:
    location: classpath:application.yml,classpath:custom.yml
```

위의 예에서 `application.yml` 파일이 먼저 로드된 다음 `custom.yml` 파일이 로드됩니다.

시스템 속성이나 환경 변수를 사용하여 `spring.config.location` 속성을 지정할 수도 있습니다. 예를 들어 애플리케이션을 시작할 때 `spring.config.location` 시스템 속성을 설정할 수 있습니다.

```
java -jar myapp.jar --spring.config.location=classpath:application.yml,classpath:custom.yml
```

또는 `SPRING_CONFIG_LOCATION` 환경 변수를 설정할 수 있습니다.

```
SPRING_CONFIG_LOCATION=classpath:application.yml,classpath:custom.yml java -jar myapp.jar
```

## 구성 값 지정

Spring Boot에서 구성 값을 지정하는 방법에는 여러 가지가 있습니다. 가장 일반적인 방법은 이전 섹션에 표시된 대로 `application.yml` 파일을 사용하는 것입니다.

구성 값을 지정하는 또 다른 방법은 시스템 속성 또는 환경 변수를 사용하는 것입니다. 예를 들어 애플리케이션을 시작할 때 `server.port` 시스템 속성을 설정할 수 있습니다.

```
java -jar myapp.jar --server.port=8080
```

또는 `SERVER_PORT` 환경 변수를 설정할 수 있습니다.

```
SERVER_PORT=8080 java -jar myapp.jar
```

Java 시스템 특성을 사용하여 구성 값을 지정할 수도 있습니다. 예를 들어 `application.yml` 파일에서 `server.port` 시스템 속성을 설정할 수 있습니다.

```yaml
server:
  port: ${SERVER_PORT}
```

## 구성 값 액세스

구성 값을 지정하면 `@Value` 주석을 사용하여 코드에서 해당 값에 액세스할 수 있습니다.

```java
@Value("${server.port}")
private int port;
```

위의 예에서 `port` 변수는 `server.port` 구성 속성의 값으로 채워집니다.

여러 구성 값에 액세스해야 하는 경우 `@ConfigurationProperties` 주석 클래스를 만들 수 있습니다.

```java
@ConfigurationProperties(prefix = "server")
public class ServerProperties {

    private int port;
    private String contextPath;

    // getters and setters
}
```

위의 예에서 `port` 및 `contextPath` 변수는 각각 `server.port` 및 `server.context-path` 구성 속성의 값으로 채워집니다.

그런 다음 `ServerProperties` 클래스의 인스턴스를 코드에 삽입할 수 있습니다.

```java
@Autowired
private ServerProperties serverProperties;
```

## 결론

이 문서에서는 Spring Boot에서 사용자 지정 구성을 만들고 사용하는 방법을 배웠습니다. 또한 구성 값을 지정하는 방법과 코드에서 구성 값에 액세스하는 방법도 배웠습니다.