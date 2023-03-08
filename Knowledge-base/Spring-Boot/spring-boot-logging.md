---
title: 스프링 부트 로깅
description: 
published: true
date: 2023-02-01T02:17:22.500Z
tags: 
editor: markdown
dateCreated: 2023-02-01T02:17:20.837Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Spring Boot Logging***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-logging)
{.links-list}



# 스프링 부트 로깅

Spring Boot를 사용하면 애플리케이션에 대한 로깅을 쉽게 구성할 수 있습니다. 기본적으로 Spring Boot는 `java.util.logging`(JUL) 로깅 프레임워크를 사용하도록 애플리케이션을 구성합니다. 프로젝트에 적절한 스타터 종속성을 추가하여 Log4j2, Logback 또는 slf4j를 사용하도록 변경할 수 있습니다.

이 기사에서는 Spring Boot에서 로깅을 구성하는 방법을 살펴보겠습니다. 기본 예제로 시작한 다음 고급 항목으로 이동합니다.

## 기본 구성

Spring Boot에서 로깅을 구성하는 가장 간단한 방법은 `application.properties` 파일에 `logging.level` 속성을 추가하는 것입니다. 로깅 수준은 특정 패키지 또는 특정 로거에 대해 설정할 수 있습니다. 예를 들어 다음 구성은 `com.example` 패키지의 로깅 수준을 `DEBUG`로 설정합니다.

```
logging.level.com.example=DEBUG
```

모든 패키지의 로깅 수준을 설정하려면 `root` 로거를 사용할 수 있습니다. 예를 들어 다음 구성은 모든 패키지의 로깅 수준을 'INFO'로 설정합니다.

```
logging.level.root=INFO
```

## 로거

로깅 수준을 설정하는 것 외에도 로그 출력 형식을 구성할 수도 있습니다. 기본적으로 Spring Boot는 `%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n` 형식으로 로그 메시지를 출력합니다.

`logging.pattern.console` 속성을 설정하여 형식을 변경할 수 있습니다. 예를 들어 다음 구성은 로그 메시지를 `%d [%thread] %-5level %logger{36} - %msg%n` 형식으로 출력합니다.

```
logging.pattern.console=%d [%thread] %-5level %logger{36} - %msg%n
```

## 어펜더

콘솔 외에도 Spring Boot는 파일에 로그인할 수도 있습니다. 기본적으로 로그 메시지는 `tmp` 디렉토리의 `spring.log` 파일에 출력됩니다. `logging.file` 속성을 설정하여 파일의 위치를 변경할 수 있습니다. 예를 들어 다음 구성은 로그 메시지를 `/var/log/spring.log` 파일로 출력합니다.

```
logging.file=/var/log/spring.log
```

## 커스텀 로거

사용자 지정 로거를 만들려면 `logging.config` 속성을 사용하여 log4j2.xml 파일의 위치를 지정할 수 있습니다. 예를 들어 다음 구성은 로그 메시지를 `/var/log/spring.log` 파일로 출력합니다.

```
logging.config=log4j2.xml
```

## 고급 구성

기본 구성 외에도 Spring Boot는 여러 고급 기능을 제공합니다. 예를 들어 로그 메시지를 여러 파일에 출력하도록 로거를 구성할 수 있습니다. 특정 클래스에 대한 로그 수준을 설정할 수도 있습니다.

## 여러 파일에 로깅

`logging.file.name` 및 `logging.file.max-size` 속성을 설정하여 로그 메시지를 여러 파일에 출력하도록 로거를 구성할 수 있습니다. 예를 들어, 다음 구성은 `tmp` 디렉토리의 `spring.log` 및 `spring.log.1` 파일에 로그 메시지를 출력합니다.

```
logging.file.name=spring.log
logging.file.max-size=10MB
```

## 클래스의 로깅 수준

`logging.level.{class}` 속성을 설정하여 특정 클래스에 대한 로깅 수준을 설정할 수 있습니다. 예를 들어 다음 구성은 `com.example.MyClass` 클래스의 로깅 수준을 `DEBUG`로 설정합니다.

```
logging.level.com.example.MyClass=DEBUG
```

## 결론

이 기사에서는 Spring Boot에서 로깅을 구성하는 방법을 살펴보았습니다. 로깅 수준을 설정하는 방법과 로그 출력 형식을 변경하는 방법을 살펴보았습니다. 또한 여러 파일에 로그 메시지를 출력하는 방법과 특정 클래스에 대한 로깅 수준을 설정하는 방법도 살펴보았습니다.