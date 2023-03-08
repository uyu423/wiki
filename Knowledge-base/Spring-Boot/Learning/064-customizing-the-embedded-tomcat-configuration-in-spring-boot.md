---
title: 064: Spring Boot에서 Embedded Tomcat 구성 사용자 지정
description: 
published: true
date: 2023-02-02T16:23:33.376Z
tags: 
editor: markdown
dateCreated: 2023-02-02T16:23:28.849Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [064: Customizing the Embedded Tomcat Configuration in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/064-customizing-the-embedded-tomcat-configuration-in-spring-boot)
{.links-list}


# Spring Boot에서 Embedded Tomcat 구성 사용자 지정

Spring Boot는 임베디드 Tomcat 구성을 사용자 지정하는 데 사용할 수 있는 여러 기능을 제공합니다. 이 게시물에서는 가장 중요한 몇 가지 구성 옵션을 살펴보겠습니다.

## HTTP 포트 구성

가장 먼저 할 일은 Tomcat이 실행 중인 HTTP 포트를 변경하는 것입니다. 기본적으로 Tomcat은 포트 8080에서 실행되지만 application.properties 파일에서 ```server.port``` 속성을 설정하여 이를 변경할 수 있습니다.

```properties
server.port=8081
```

## Tomcat 세션 시간 초과 구성

또 다른 일반적인 사용자 지정은 세션 시간 제한을 변경하는 것입니다. 기본적으로 Tomcat은 30분 세션 제한 시간을 사용하지만 ```server.session-timeout``` 속성을 설정하여 이를 변경할 수 있습니다.

```properties
server.session-timeout=1
```

## Tomcat 액세스 로그 구성

또한 Tomcat은 서버에 대한 모든 요청에 대한 정보가 포함된 액세스 로그를 생성합니다. 기본적으로 이 로그는 ```logs``` 디렉토리에 있지만 ```server.tomcat.accesslog.directory``` 속성을 설정하여 위치를 변경할 수 있습니다.

```properties
server.tomcat.accesslog.directory=/var/log/tomcat
```

## Tomcat URI 인코딩 구성

기본적으로 Tomcat은 URI 인코딩에 ISO-8859-1 문자 집합을 사용합니다. 그러나 ```server.tomcat.uri-encoding``` 속성을 설정하여 이를 변경할 수 있습니다.

```properties
server.tomcat.uri-encoding=UTF-8
```

## Tomcat 커넥터 구성

Tomcat은 커넥터를 사용하여 요청을 받고 응답을 보냅니다. 기본적으로 Tomcat은 AJP 커넥터를 사용하지만 ```server.tomcat.protocol-header``` 속성을 설정하여 이를 변경할 수 있습니다.

```properties
server.tomcat.protocol-header=org.apache.coyote.http11.Http11NioProtocol
```

## Tomcat 컨텍스트 경로 구성

컨텍스트 경로는 애플리케이션에 액세스하는 데 사용되는 경로입니다. 기본적으로 ```/```로 설정되지만 ```server.context-path``` 속성을 설정하여 변경할 수 있습니다.

```properties
server.context-path=/myapp
```

## Tomcat SSL 구성

Tomcat은 보안 통신을 위해 SSL도 지원합니다. SSL을 구성하려면 ```server.ssl.key-store```, ```server.ssl.key-store-password```, ```server.ssl.key-alias를 설정해야 합니다. ``` 및 ```server.ssl.key-alias-password``` 속성. Tomcat에서 SSL을 구성하는 방법에 대한 자세한 내용은 [Tomcat SSL 구성 방법](https://tomcat.apache.org/tomcat-8.5-doc/ssl-howto.html)을 참조하세요.

## 결론

이 게시물에서는 Spring Boot에서 임베디드 Tomcat 구성을 사용자 정의하는 가장 중요한 몇 가지 방법을 살펴보았습니다. 몇 가지 간단한 속성을 변경하여 필요에 맞게 Tomcat 실행 방식을 변경할 수 있습니다.