---
title: 091: 조정 및 동기화를 위해 Apache Zookeeper와 Spring Boot 통합
description: 
published: true
date: 2023-02-05T21:32:22.415Z
tags: 
editor: markdown
dateCreated: 2023-02-05T21:32:20.809Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [091: Integrating Spring Boot with Apache Zookeeper for Coordination and Synchronization***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/091-integrating-spring-boot-with-apache-zookeeper-for-coordination-and-synchronization)
{.links-list}


# 091: 조정 및 동기화를 위해 Apache Zookeeper와 Spring Boot 통합

Apache Zookeeper는 분산 시스템을 위한 분산 조정 서비스입니다. 대규모 분산 시스템을 관리하는 데 사용됩니다. Spring Boot는 마이크로서비스 개발에 널리 사용되는 Java 프레임워크입니다.

이번 포스트에서는 Spring Boot와 Apache Zookeeper를 통합하는 방법에 대해 알아보겠습니다. Zookeeper를 사용하여 Spring Boot 마이크로 서비스를 조정하고 동기화합니다.

## 아파치 주키퍼 설치하기

Zookeeper를 사용하기 전에 먼저 설치해야 합니다. macOS에서 Homebrew를 사용하여 Zookeeper를 설치할 수 있습니다.

```
$ brew install zookeeper
```

또는 [Apache Zookeeper 웹사이트](https://zookeeper.apache.org/)에서 Zookeeper 바이너리 릴리스를 다운로드할 수 있습니다.

## 아파치 주키퍼 시작하기

Zookeeper가 설치되면 다음 명령을 사용하여 시작할 수 있습니다.

```
$ zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties
```

## 스프링 부트 프로젝트 생성

[Spring Initializr](https://start.spring.io/)를 사용하여 Spring Boot 프로젝트를 생성할 수 있습니다. 다음 종속성을 사용합니다.

* 웹
* 액추에이터
* 롬복

## 스프링 부트 설정

Zookeeper를 사용하려면 Spring Boot 애플리케이션을 구성해야 합니다. `application.properties` 파일에 다음 속성을 추가하여 이를 수행할 수 있습니다.

```properties
spring.cloud.zookeeper.connect-string=localhost:2181
spring.cloud.zookeeper.discovery.instance-id=${spring.application.name}
spring.cloud.zookeeper.discovery.root=/${spring.application.name}
spring.cloud.zookeeper.discovery.service-name=${spring.application.name}
spring.cloud.zookeeper.discovery.enabled=true
```

## 스프링 부트 서비스 생성

`@SpringBootApplication` 주석을 사용하여 Spring Boot 서비스를 만들 수 있습니다.

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

## 나머지 컨트롤러 추가

`@RestController` 주석을 사용하여 Rest 컨트롤러를 서비스에 추가할 수 있습니다.

```java
@RestController
public class GreetingController {

    @GetMapping("/greeting")
    public String greeting() {
        return "Hello, world!";
    }

}
```

## 서비스 테스트

`/greeting` 엔드포인트에 `GET` 요청을 전송하여 서비스를 테스트할 수 있습니다.

```
$ curl localhost:8080/greeting
Hello, world!
```

## Zookeeper에 서비스 등록하기

서비스가 실행되면 Zookeeper에 등록해야 합니다. `@DiscoveryClient` 주석을 사용하여 이를 수행할 수 있습니다.

```java
@SpringBootApplication
@DiscoveryClient
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

## 다른 서비스에서 서비스에 액세스

우리 서비스가 Zookeeper에 등록되면 다른 서비스에서 액세스할 수 있습니다. 컨트롤러에 `DiscoveryClient`를 삽입하여 이를 수행할 수 있습니다.

```java
@RestController
public class GreetingController {

    @Autowired
    private DiscoveryClient discoveryClient;

    @GetMapping("/greeting")
    public String greeting() {
        List<ServiceInstance> instances = discoveryClient.getInstances("greeting-service");
        if (instances.isEmpty()) {
            return "Hello, world!";
        }
        String url = instances.get(0).getUri().toString();
        return "Hello, world! (from " + url + ")";
    }

}
```

## 결론

이번 포스트에서는 Spring Boot와 Apache Zookeeper를 통합하는 방법에 대해 알아보았습니다. 우리는 Zookeeper를 사용하여 Spring Boot 마이크로서비스를 조정하고 동기화했습니다.