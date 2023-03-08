---
title: Netflix OSS를 사용한 Spring Boot 마이크로서비스
description: 
published: true
date: 2023-02-08T00:32:55.345Z
tags: 
editor: markdown
dateCreated: 2023-02-08T00:32:53.647Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot Microservices with Netflix OSS***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-microservices-with-netflix-oss)
{.links-list}


# Netflix OSS를 사용한 Spring Boot 마이크로서비스

과거에는 대규모 모놀리식 애플리케이션이 단일 단위로 구축되었습니다. 그러나 애플리케이션의 크기와 복잡성이 증가함에 따라 유지 관리가 점점 더 어려워졌습니다. 또한 전체 애플리케이션을 한 번에 배포해야 했기 때문에 이러한 애플리케이션의 배포가 더욱 복잡해졌습니다.

이러한 문제를 해결하기 위해 마이크로서비스는 애플리케이션 구축을 위한 인기 있는 아키텍처 스타일이 되었습니다. 마이크로서비스는 더 큰 애플리케이션을 형성하기 위해 함께 작동하는 작은 독립형 서비스입니다. 이 아키텍처에는 다음과 같은 많은 이점이 있습니다.

- 손쉬운 배포 및 확장: 마이크로서비스는 독립적으로 배포 및 확장할 수 있으므로 필요에 따라 새로운 기능을 쉽게 배포하거나 서비스를 확장할 수 있습니다.

- 느슨한 결합: 서비스는 독립적이며 다른 서비스에 영향을 주지 않고 변경 또는 업데이트할 수 있습니다.

- 복원력: 하나의 서비스가 중단되더라도 다른 서비스는 계속 실행될 수 있습니다.

Netflix OSS는 마이크로서비스 구축을 위한 도구 및 라이브러리 세트입니다. 이 기사에서는 Netflix OSS를 사용하여 Spring Boot 마이크로 서비스를 구축하는 방법을 배웁니다.

## 전제 조건

시작하기 전에 필요한 몇 가지 사항이 있습니다.

- 자바 8
- 메이븐 3.3.9 이상

## 스프링 부트 프로젝트 생성

Spring Boot 프로젝트를 생성하는 것으로 시작하겠습니다. 이 예제에서는 Spring Initializr를 사용하여 프로젝트를 생성합니다.

https://start.spring.io/로 이동하여 다음 옵션을 선택합니다.

- 프로젝트: 메이븐 프로젝트
- 언어: 자바
- 스프링 부트 버전: 2.1.3

"프로젝트 생성"을 클릭하여 프로젝트를 다운로드합니다.

## 의존성 추가

다음으로 프로젝트에 몇 가지 종속성을 추가해야 합니다. 생성된 `pom.xml` 파일을 열고 다음 종속성을 추가합니다.

```xml
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-actuator</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
	</dependency>
</dependencies>
```

`spring-boot-starter-actuator` 종속성은 애플리케이션을 모니터링하고 관리하는 기능을 제공합니다. 'spring-cloud-starter-netflix-eureka-client' 종속성은 Eureka 서비스 검색 도구와의 통합을 제공합니다.

## 유레카 구성

Eureka는 서비스 검색 도구입니다. 이를 통해 서비스가 스스로 등록하고 다른 서비스에서 검색할 수 있습니다. 우리는 마이크로서비스를 발견하기 위해 Eureka를 사용할 것입니다.

먼저 `application.properties` 파일에 몇 가지 구성을 추가해야 합니다.

```properties
eureka.instance.hostname=localhost
eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
```

다음으로 `@Configuration` 클래스를 만들고 `@EnableEurekaClient`로 주석을 추가합니다.

```java
@Configuration
@EnableEurekaClient
public class EurekaConfig {
}
```

## 마이크로서비스 생성

이제 프로젝트가 설정되었으므로 마이크로서비스 생성을 시작할 수 있습니다. 이 예에서는 인사말을 반환하는 간단한 서비스를 만듭니다.

먼저 `GreetingController`를 만듭니다.

```java
@RestController
public class GreetingController {

    @GetMapping("/greeting")
    public String greeting() {
        return "Hello, world!";
    }
}
```

다음으로 `@Configuration` 클래스를 만들고 `@EnableWebMvc`로 주석을 추가합니다.

```java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {
}
```

마지막으로 `@SpringBootApplication` 클래스를 만듭니다.

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

## 애플리케이션 빌드 및 실행

이제 마이크로서비스가 생성되었으므로 빌드하고 실행할 수 있습니다. 터미널에서 프로젝트 디렉터리로 이동하고 다음 명령을 실행합니다.

```
mvn spring-boot:run
```

다음 출력이 표시되어야 합니다.

