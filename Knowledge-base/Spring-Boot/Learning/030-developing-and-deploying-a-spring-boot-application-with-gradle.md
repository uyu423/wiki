---
title: 030: Gradle로 Spring Boot 애플리케이션 개발 및 배포
description: 
published: true
date: 2023-02-03T22:32:28.781Z
tags: 
editor: markdown
dateCreated: 2023-02-03T22:32:27.163Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [030: Developing and deploying a Spring Boot application with Gradle***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/030-developing-and-deploying-a-spring-boot-application-with-gradle)
{.links-list}


# 030: Gradle로 Spring Boot 애플리케이션 개발 및 배포

Spring Boot는 웹 애플리케이션 개발에 널리 사용되는 Java 프레임워크입니다. "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다.

이 게시물에서는 Gradle을 사용하여 Spring Boot 애플리케이션을 개발하고 배포하는 방법을 살펴보겠습니다. 먼저 프로젝트를 설정한 다음 코드를 작성하고 jar 파일로 패키징합니다. 마지막으로 애플리케이션을 서버에 배포합니다.

## 프로젝트 설정

가장 먼저 해야 할 일은 프로젝트를 설정하는 것입니다. 프로젝트를 위한 새 디렉토리를 생성하고 Gradle 빌드 스크립트를 초기화합니다.

```
$ mkdir my-spring-boot-app
$ cd my-spring-boot-app
$ gradle init
```

다음으로 빌드 스크립트에 Spring Boot 종속성을 추가해야 합니다. `build.gradle` 파일에 다음 행을 추가하여 이를 수행합니다.

```
dependencies {
    compile 'org.springframework.boot:spring-boot-starter-web'
}
```

## 코드 작성

이제 프로젝트가 설정되었으므로 코드 작성을 시작할 수 있습니다. "Hello, world!"를 출력하는 간단한 Spring Boot 애플리케이션을 만들겠습니다.

먼저 `src/main/java` 디렉토리에 `HelloWorldController.java`라는 파일을 만듭니다. 이 파일에는 컨트롤러가 포함됩니다.

```java
package com.example.myapp;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloWorldController {

    @RequestMapping("/")
    public String index() {
        return "Hello, world!";
    }

}
```

다음으로 `src/main/java` 디렉토리에 `Application.java`라는 파일을 생성합니다. 이 파일에는 기본 애플리케이션 클래스가 포함됩니다.

```java
package com.example.myapp;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

## 애플리케이션 패키징

이제 코드가 작성되었으므로 jar 파일로 패키징해야 합니다. `gradle build` 명령을 실행하여 이를 수행할 수 있습니다. 그러면 `build/libs` 디렉토리에 jar 파일이 생성됩니다.

## 애플리케이션 배포

이제 애플리케이션이 패키징되었으므로 서버에 배포할 수 있습니다. `java -jar` 명령을 사용하여 jar 파일을 실행합니다.

```
$ java -jar build/libs/my-spring-boot-app.jar
```

애플리케이션은 포트 8080에서 시작됩니다. 브라우저에서 http://localhost:8080으로 이동하여 액세스할 수 있습니다.

## 결론

이 게시물에서는 Gradle을 사용하여 Spring Boot 애플리케이션을 개발하고 배포하는 방법을 살펴보았습니다. 프로젝트를 설정하고, 코드를 작성하고, jar 파일로 패키징하고, 서버에 배포했습니다.