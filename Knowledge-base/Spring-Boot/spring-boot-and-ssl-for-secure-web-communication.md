---
title: 보안 웹 통신을 위한 Spring Boot 및 SSL
description: 
published: true
date: 2023-02-08T05:32:40.749Z
tags: 
editor: markdown
dateCreated: 2023-02-08T05:32:39.318Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot and SSL for Secure Web Communication***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-ssl-for-secure-web-communication)
{.links-list}


# 보안 웹 통신을 위한 Spring Boot 및 SSL

이 기사에서는 보안 웹 통신을 위해 Spring Boot 및 SSL을 사용하는 방법을 살펴보겠습니다. SSL을 사용하도록 Spring Boot를 구성하는 방법, 자체 서명된 SSL 인증서를 만드는 방법 및 프로덕션 환경을 위해 SSL을 구성하는 방법을 살펴보겠습니다.

## SSL용 스프링 부트 구성

SSL을 사용하도록 Spring Boot를 구성하는 것은 매우 간단합니다. 먼저 `pom.xml`에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

다음으로 SSL을 사용하도록 `application.properties` 파일을 구성해야 합니다. 파일에 다음 줄을 추가합니다.

```
server.port: 8443
server.ssl.key-alias: springboot
server.ssl.key-store: keystore.jks
server.ssl.key-store-password: secret
```

`keystore.jks`를 키 저장소 파일의 경로로 바꾸고 `secret`을 키 저장소의 암호로 바꿉니다.

## 자체 서명된 SSL 인증서 생성

애플리케이션을 개발하고 테스트하는 중이라면 자체 서명된 SSL 인증서를 생성할 수 있습니다. 이렇게 하려면 JDK와 함께 제공되는 `keytool` 유틸리티를 사용해야 합니다. 먼저 키 저장소 파일을 만듭니다.

```
keytool -genkey -alias springboot -keyalg RSA -keysize 2048 -keystore keystore.jks
```

키 저장소의 암호를 입력하라는 메시지가 표시됩니다. 비밀번호를 입력하고 엔터를 누릅니다. 그러면 이름, 조직 등을 입력하라는 메시지가 표시됩니다.

키 저장소가 생성되면 자체 서명된 인증서를 생성해야 합니다.

```
keytool -selfsign -alias springboot -keyalg RSA -keysize 2048 -validity 365 -keystore keystore.jks
```

'365'를 인증서 유효 기간으로 바꾸십시오.

## 프로덕션 환경을 위한 SSL 구성

애플리케이션을 프로덕션 환경에 배포하는 경우 인증 기관에서 적절한 SSL 인증서를 받아야 합니다. 인증서가 있으면 키 저장소로 가져올 수 있습니다.

```
keytool -import -alias springboot -file your_certificate.crt -keystore keystore.jks
```

`your_certificate.crt`를 인증서 경로로 바꿉니다. 키 저장소 암호를 입력하라는 메시지가 표시됩니다. 비밀번호를 입력하고 엔터를 누릅니다.

## 결론

이 기사에서는 보안 웹 통신을 위해 Spring Boot 및 SSL을 사용하는 방법을 살펴보았습니다. SSL을 사용하도록 Spring Boot를 구성하는 방법, 자체 서명된 SSL 인증서를 만드는 방법 및 프로덕션 환경에 대해 SSL을 구성하는 방법을 살펴보았습니다.