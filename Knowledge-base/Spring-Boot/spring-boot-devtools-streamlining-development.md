---
title: Spring Boot DevTools: 개발 간소화
description: 
published: true
date: 2023-02-01T04:57:32.965Z
tags: 
editor: markdown
dateCreated: 2023-02-01T04:57:29.166Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Spring Boot DevTools: Streamlining Development***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-devtools-streamlining-development)
{.links-list}



# Spring Boot DevTools: 개발 간소화

Spring Boot DevTools는 Spring Boot 애플리케이션으로 작업할 때 개발 환경을 개선하는 데 사용할 수 있는 도구 세트를 제공합니다. 이러한 도구를 사용하여 애플리케이션을 빠르게 다시 시작하고, 정적 리소스를 실시간으로 다시 로드하고, 기타 여러 개발 관련 작업을 수행할 수 있습니다.

이 기사에서는 Spring Boot DevTools를 사용하여 개발 프로세스를 간소화하는 방법을 살펴보겠습니다. 또한 DevTools가 제공하는 다른 기능 중 일부를 살펴보겠습니다.

## 빠른 재시작

DevTools의 가장 유용한 기능 중 하나는 애플리케이션을 빠르게 다시 시작하는 기능입니다. 응용 프로그램이 실행되는 동안 "R" 키를 누르기만 하면 됩니다.

DevTools는 코드에 대한 모든 변경 사항을 자동으로 감지하고 애플리케이션을 다시 시작합니다. 즉, 변경할 때마다 애플리케이션을 수동으로 중지하고 시작할 필요가 없습니다.

## 라이브 리로드

DevTools의 또 다른 유용한 기능은 실시간 재로드입니다. 이 기능은 HTML, CSS 및 JavaScript와 같은 정적 리소스가 변경될 때 자동으로 다시 로드하는 데 사용할 수 있습니다.

라이브 리로드를 사용하려면 먼저 `pom.xml` 파일에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-devtools</artifactId>
  <optional>true</optional>
</dependency>
```

그런 다음 `application.properties` 파일에 다음 속성을 추가하여 실시간 재로드를 활성화할 수 있습니다.

```properties
spring.devtools.livereload.enabled=true
```

## 원격 개발

DevTools는 Spring Boot 애플리케이션을 원격으로 디버깅하고 개발하는 기능도 제공합니다. 이는 `application.properties` 파일에 다음 속성을 추가하여 수행할 수 있습니다.

```properties
spring.devtools.remote.secret=<secret>
```

`<비밀>`을 선택한 비밀로 바꿉니다. 이 비밀은 들어오는 요청을 인증하는 데 사용됩니다.

완료하면 다음 명령을 사용하여 디버그 모드에서 애플리케이션을 시작할 수 있습니다.

```
$ mvn spring-boot:run -Dspring-boot.run.jvmArguments='-Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=5005'
```

이렇게 하면 디버그 모드에서 애플리케이션이 시작되고 포트 5005에서 수신 대기합니다. 그런 다음 Eclipse 또는 Visual Studio Code와 같은 원격 디버거를 사용하여 애플리케이션에 연결할 수 있습니다.

## 결론

이 기사에서는 Spring Boot DevTools를 사용하여 개발 프로세스를 간소화하는 방법을 살펴보았습니다. DevTools가 제공하는 다른 기능 중 일부도 살펴보았습니다.

개발 환경을 개선하려는 경우 DevTools를 확인해 볼 가치가 있습니다.