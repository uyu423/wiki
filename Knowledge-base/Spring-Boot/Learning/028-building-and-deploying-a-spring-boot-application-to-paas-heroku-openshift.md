---
title: 028: PaaS(Heroku, OpenShift)에 Spring Boot 애플리케이션 구축 및 배포
description: 
published: true
date: 2023-02-03T20:32:44.244Z
tags: 
editor: markdown
dateCreated: 2023-02-03T20:32:39.158Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [028: Building and deploying a Spring Boot application to PaaS (Heroku, OpenShift)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/028-building-and-deploying-a-spring-boot-application-to-paas-heroku-openshift)
{.links-list}


# 028: PaaS(Heroku, OpenShift)에 Spring Boot 애플리케이션 빌드 및 배포

이 게시물에서는 Spring Boot 애플리케이션을 빌드하고 PaaS(Platform as a Service) 공급자에 배포하는 방법을 알아봅니다. 특히 인기 있는 두 PaaS 공급자인 Heroku와 OpenShift에 초점을 맞출 것입니다.

PaaS 제공업체에 Spring Boot 애플리케이션을 빌드하고 배포하는 것은 애플리케이션을 빠르게 시작하고 실행할 수 있는 좋은 방법입니다. PaaS 공급자는 모든 인프라 및 배포 구성을 처리하므로 애플리케이션 개발에 집중할 수 있습니다.

## 전제 조건

시작하기 전에 필요한 몇 가지 사항이 있습니다.

* PaaS 계정. [heroku.com](https://www.heroku.com/)에서 무료 Heroku 계정에 가입할 수 있습니다. OpenShift의 경우 [openshift.com](https://www.openshift.com/)에서 무료 계정에 가입할 수 있습니다.
* 텍스트 편집기 또는 IDE. 이 게시물에서는 [Visual Studio Code](https://code.visualstudio.com/)를 사용하지만 원하는 편집기를 사용할 수 있습니다.
* [JDK 8](https://adoptopenjdk.net/) 이상.
* [Maven](https://maven.apache.org/) 3.3.9 이상.

## 스프링 부트 애플리케이션 만들기

간단한 Spring Boot 애플리케이션을 만드는 것부터 시작하겠습니다. [Spring Initializr](https://start.spring.io/)를 사용하여 프로젝트를 생성합니다.

[Spring Initializr](https://start.spring.io/)로 이동하여 다음 옵션을 선택합니다.

* `Maven 프로젝트` 생성
* `자바 8` 사용
* `스프링 부트 2.2.2` 사용
* 포장: '항아리'
* 유형: `웹`
* 아티팩트: `데모`

`프로젝트 생성`을 클릭하면 `demo.zip` 파일이 다운로드됩니다. zip 파일의 내용을 컴퓨터의 디렉토리에 추출하십시오.

Visual Studio Code에서 프로젝트를 열면 다음 프로젝트 구조가 표시됩니다.

```
demo
├── pom.xml
└── src
    └── main
        ├── java
        │   └── com
        │       └── example
        │           └── demo
        │               └── DemoApplication.java
        └── resources
            └── application.properties
```

`pom.xml` 파일은 Maven 프로젝트 구성 파일입니다. `src/main/java` 디렉토리에는 애플리케이션의 Java 소스 코드가 포함되어 있습니다. `src/main/resources` 디렉토리에는 애플리케이션 구성 파일이 포함되어 있습니다.

`DemoApplication.java` 파일을 열고 다음 `@RestController`를 추가합니다.

```java
package com.example.demo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class DemoApplication {

    @GetMapping("/")
    public String home() {
        return "Hello, world!";
    }

}
```

이 `@RestController`는 `Hello, world!` 문자열을 반환하는 `/` 엔드포인트를 노출합니다.

## 로컬에서 애플리케이션 실행

응용 프로그램을 로컬에서 실행하여 제대로 작동하는지 확인하십시오. 터미널에서 `demo` 디렉터리로 이동하고 다음 명령을 실행합니다.

```
mvn spring-boot:run
```

그러면 로컬 컴퓨터에서 응용 프로그램이 시작됩니다. [http://localhost:8080](http://localhost:8080)에서 애플리케이션에 액세스할 수 있습니다. 'Hello, world!' 문자열이 표시되어야 합니다.

## Heroku에 애플리케이션 배포

이제 작동하는 애플리케이션이 있으므로 Heroku에 배포해 보겠습니다.

Heroku는 배포에 [Git](https://git-scm.com/)을 사용하므로 가장 먼저 해야 할 일은 `demo` 디렉토리에서 Git 저장소를 초기화하는 것입니다. 터미널에서 다음 명령을 실행합니다.

```
git init
git add .
git commit -m "Initial commit"
```

이렇게 하면 Git 리포지토리가 초기화되고 초기 커밋이 수행됩니다.

다음으로 Heroku 애플리케이션을 만들어야 합니다. 터미널에서 다음 명령을 실행합니다.

```
heroku create
```

이렇게 하면 새 Heroku 애플리케이션이 생성되고 Git 리포지토리에 원격이 추가됩니다.

이제 애플리케이션을 Heroku에 배포할 수 있습니다. 터미널에서 다음 명령을 실행합니다.

```
git push heroku master
```

이렇게 하면 코드가 Heroku 원격으로 푸시되고 배포가 트리거됩니다.

배포가 완료되면 Heroku에서 제공하는 URL에서 애플리케이션을 볼 수 있습니다. 'Hello, world!' 문자열이 표시되어야 합니다.

## OpenShift에 애플리케이션 배포

OpenShift는 배포에 [Git](https://git-scm.com/)을 사용하므로 가장 먼저 해야 할 일은 `demo` 디렉토리에서 Git 리포지토리를 초기화하는 것입니다. 터미널에서 다음 명령을 실행합니다.

```
git init
git add .
git commit -m "Initial commit"
```

이렇게 하면 Git 리포지토리가 초기화되고 초기 커밋이 수행됩니다.

다음으로 새 OpenShift 프로젝트를 생성해야 합니다. OpenShift 프로젝트는 리소스의 논리적 그룹입니다. OpenShift 웹 콘솔을 사용하여 프로젝트를 생성합니다.

[OpenShift 웹 콘솔](https://console.openshift.com/)에 로그인하고 `프로젝트 생성`을 클릭합니다. 프로젝트 이름에 `demo`를 입력하고 `만들기`를 클릭합니다.

프로젝트가 생성되면 애플리케이션을 OpenShift에 배포할 수 있습니다. 터미널에서 다음 명령을 실행합니다.

```
git push openshift master
```

이렇게 하면 코드가 OpenShift 원격으로 푸시되고 배포가 트리거됩니다.

배포가 완료되면 OpenShift에서 제공하는 URL에서 애플리케이션을 볼 수 있습니다. 'Hello, world!' 문자열이 표시되어야 합니다.