```
  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.1.3.RELEASE)

2019-03-29 13:48:41.537  INFO 14073 --- [           main] c.e.a.Application                    : Starting Application on my-macbook-pro.local with PID 14073 (/Users/jdoe/projects/spring-boot-microservices/target/classes started by jdoe in /Users/jdoe/projects/spring-boot-microservices)
2019-03-29 13:48:41.541  INFO 14073 --- [           main] c.e.a.Application                    : No active profile set, falling back to default profiles: default
2019-03-29 13:48:42.591  INFO 14073 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2019-03-29 13:48:42.604  INFO 14073 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2019-03-29 13:48:42.604  INFO 14073 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.17]
2019-03-29 13:48:42.617  INFO 14073 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2019-03-29 13:48:42.618  INFO 14073 --- [           main] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 1735 ms
2019-03-29 13:48:42.791  INFO 14073 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2019-03-29 13:48:42.917  INFO 14073 --- [           main] c.n.eureka.cluster. PeersRefreshScheduler : Starting...
2019-03-29 13:48:42.932  INFO 14073 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2019-03-29 13:48:42.935  INFO 14073 --- [           main] c.e.a.Application                    : Started Application in 1.948 seconds (JVM running for 2.485)
```

이제 http://localhost:8080/greeting에서 서비스에 액세스할 수 있습니다.

## 마이크로서비스 구성

이제 마이크로 서비스가 실행 중이므로 이를 구성해야 합니다. `application.properties` 파일에 `spring.application.name` 속성을 추가하여 시작하겠습니다.

```properties
spring.application.name=greeting-service
```

이 속성은 서비스 이름을 설정합니다. Eureka에서 서비스를 식별하는 데 사용됩니다.

다음으로 `server.port` 속성을 추가합니다.

```properties
server.port=8081
```

이 속성은 서비스가 실행될 포트를 설정합니다. 기본적으로 Spring Boot는 포트 8080에서 실행됩니다. 그러나 `server.port` 속성을 설정하여 이를 변경할 수 있습니다.

## Eureka에 마이크로서비스 등록

이제 마이크로서비스가 구성되었으므로 Eureka에 등록해야 합니다. 이를 위해 `Application` 클래스에 `@EnableEurekaClient` 주석을 추가합니다.

```java
@SpringBootApplication
@EnableEurekaClient
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

이 주석은 Spring에 마이크로서비스를 Eureka에 등록하도록 지시합니다.

## 애플리케이션 빌드 및 실행

이제 마이크로서비스를 Eureka에 등록했으므로 빌드하고 실행할 수 있습니다. 터미널에서 프로젝트 디렉터리로 이동하고 다음 명령을 실행합니다.

```
mvn spring-boot:run
```

다음 출력이 표시되어야 합니다.

```
  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.1.3.RELEASE)

2019-03-29 13:54:45.264  INFO 29122 --- [           main] c.e.a.Application                    : Starting Application on my-macbook-pro.local with PID 29122 (/Users/jdoe/projects/spring-boot-microservices/target/classes started by jdoe in /Users/jdoe/projects/spring-boot-microservices)
2019-03-29 13:54:45.266  INFO 29122 --- [           main] c.e.a.Application                    : No active profile set, falling back to default profiles: default
2019-03-29 13:54:46.318  INFO 29122 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8081 (http)
2019-03-29 13:54:46.330  INFO 29122 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2019-03-29 13:54:46.331  INFO 29122 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.17]
2019-03-29 13:54:46.344  INFO 29122 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2019-03-29 13:54:46.345  INFO 29122 --- [           main] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 1773 ms
2019-03-29 13:54:46.522  INFO 29122 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2019-03-29 13:54:46.643  INFO 29122 --- [           main] c.n.eureka.cluster. PeersRefreshScheduler : Starting...
2019-03-29 13:54:46.657  INFO 29122 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8081 (http) with context path ''
2019-03-29 13:54:46.660  INFO 29122 --- [           main] c.e.a.Application                    : Started Application in 1.965 seconds (JVM running for 2.502)
```

이제 http://localhost:8081/greeting에서 서비스에 액세스할 수 있습니다.

## 마이크로서비스 테스트

이제 마이크로 서비스가 실행 중이므로 테스트할 수 있습니다. 터미널에서 다음 명령을 실행합니다.

```
curl http://localhost:8081/greeting
```

다음 출력이 표시되어야 합니다.

```
Hello, world!
```

## 결론

이 기사에서는 Netflix OSS를 사용하여 Spring Boot 마이크로 서비스를 구축하는 방법을 배웠습니다. 또한 Eureka에 마이크로서비스를 등록하는 방법과 이를 테스트하는 방법도 배웠습니다.