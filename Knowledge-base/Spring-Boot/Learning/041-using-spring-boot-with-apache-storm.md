---
title: 041: 아파치 스톰과 함께 스프링 부트 사용하기
description: 
published: true
date: 2023-02-04T07:32:19.480Z
tags: 
editor: markdown
dateCreated: 2023-02-04T07:32:17.920Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [041: Using Spring Boot with Apache Storm***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/041-using-spring-boot-with-apache-storm)
{.links-list}


# Apache Storm과 함께 Spring Boot 사용

이 게시물에서는 Apache Storm과 함께 Spring Boot를 사용하는 방법에 대해 알아봅니다. 다음 주제를 다룹니다.

* 아파치 스톰이란?
* 스프링 부트란?
* Apache Storm에서 Spring Boot를 사용하는 방법

## 아파치 스톰이란?

Apache Storm은 무료 오픈 소스 분산 실시간 계산 시스템입니다. Storm을 사용하면 Hadoop이 일괄 처리를 위해 수행한 작업을 실시간으로 처리하여 무한한 데이터 스트림을 안정적으로 처리할 수 있습니다.

Storm은 간단하고, 모든 프로그래밍 언어와 함께 사용할 수 있으며, 사용하기에 매우 재미있습니다!

## 스프링부트란?

Spring Boot는 "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 응용 프로그램을 쉽게 만들기 위한 프레임워크입니다. 최소한의 소란으로 시작할 수 있도록 Spring 플랫폼 및 타사 라이브러리에 대한 독단적인 견해를 취합니다. 대부분의 Spring Boot 애플리케이션에는 Spring 구성이 거의 필요하지 않습니다.

## Apache Storm에서 Spring Boot를 사용하는 방법

이제 Storm과 Spring Boot가 무엇인지 알았으니 함께 사용하는 방법을 살펴보겠습니다.

가장 먼저 필요한 것은 Storm에 대한 Maven 종속성입니다.

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>1.1.1</version>
    <scope>provided</scope>
</dependency>
```

Spring Boot에 대한 종속성도 필요합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

이제 Spring Boot 애플리케이션을 만들 수 있습니다.

```java
@SpringBootApplication
public class StormApplication {

    public static void main(String[] args) {
        SpringApplication.run(StormApplication.class, args);
    }

}
```

이제 애플리케이션에서 Storm 토폴로지를 만들 수 있습니다.

```java
@Component
public class MyTopology {

    @Autowired
    private TopologyBuilder topologyBuilder;

    @PostConstruct
    public void init() {
        // ...
    }

}
```

그리고 그게 다야! 이제 Spring Boot 애플리케이션 내에 작동하는 Storm 토폴로지가 있습니다.

## 추가 정보

* Apache Storm에 대한 자세한 내용은 [Apache Storm 웹사이트](https://storm.apache.org/)를 참조하세요.
* Spring Boot에 대한 자세한 내용은 [Spring Boot 웹사이트](https://projects.spring.io/spring-boot/)를 참조하십시오.