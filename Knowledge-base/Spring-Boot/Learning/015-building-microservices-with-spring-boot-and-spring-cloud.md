---
title: 015: Spring Boot 및 Spring Cloud로 마이크로서비스 구축
description: 
published: true
date: 2023-02-03T09:36:34.591Z
tags: 
editor: markdown
dateCreated: 2023-02-03T09:36:32.946Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [015: Building microservices with Spring Boot and Spring Cloud***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/015-building-microservices-with-spring-boot-and-spring-cloud)
{.links-list}


# 소개

마이크로서비스는 클라우드 네이티브 애플리케이션을 구축하는 데 널리 사용되는 아키텍처 스타일입니다. 이들은 독립적으로 배포할 수 있고 복잡한 애플리케이션으로 구성할 수 있는 작고 독립적인 장치입니다.

Spring Boot는 마이크로서비스 구축에 널리 사용되는 프레임워크입니다. "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다.

Spring Cloud는 마이크로서비스 구축을 위한 오픈 소스 도구의 생태계입니다. 서비스 검색, 회로 차단기 및 분산 추적과 같은 분산 시스템에서 사용되는 공통 패턴에 대한 라이브러리를 제공합니다.

이번 포스트에서는 Spring Boot와 Spring Cloud로 마이크로서비스를 구축하는 방법에 대해 알아보겠습니다. "hello world" 마이크로서비스의 간단한 예제로 시작한 다음 Spring Cloud Netflix Eureka 및 Ribbon을 사용하여 서비스 검색 및 로드 밸런싱을 추가합니다. 마지막으로 Spring Cloud Sleuth를 사용하여 분산 추적을 추가합니다.

# "Hello World" 마이크로서비스 구축

간단한 "hello world" 마이크로서비스를 만들어 보겠습니다. Spring Initializr를 사용하여 다음 종속성이 있는 프로젝트를 생성합니다.

- 웹
- 액추에이터

웹 의존성은 Spring MVC로 웹 애플리케이션을 구축하기 위한 지원을 추가합니다. Actuator 종속성은 애플리케이션 모니터링 및 관리에 대한 지원을 추가합니다.

프로젝트가 생성되면 IDE에서 프로젝트를 열고 간단한 컨트롤러를 추가할 수 있습니다.

```java
@RestController
public class HelloController {

    @RequestMapping("/")
    public String hello() {
        return "Hello, world!";
    }

}
```

이 컨트롤러에는 "Hello, world!"를 반환하는 단일 엔드포인트가 있습니다. 메시지.

애플리케이션을 실행하기 위해 Spring Boot Maven 플러그인을 사용할 수 있습니다.

```
./mvnw spring-boot:run
```

애플리케이션이 실행되면 http://localhost:8080/에서 "hello world" 엔드포인트에 액세스할 수 있습니다.

# 서비스 디스커버리 추가

마이크로서비스 아키텍처에서 서비스는 일반적으로 노드 클러스터에 배포됩니다. 서비스가 배포되면 다른 서비스에서 찾을 수 있도록 서비스 검색 서버에 등록해야 합니다.

Spring Cloud Netflix Eureka는 인기 있는 서비스 검색 서버입니다. 프로젝트에 Eureka를 추가하기 위해 다음 종속성을 추가할 수 있습니다.

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

종속성이 추가되면 기본 애플리케이션 클래스에 @EnableEurekaServer 주석을 추가하여 Eureka 서버를 활성화할 수 있습니다.

```java
@SpringBootApplication
@EnableEurekaServer
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

이제 애플리케이션을 시작하고 http://localhost:8761/에서 Eureka 대시보드에 액세스할 수 있습니다.

# 부하 분산 추가

마이크로서비스 아키텍처에서는 서비스가 여러 노드에 배포되는 것이 일반적입니다. 서비스가 호출되면 로드 밸런서를 사용하여 요청을 노드 중 하나로 라우팅합니다.

Spring Cloud Netflix 리본은 널리 사용되는 로드 밸런서입니다. 리본을 프로젝트에 추가하기 위해 다음 종속성을 추가할 수 있습니다.

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-ribbon</artifactId>
</dependency>
```

종속성이 추가되면 기본 애플리케이션 클래스에 @RibbonClient 주석을 추가하여 리본을 구성할 수 있습니다.

```java
@SpringBootApplication
@EnableEurekaServer
@RibbonClient(name = "hello-service")
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

이 주석은 "hello-service" 서비스에 대한 리본 클라이언트를 구성합니다.

# 분산 추적 추가

마이크로서비스 아키텍처에서는 요청이 여러 서비스를 통해 라우팅될 수 있기 때문에 문제를 해결하기 어려울 수 있습니다. 분산 추적은 시스템을 통과하는 요청을 추적하여 도움이 될 수 있습니다.

Spring Cloud Sleuth는 널리 사용되는 분산 추적 프레임워크입니다. 프로젝트에 Sleuth를 추가하기 위해 다음 종속성을 추가할 수 있습니다.

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-sleuth</artifactId>
</dependency>
```

종속성이 추가되면 Sleuth는 요청을 추적하도록 자동으로 구성됩니다.

# 결론

이번 포스트에서는 Spring Boot와 Spring Cloud로 마이크로서비스를 구축하는 방법에 대해 알아보았습니다. 간단한 "hello world" 마이크로서비스로 시작하여 서비스 검색, 로드 밸런싱 및 분산 추적을 추가했습니다.