---
title: 074: 캐싱 및 세션 관리를 위해 Redis와 Spring Boot 통합
description: 
published: true
date: 2023-02-02T15:23:31.023Z
tags: 
editor: markdown
dateCreated: 2023-02-02T15:23:29.446Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [074: Integrating Spring Boot with Redis for Caching and Session Management***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/074-integrating-spring-boot-with-redis-for-caching-and-session-management)
{.links-list}


# 소개

이 게시물에서는 캐싱 및 세션 관리를 위해 Redis와 Spring Boot를 통합하는 방법을 알아봅니다.

캐싱은 자주 액세스하는 데이터를 메모리에 저장하여 필요할 때 빠르게 검색할 수 있도록 하는 기술입니다. 세션 관리는 사용자의 기본 설정 또는 장바구니에 있는 항목과 같은 사용자 세션에 대한 데이터를 저장하고 검색하는 프로세스입니다.

캐싱과 세션 관리를 모두 사용하여 웹 애플리케이션의 성능을 향상시킬 수 있습니다. Redis는 빠르고 확장 가능하며 사용하기 쉽기 때문에 캐싱 및 세션 관리 모두에 널리 사용됩니다.

# 레디스 설치

Redis를 사용하기 전에 Redis를 설치해야 합니다. Redis는 모든 주요 운영 체제에서 사용할 수 있으므로 개발 시스템, 서버 또는 클라우드 환경에 설치할 수 있습니다.

Linux를 사용하는 경우 배포의 패키지 관리자에서 Redis를 설치할 수 있습니다. 예를 들어 Ubuntu에서는 apt를 사용할 수 있습니다.

```
sudo apt install redis-server
```

macOS를 사용하는 경우 Homebrew를 사용하여 Redis를 설치할 수 있습니다.

```
brew install redis
```

Windows를 사용하는 경우 Microsoft Store에서 Redis를 설치할 수 있습니다.

```
Get-AppxPackage -AllUsers -Name Microsoft.Portable.Redis | Foreach {Add-AppxPackage -DisableDevelopmentMode -Register "$($_.InstallLocation)\AppXManifest.xml"}
```

Redis가 설치되면 다음 명령을 실행하여 서버를 시작할 수 있습니다.

```
redis-server
```

# 스프링 부트 설정

이제 Redis가 설치되었으므로 이를 사용하도록 Spring Boot를 구성할 수 있습니다. 먼저 프로젝트에 spring-boot-starter-data-redis 스타터를 추가해야 합니다. 이 스타터는 Redis를 Spring Boot와 함께 사용하는 데 필요한 종속성을 가져옵니다.

Maven을 사용하는 경우 pom.xml 파일에 스타터를 추가할 수 있습니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

Gradle을 사용하는 경우 build.gradle 파일에 스타터를 추가할 수 있습니다.

```groovy
dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-data-redis'
}
```

스타터가 프로젝트에 추가되면 Redis 서버에 연결하도록 Spring Boot를 구성해야 합니다. application.properties 파일에 다음 속성을 추가하여 이를 수행할 수 있습니다.

```
spring.redis.host=localhost
spring.redis.port=6379
```

# Redis로 캐싱

이제 Redis를 구성했으므로 캐싱에 Redis를 사용할 수 있습니다. 캐싱은 자주 액세스하는 데이터를 메모리에 저장하여 필요할 때 빠르게 검색할 수 있도록 하는 기술입니다.

예를 들어 제품 목록을 표시하는 웹 애플리케이션이 있다고 가정해 보겠습니다. 페이지가 로드될 때마다 애플리케이션은 데이터베이스에서 제품 목록을 가져와야 합니다. 특히 데이터베이스가 크거나 원격에 있는 경우 속도가 느릴 수 있습니다.

Redis에서 제품 목록을 캐싱하여 페이지 속도를 높일 수 있습니다. 페이지가 처음 로드되면 애플리케이션은 데이터베이스에서 제품 목록을 가져와 Redis에 저장합니다. 페이지에 대한 후속 요청은 데이터베이스에서 가져오는 것보다 훨씬 빠른 Redis에서 제품 목록을 검색합니다.

Spring Boot에서 캐싱을 위해 Redis를 사용하려면 기본 애플리케이션 클래스에 @EnableCaching 주석을 추가해야 합니다.

```java
@SpringBootApplication
@EnableCaching
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

또한 캐시 관리자를 만들어야 합니다. 캐시 관리자는 애플리케이션의 캐시 관리를 담당합니다. Spring Boot는 Redis 캐시를 관리하는 데 사용할 수 있는 RedisCacheManager를 제공합니다.

@Bean 및 @Primary로 빈에 주석을 달아 RedisCacheManager를 만들 수 있습니다.

```java
@Bean
@Primary
public CacheManager cacheManager(RedisConnectionFactory connectionFactory) {
    return RedisCacheManager.create(connectionFactory);
}
```

# Redis로 세션 관리

캐싱 외에도 Redis는 세션 관리에도 사용할 수 있습니다. 세션 관리는 사용자의 기본 설정 또는 장바구니에 있는 항목과 같은 사용자 세션에 대한 데이터를 저장하고 검색하는 프로세스입니다.

사용자가 웹 애플리케이션에 로그인하면 세션이 생성됩니다. 이 세션은 사용자가 애플리케이션을 사용할 때 사용자 활동을 추적하는 데 사용됩니다. 예를 들어 사용자가 장바구니에 항목을 추가하면 장바구니에 항목을 저장하는 데 세션이 사용됩니다.

사용자가 로그아웃하거나 세션이 만료되면 세션 데이터가 삭제됩니다.

세션 관리는 데이터베이스에 저장하지 않고도 사용자 세션에 대한 데이터를 저장할 수 있기 때문에 중요합니다. 이렇게 하면 데이터베이스에서 데이터를 검색하는 속도가 느려질 수 있으므로 성능이 향상될 수 있습니다.

Spring Boot에서 세션 관리를 위해 Redis를 사용하려면 application.properties 파일에 다음 속성을 추가해야 합니다.

```
server.servlet.session.store-type=redis
```

이 속성은 세션 데이터를 저장하기 위해 Redis를 사용하도록 Spring Boot에 지시합니다.

# 결론

이번 포스트에서는 캐싱 및 세션 관리를 위해 Spring Boot와 Redis를 통합하는 방법을 배웠습니다. 또한 Redis를 설치하고 이를 사용하도록 Spring Boot를 구성하는 방법도 배웠습니다.