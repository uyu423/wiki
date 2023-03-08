---
title: 077: Docker를 사용하여 Spring Boot 애플리케이션 배포
description: 
published: true
date: 2023-02-05T08:32:53.716Z
tags: 
editor: markdown
dateCreated: 2023-02-05T08:32:52.059Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [077: Deploying a Spring Boot Application with Docker***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/077-deploying-a-spring-boot-application-with-docker)
{.links-list}


## 소개

Docker는 애플리케이션을 모든 종속성과 함께 패키징하고 하나의 단위로 배송할 수 있게 해주는 컨테이너화 기술입니다. 이를 통해 Docker를 지원하는 모든 호스트에서 애플리케이션을 쉽게 배포하고 실행할 수 있습니다.

이 게시물에서는 Docker를 사용하여 Spring Boot 애플리케이션을 배포하는 방법을 배웁니다. 간단한 Spring Boot 애플리케이션을 빌드하고 Docker 이미지로 패키징하는 것으로 시작하겠습니다. 그런 다음 로컬 Docker 호스트에서 Docker 이미지를 실행합니다. 마지막으로 Docker 이미지를 Docker 레지스트리로 푸시하여 프로덕션 서버에 배포할 수 있습니다.

## 전제 조건

이 게시물을 따라하려면 다음이 필요합니다.

- 텍스트 편집기
- JDK 8 이상
- 메이븐 3.0 이상
- 도커 CE 18.03 이상

## 스프링 부트 애플리케이션 빌드

간단한 Spring Boot 애플리케이션을 빌드하는 것으로 시작하겠습니다. 애플리케이션에는 국가 목록을 반환하는 단일 REST 엔드포인트가 있습니다.

먼저 프로젝트의 새 디렉터리를 만들고 해당 디렉터리로 변경합니다. 그런 다음 다음 내용으로 `pom.xml`이라는 파일을 만듭니다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>spring-boot-docker-example</artifactId>
    <version>1.0-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.4.RELEASE</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
```

프로젝트의 Maven `pom.xml` 파일입니다. 종속성을 관리하고 빌드를 구성하는 편리한 방법을 제공하는 Spring Boot 스타터 부모를 사용하고 있습니다. 또한 웹 애플리케이션 빌드를 위한 종속성을 포함하는 Spring Boot 스타터 웹 종속성을 사용하고 있습니다.

다음으로 다음 내용으로 `src/main/java/com/example/springboot/Application.java`라는 파일을 만듭니다.

```java
package com.example.springboot;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

이것은 기본 응용 프로그램 클래스입니다. 자동 구성 및 구성 요소 검색을 활성화하기 위해 `@SpringBootApplication` 주석을 사용합니다.

다음으로 다음 내용으로 `src/main/java/com/example/springboot/controller/CountryController.java`라는 파일을 만듭니다.

```java
package com.example.springboot.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.Arrays;
import java.util.List;

@RestController
public class CountryController {

    @GetMapping("/countries")
    public List<String> getCountries() {
        return Arrays.asList("Australia", "Canada", "France", "Germany", "India", "Japan", "United Kingdom", "United States");
    }

}
```

이것은 `/countries` 엔드포인트에 대한 컨트롤러입니다. 국가 목록을 반환합니다.

이제 애플리케이션이 완료되었으므로 Docker 이미지로 패키징할 수 있습니다.

## 애플리케이션을 Docker 이미지로 패키징

Maven을 사용하여 애플리케이션을 Docker 이미지로 패키징합니다. 먼저 `<plugin>`을 `pom.xml` 파일에 추가해야 합니다.

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
        <plugin>
            <groupId>com.spotify</groupId>
            <artifactId>dockerfile-maven-plugin</artifactId>
            <version>1.3.6</version>
            <configuration>
                <repository>${docker.repository}</repository>
                <tag>${project.version}</tag>
                <buildArgs>
                    <JAR_FILE>target/${project.build.finalName}.jar</JAR_FILE>
                </buildArgs>
            </configuration>
        </plugin>
    </plugins>
