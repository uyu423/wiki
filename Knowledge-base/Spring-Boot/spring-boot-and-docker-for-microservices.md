---
title: 마이크로 서비스용 Spring Boot 및 Docker
description: 
published: true
date: 2023-02-08T01:32:41.759Z
tags: 
editor: markdown
dateCreated: 2023-02-08T01:32:40.077Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot and Docker for Microservices***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-docker-for-microservices)
{.links-list}


# 소개

개발자들은 확장 가능한 애플리케이션을 구축하는 방법으로 마이크로서비스로 전환하고 있습니다. 마이크로서비스는 대규모 애플리케이션이 작고 독립적인 서비스 모음으로 구축되는 소프트웨어 아키텍처 유형입니다. 이 접근 방식에는 서비스를 독립적으로 업데이트하고 배포하는 기능과 서비스를 수평으로 확장하는 기능을 포함하여 많은 이점이 있습니다.

마이크로서비스는 많은 이점을 제공하지만 관리하기 복잡할 수도 있습니다. 바로 여기에서 Docker가 등장합니다. Docker는 마이크로서비스를 쉽게 패키징, 배포 및 관리할 수 있게 해주는 컨테이너화 플랫폼입니다.

이 기사에서는 Docker 및 Spring Boot를 사용하여 마이크로 서비스를 개발하고 배포하는 방법을 살펴보겠습니다. 간단한 예제로 시작한 다음 Spring Boot 및 Docker가 마이크로 서비스 개발을 위해 제공하는 고급 기능 중 일부를 살펴보겠습니다.

# 스프링부트란?

Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 응용 프로그램을 쉽게 만들 수 있는 Java 기반 프레임워크입니다. 다음을 포함하여 마이크로서비스를 쉽게 개발하고 배포할 수 있는 다양한 기능을 제공합니다.

- 임베디드 Tomcat: Spring Boot는 임베디드 Tomcat 서버와 함께 제공되어 애플리케이션을 독립 실행형 Java 애플리케이션으로 쉽게 실행할 수 있습니다.
- 종속성 관리: Spring Boot는 자동으로 종속성을 관리합니다. 이는 종속성을 수동으로 관리하는 것에 대해 걱정할 필요가 없기 때문에 마이크로서비스를 개발할 때 엄청난 시간을 절약할 수 있습니다.
- 구성: Spring Boot는 애플리케이션을 구성하는 다양한 방법을 제공합니다. 표준 Java 속성 파일, YAML 파일 또는 환경 변수를 사용할 수 있습니다. 이를 통해 다양한 환경(개발, 프로덕션 등)에 대해 애플리케이션을 쉽게 구성할 수 있습니다.

# 도커란?

Docker는 애플리케이션을 쉽게 패키징, 배포 및 관리할 수 있는 컨테이너화 플랫폼입니다. Docker 컨테이너는 애플리케이션을 쉽게 패키징하고 배포할 수 있는 독립적이고 격리된 환경입니다.

Docker 컨테이너는 가볍고 휴대가 간편하여 마이크로서비스에 이상적입니다. 또한 플랫폼에 구애받지 않는다는 추가 이점이 있으므로 Docker를 지원하는 모든 플랫폼에 배포할 수 있습니다.

# 스프링부트와 도커로 마이크로서비스 개발하기

이 섹션에서는 Spring Boot 및 Docker를 사용하여 간단한 마이크로 서비스를 개발하고 배포하는 방법을 살펴보겠습니다.

# 프로젝트 생성

먼저 새로운 Spring Boot 프로젝트를 생성해야 합니다. Spring Initializr를 사용하여 이를 수행할 수 있습니다. Initializr는 Spring Boot 프로젝트를 쉽게 만들 수 있는 웹 기반 도구입니다.

간단한 Maven 프로젝트를 만드는 것으로 시작하겠습니다. 프로젝트 이름을 "hello-world"로 지정하고 최신 버전의 Spring Boot(작성 당시 2.0.4)를 사용합니다. "Web" 및 "Actuator" 종속성도 추가할 것입니다. 예를 들어 이 두 가지가 모두 필요하기 때문입니다.

프로젝트가 생성되면 `pom.xml` 파일에 몇 가지 종속성을 추가해야 합니다.

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

# 서비스 만들기

이제 프로젝트가 설정되었으므로 마이크로서비스를 만들 수 있습니다. 간단한 `HelloController`를 생성하여 시작하겠습니다.

```java
@RestController
public class HelloController {

    @RequestMapping("/")
    public String index() {
        return "Hello, world!";
    }
}
```

이 컨트롤러는 `/` 경로에 매핑되며 "Hello, world!"라는 문자열을 반환합니다. 부를 때.

# Dockerfile 추가

이제 마이크로 서비스가 생성되었으므로 프로젝트에 `Dockerfile`을 추가해야 합니다. `Dockerfile`은 Docker 이미지를 빌드하기 위한 지침이 포함된 텍스트 파일입니다.

우리의 `Dockerfile`은 매우 간단합니다. 사용하려는 기본 이미지를 지정하여 시작하겠습니다. 이 예에서는 `openjdk:8-jdk-alpine` 이미지를 사용합니다. 이 이미지에는 최소 버전의 Alpine Linux 및 OpenJDK 8 JDK가 포함되어 있습니다.

다음으로 애플리케이션에 필요한 종속성을 설치하기 위해 몇 줄을 추가합니다.

```dockerfile
FROM openjdk:8-jdk-alpine

RUN apk add --no-cache curl
```

`curl` 명령줄 도구를 설치하기 위해 `apk` 명령을 사용하고 있습니다. `curl`은 나중에 응용 프로그램이 실행 중인지 테스트하도록 요청하는 데 사용됩니다.

이제 몇 줄을 추가하여 애플리케이션 jar 파일을 이미지에 복사하고 컨테이너가 시작될 때 실행해야 하는 명령을 지정합니다.

```dockerfile
FROM openjdk:8-jdk-alpine

RUN apk add --no-cache curl

COPY target/hello-world-0.0.1-SNAPSHOT.jar /hello-world.jar

ENTRYPOINT ["java", "-jar", "/hello-world.jar"]
```

# Docker 이미지 빌드

이제 `Dockerfile`이 있으므로 Docker 이미지를 빌드할 수 있습니다. `docker build` 명령을 사용하여 이미지를 빌드합니다. 이미지에 "hello-world"라는 이름을 지정합니다.

```
$ docker build -t hello-world .
```

# 컨테이너 실행

이제 Docker 이미지가 있으므로 컨테이너를 실행할 수 있습니다. `docker run` 명령을 사용하여 컨테이너를 실행합니다. 또한 컨테이너를 실행할 포트를 지정합니다. 이 예에서는 포트 8080을 사용합니다.

```
$ docker run -p 8080:8080 hello-world
```

# 애플리케이션 테스트

이제 컨테이너가 실행 중이므로 애플리케이션을 테스트할 수 있습니다. 애플리케이션에 요청을 하기 위해 `curl` 명령을 사용할 것입니다:

```
$ curl http://localhost:8080

Hello, world!
```

# 결론

이 기사에서는 Spring Boot 및 Docker를 사용하여 마이크로 서비스를 개발하고 배포하는 방법을 살펴보았습니다. 간단한 마이크로서비스를 만드는 방법, 서비스용 Docker 이미지를 빌드하는 방법 및 Docker 컨테이너에서 서비스를 실행하는 방법을 살펴보았습니다.