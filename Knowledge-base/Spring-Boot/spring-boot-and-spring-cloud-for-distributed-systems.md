---
title: 분산 시스템용 Spring Boot 및 Spring Cloud
description: 
published: true
date: 2023-02-03T19:17:27.803Z
tags: 
editor: markdown
dateCreated: 2023-02-03T19:17:22.854Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot and Spring Cloud for Distributed Systems***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-spring-cloud-for-distributed-systems)
{.links-list}


# 분산 시스템을 위한 Spring Boot 및 Spring Cloud

클라우드는 많은 기업과 조직에서 새로운 표준이 되었습니다. 비용 효율적이고 확장 가능하며 여러 가지 다른 이점을 제공합니다. 그러나 움직이는 부분이 많아 복잡할 수도 있습니다.

클라우드에서 분산 시스템을 보다 쉽게 개발할 수 있는 한 가지 방법은 Spring Boot 및 Spring Cloud를 사용하는 것입니다. 이 기사에서는 이 두 프레임워크가 무엇이며 어떻게 함께 사용할 수 있는지 살펴보겠습니다.

## 스프링부트란?

Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 만드는 데 도움이 되는 프레임워크입니다. 최소한의 구성으로 가능한 한 빨리 시작하고 실행할 수 있도록 설계되었습니다.

Spring Boot에는 다음과 같은 다양한 기능이 포함되어 있습니다.

- 애플리케이션을 쉽게 배포할 수 있는 임베디드 서버
- 다양한 데이터 소스 지원
- 최소한의 구성으로 프로젝트에 공통 종속성을 추가하는 데 사용할 수 있는 다수의 스타터 종속성
- Spring Bean 자동 구성
- 독창적이지만 유연한 구성

Spring Boot를 사용하면 Spring 기반 애플리케이션 및 서비스를 쉽게 만들 수 있습니다. Spring 플랫폼에 대한 독단적인 관점을 취하고 최소한의 구성으로 시작하고 실행할 수 있습니다.

## 스프링클라우드란?

Spring Cloud는 클라우드 네이티브 애플리케이션을 구축하기 위한 도구 모음입니다. 다음과 같은 다양한 기능을 제공합니다.

- Service Discovery: 서비스 등록 및 검색을 위한 메커니즘
- 구성 관리: 분산형 구성 서비스
- 라우팅: 요청을 백엔드 서비스로 라우팅하기 위한 역방향 프록시 서비스
- 로드 밸런싱: 클라이언트 측 로드 밸런싱 라이브러리
- 회로 차단기: 분산 시스템의 장애를 관리하기 위한 라이브러리

Spring Cloud는 확장 가능하고 탄력적이며 스스로 관리하는 클라우드 네이티브 애플리케이션을 구축하는 데 도움이 됩니다.

## Spring Boot와 Spring Cloud를 함께 사용하기

Spring Boot와 Spring Cloud는 함께 잘 작동합니다. Spring Boot를 사용하면 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있으며 Spring Cloud를 사용하면 마이크로 서비스를 쉽게 구축하고 배포할 수 있습니다.

다음은 Spring Boot 및 Spring Cloud로 구축된 마이크로서비스의 간단한 예입니다.

```java
@SpringBootApplication
@EnableDiscoveryClient
public class MyService {
    
    @Autowired
    private DiscoveryClient discoveryClient;
    
    @RequestMapping("/")
    public String home() {
        return "Hello from MyService";
    }
    
    @RequestMapping("/service-instances/{applicationName}")
    public List<ServiceInstance> serviceInstancesByApplicationName(
        @PathVariable String applicationName) {
        return this.discoveryClient.getInstances(applicationName);
    }
}
```

이 마이크로서비스는 Spring Cloud DiscoveryClient에 등록되어 다른 서비스에서 검색할 수 있습니다. 또한 두 개의 REST 끝점을 노출합니다. 하나는 간단한 인사말을 반환하기 위한 것이고 다른 하나는 지정된 애플리케이션 이름에 대한 ServiceInstances 목록을 반환하기 위한 것입니다.

이 마이크로서비스를 실행하려면 Spring Boot Maven 플러그인을 사용할 수 있습니다.

```
$ mvn spring-boot:run
```

그런 다음 http://localhost:8080에서 마이크로서비스에 액세스할 수 있습니다.

## 결론

이 기사에서는 Spring Boot와 Spring Cloud가 무엇이며 어떻게 함께 사용할 수 있는지 살펴보았습니다. 또한 이 두 프레임워크로 구축된 마이크로서비스의 간단한 예도 보았습니다.

클라우드에서 분산 시스템 개발을 단순화하는 방법을 찾고 있다면 Spring Boot와 Spring Cloud를 확인해 볼 가치가 있습니다.