</build>
```

이렇게 하면 애플리케이션을 Docker 이미지로 패키징하는 Spotify Dockerfile Maven 플러그인이 추가됩니다. 또한 `${project.version}`을 Docker 이미지 태그로 사용하고 `${project.build.finalName}.jar` 파일을 빌드 인수로 전달하도록 플러그인을 구성하고 있습니다.

다음으로 다음 내용으로 `src/main/docker/Dockerfile`이라는 파일을 만듭니다.

```dockerfile
FROM openjdk:8-jdk-alpine
VOLUME /tmp
ARG JAR_FILE
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
```

이것은 이미지의 Dockerfile입니다. OpenJDK 8 Alpine Docker 이미지를 기본 이미지로 사용합니다. 또한 `${JAR_FILE}`을 `app.jar` 파일에 복사하고 이를 이미지의 진입점으로 설정합니다.

이제 다음 명령을 실행하여 애플리케이션을 Docker 이미지로 패키징할 수 있습니다.

```
$ mvn package docker:build
```

그러면 애플리케이션이 JAR 파일로 패키징되고 Docker 이미지가 빌드됩니다. Docker 이미지에는 `${project.version}` 태그가 지정되며 이 경우에는 `1.0-SNAPSHOT`입니다.

## 도커 이미지 실행

이제 Docker 이미지가 있으므로 로컬 Docker 호스트에서 실행할 수 있습니다. 먼저 Docker 호스트를 시작해야 합니다. Docker Machine을 사용하는 경우 다음 명령을 사용하여 Docker 호스트를 시작할 수 있습니다.

```
$ docker-machine create --driver virtualbox default
```

이렇게 하면 이름이 `default`인 Docker 호스트가 생성됩니다.

다음으로 Docker 호스트에 액세스할 수 있도록 몇 가지 환경 변수를 설정해야 합니다.

```
$ eval $(docker-machine env default)
```

이제 다음 명령을 사용하여 Docker 이미지를 실행할 수 있습니다.

```
$ docker run -d -p 8080:8080 spring-boot-docker-example:1.0-SNAPSHOT
```

분리 모드에서 Docker 이미지를 실행하고 Docker 호스트의 포트 '8080'을 컨테이너의 포트 '8080'에 매핑합니다.

다음 명령을 사용하여 컨테이너가 실행 중인지 확인할 수 있습니다.

```
$ docker ps
```

다음과 같은 출력이 표시됩니다.

```
CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
e9c4b7a4d4f4        spring-boot-docker-example:1.0   "java -Djava.securit…"   3 seconds ago       Up 2 seconds        0.0.0.0:8080->8080/tcp   stoic_ardinghelli
```

이제 웹 브라우저에서 http://localhost:8080을 열어 애플리케이션에 액세스할 수 있습니다. 다음과 같은 페이지가 표시됩니다.

![스프링부트 도커 예시](https://i.imgur.com/hm4Tv0b.png)

## Docker 이미지를 레지스트리로 푸시

이제 작동하는 Docker 이미지가 있으므로 이를 Docker 레지스트리에 푸시하여 프로덕션 서버에 배포할 수 있습니다.

먼저 Docker 레지스트리를 만들어야 합니다. 이 예제에서는 Docker 허브를 사용합니다. Docker Hub 계정에 가입한 다음 새 리포지토리를 만듭니다. 저장소를 `spring-boot-docker-example`이라고 합니다.

리포지토리가 생성되면 다음 명령을 사용하여 Docker 이미지를 푸시할 수 있습니다.

```
$ docker push spring-boot-docker-example:1.0-SNAPSHOT
```

그러면 `spring-boot-docker-example:1.0-SNAPSHOT` 이미지가 Docker Hub의 `spring-boot-docker-example` 리포지토리로 푸시됩니다.

## 결론

이 게시물에서는 Docker를 사용하여 Spring Boot 애플리케이션을 배포하는 방법을 배웠습니다. 우리는 간단한 Spring Boot 애플리케이션을 빌드하고 이를 Docker 이미지로 패키징하는 것으로 시작했습니다. 그런 다음 로컬 Docker 호스트에서 Docker 이미지를 실행했습니다. 마지막으로 Docker 이미지를 Docker 레지스트리로 푸시하여 프로덕션 서버에 배포할 수 있도록 했습니다.