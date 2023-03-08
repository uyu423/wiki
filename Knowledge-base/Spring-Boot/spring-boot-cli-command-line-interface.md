---
title: Spring Boot CLI 명령줄 인터페이스
description: 
published: true
date: 2023-02-17T18:15:01.536Z
tags: 
editor: markdown
dateCreated: 2023-01-30T22:23:38.606Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Spring Boot CLI Command Line Interface***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-cli-command-line-interface)
{.links-list}



# Spring Boot CLI 명령줄 인터페이스

Spring Boot CLI는 Spring 기반 애플리케이션을 빠르게 빌드하는 데 사용되는 명령줄 인터페이스입니다. 필요한 모든 종속성을 갖춘 Spring 프로젝트를 생성하는 빠른 방법을 제공합니다.

Spring Boot CLI는 Spring을 빠르게 시작하고 실행하려는 개발자에게 중요한 도구입니다. 이 기사에서는 Spring Boot CLI를 사용하여 Spring 프로젝트를 빠르게 생성하는 방법을 살펴보겠습니다. 또한 Spring Boot CLI가 제공하는 일부 기능에 대해서도 설명합니다.

## 시작하기

Spring Boot CLI를 사용하려면 다음을 설치해야 합니다.

* 자바 8 이상
* 아파치 메이븐 3.3.9 이상

다음 명령을 실행하여 설치되어 있는지 확인할 수 있습니다.

```
java -version
mvn -version
```

설치되어 있지 않은 경우 [여기](https://spring.io/guides/gs/getting-started-maven/)의 지침을 따를 수 있습니다.

설치가 완료되면 [이 링크](https://repo.spring.io/release/org/springframework/boot/spring-boot-cli/2.3.1.RELEASE/를 방문하여 Spring Boot CLI를 다운로드할 수 있습니다. spring-boot-cli-2.3.1.RELEASE-bin.zip).

Spring Boot CLI를 다운로드했으면 압축을 풀고 `bin` 디렉토리를 `PATH`에 추가해야 합니다. 이렇게 하면 모든 디렉토리에서 `spring` 명령을 실행할 수 있습니다.

## 스프링 프로젝트 생성

이제 Spring Boot CLI를 설치했으므로 이를 사용하여 Spring 프로젝트를 생성해 보겠습니다. [Web](https://start.spring.io/#dependencies=web) 및 [JPA](https://start.spring.io/#dependencies=data-jpa)를 사용하는 프로젝트를 생성합니다. 종속성.

이를 위해 `spring init` 명령을 사용합니다. 이 명령은 지정된 종속성을 사용하여 Spring 프로젝트를 생성합니다. `-d` 플래그는 프로젝트에 포함하려는 종속성을 지정하는 데 사용됩니다. 우리의 경우 웹 및 JPA 종속성을 포함하려고 합니다. 또한 [bootstrap](https://getbootstrap.com/) 종속성을 사용하고자 함을 나타내기 위해 `-b` 플래그를 지정합니다.

```
spring init -d=web,data-jpa -b
```

그러면 다음 구조로 `my-project`라는 디렉토리가 생성됩니다.

```
my-project
├── pom.xml
└── src
    ├── main
    │   ├── java
    │   │   └── com
    │   │       └── example
    │   │           └── myproject
    │   │               └── MyprojectApplication.java
    │   └── resources
    │       └── application.properties
    └── test
        └── java
            └── com
                └── example
                    └── myproject
                        └── MyprojectApplicationTests.java
```

`pom.xml` 파일에는 프로젝트의 종속성이 포함되어 있습니다. `src/main/java` 디렉토리에는 프로젝트의 Java 소스 코드가 포함되어 있습니다. `src/test/java` 디렉토리에는 프로젝트의 테스트가 포함되어 있습니다. `src/main/resources` 디렉터리에는 속성 파일과 같은 프로젝트 리소스가 포함되어 있습니다.

## 애플리케이션 실행

이제 Spring 프로젝트가 생겼으니 실행하여 무엇을 하는지 살펴보겠습니다. 이를 위해 `spring run` 명령을 사용합니다. 이 명령은 애플리케이션을 컴파일하고 실행합니다.

```
spring run src/main/java/com/example/myproject/MyprojectApplication.java
```

이렇게 하면 포트 8080에서 애플리케이션이 시작됩니다. [http://localhost:8080](http://localhost:8080)을 방문하여 애플리케이션을 볼 수 있습니다.

## SpringBoot CLI 명령

`spring run` 명령은 애플리케이션을 빠르게 실행하는 데 유용하지만 Spring Boot CLI는 다양한 작업에 사용할 수 있는 다른 많은 명령을 제공합니다. 아래에서 가장 유용한 몇 가지 명령에 대해 간략하게 설명하겠습니다.

### `스프링 부트`

`spring boot` 명령을 사용하여 새로운 Spring Boot 애플리케이션을 생성할 수 있습니다. 이 명령은 지정된 종속성을 가진 새 프로젝트를 생성합니다. 이것은 이전 섹션에서 프로젝트를 생성하는 데 사용한 것과 동일한 명령입니다.

### `봄맞이 대청소`

`spring clean` 명령을 사용하여 프로젝트의 빌드 디렉토리를 정리할 수 있습니다. 이는 필요하지 않은 컴파일된 파일이나 기타 아티팩트를 제거하려는 경우에 유용합니다.

### `스프링 런`

`spring run` 명령을 사용하여 애플리케이션을 컴파일하고 실행할 수 있습니다. 이것은 이전 섹션에서 애플리케이션을 실행하는 데 사용한 것과 동일한 명령입니다.

### `스프링 테스트`

`spring test` 명령을 사용하여 프로젝트의 테스트를 실행할 수 있습니다. 이는 응용 프로그램이 올바르게 작동하는지 확인하는 데 유용합니다.

### `스프링 항아리`

`spring jar` 명령을 사용하여 애플리케이션을 JAR 파일로 패키징할 수 있습니다. 이는 응용 프로그램을 서버에 배포하는 데 유용합니다.

### `봄의 전쟁`

`spring war` 명령을 사용하여 애플리케이션을 WAR 파일로 패키징할 수 있습니다. 이는 응용 프로그램을 서버에 배포하는 데 유용합니다.

### `봄 도움말`

`spring help` 명령을 사용하여 사용 가능한 모든 명령 목록을 표시할 수 있습니다. 이것은 사용 가능한 모든 명령에 대한 빠른 개요를 얻는 데 유용합니다.

## 결론

이 기사에서는 Spring Boot CLI를 사용하여 Spring 기반 애플리케이션을 빠르게 생성하는 방법에 대해 설명했습니다. 또한 Spring Boot CLI가 제공하는 가장 유용한 명령 중 일부를 다루었습니다.