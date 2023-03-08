---
title: 034: Spring Cloud 구성과 함께 Spring Boot 사용
description: 
published: true
date: 2023-02-04T02:32:36.860Z
tags: 
editor: markdown
dateCreated: 2023-02-04T02:32:31.599Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [034: Using Spring Boot with Spring Cloud Config***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/034-using-spring-boot-with-spring-cloud-config)
{.links-list}


# Spring Cloud Config와 함께 Spring Boot 사용

Spring Cloud Config는 분산 시스템에서 외부화된 구성을 위한 서버 및 클라이언트 측 지원을 제공합니다. 구성 서버는 @EnableConfigServer 주석을 통해 Spring Boot 애플리케이션과 함께 쉽게 사용할 수 있습니다.

이 게시물에서는 Spring Boot 애플리케이션과 함께 구성 서버를 사용하는 방법을 살펴보겠습니다. 또한 구성 클라이언트를 사용하여 구성 서버에 연결하고 구성을 가져오는 방법도 살펴보겠습니다.

## 구성 서버 설정

가장 먼저 해야 할 일은 구성 서버를 설정하는 것입니다. Spring Boot 애플리케이션에서 @EnableConfigServer 주석을 사용하여 이를 수행할 수 있습니다.

```java
@SpringBootApplication
@EnableConfigServer
public class ConfigServerApplication {

    public static void main(String[] args) {
        SpringApplication.run(ConfigServerApplication.class, args);
    }
}
```

이렇게 하면 애플리케이션에서 구성 서버가 활성화됩니다. 기본적으로 구성 서버는 애플리케이션의 클래스 경로에 있는 파일에서 구성을 제공합니다.

Git 리포지토리에서 구성을 가져오도록 구성 서버를 구성할 수도 있습니다. 예를 들어 application.properties 파일에 다음을 추가할 수 있습니다.

```properties
spring.cloud.config.server.git.uri=https://github.com/spring-cloud/spring-cloud-config
spring.cloud.config.server.git.searchPaths=config-repo
```

이렇게 하면 구성 서버가 config-repo 디렉터리의 spring-cloud-config GitHub 리포지토리에서 구성을 가져오도록 지시합니다.

## 구성 클라이언트 설정

이제 구성 서버를 설정했으므로 구성 클라이언트를 설정할 수 있습니다. 구성 클라이언트는 구성 서버에서 구성을 가져오는 Spring Boot 애플리케이션입니다.

@EnableConfigClient 주석을 사용하여 구성 클라이언트를 설정할 수 있습니다.

```java
@SpringBootApplication
@EnableConfigClient
public class ConfigClientApplication {

    public static void main(String[] args) {
        SpringApplication.run(ConfigClientApplication.class, args);
    }
}
```

이렇게 하면 애플리케이션에서 구성 클라이언트가 활성화됩니다. 기본적으로 구성 클라이언트는 http://localhost:8888에서 구성 서버에 연결합니다.

다른 구성 서버에 연결하도록 구성 클라이언트를 구성할 수도 있습니다. 예를 들어 application.properties 파일에 다음을 추가할 수 있습니다.

```properties
spring.cloud.config.uri=http://config-server:8888
```

이렇게 하면 구성 클라이언트가 http://config-server:8888에서 구성 서버에 연결하도록 지시합니다.

## 구성 가져오기

구성 서버와 구성 클라이언트가 설정되면 구성 서버에서 구성을 가져올 수 있습니다. 구성 클라이언트는 구성을 가져와 애플리케이션에서 사용할 수 있도록 합니다.

예를 들어 application.properties 파일에 다음을 추가할 수 있습니다.

```properties
spring.cloud.config.name=my-app
```

이렇게 하면 구성 클라이언트가 my-app 애플리케이션에 대한 구성을 가져오도록 지시합니다. 구성은 Spring 환경을 통해 애플리케이션에서 사용할 수 있습니다.

특정 프로필에 대한 구성을 가져올 수도 있습니다. 예를 들어 application.properties 파일에 다음을 추가할 수 있습니다.

```properties
spring.cloud.config.name=my-app
spring.cloud.config.profile=dev
```

이렇게 하면 구성 클라이언트가 dev 프로필을 사용하여 my-app 애플리케이션에 대한 구성을 가져오도록 지시합니다. 구성은 Spring 환경을 통해 애플리케이션에서 사용할 수 있습니다.

## 결론

이 게시물에서는 Spring Boot 애플리케이션에서 구성 서버를 사용하는 방법을 살펴보았습니다. 또한 구성 클라이언트를 사용하여 구성 서버에 연결하고 구성을 가져오는 방법도 살펴보았습니다.