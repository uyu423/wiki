---
title: 069: 고급 개발을 위한 Spring Boot CLI 사용자 정의
description: 
published: true
date: 2023-02-05T03:32:26.881Z
tags: 
editor: markdown
dateCreated: 2023-02-05T03:32:21.531Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [069: Customizing the Spring Boot CLI for Advanced Development***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/069-customizing-the-spring-boot-cli-for-advanced-development)
{.links-list}


# 고급 개발을 위한 Spring Boot CLI 사용자 지정

Spring Boot CLI는 Spring 애플리케이션을 빠르게 부트스트래핑하기 위한 훌륭한 도구입니다. 이를 통해 웹 서버 없이도 명령줄에서 실행할 수 있는 독립 실행형 Spring 기반 애플리케이션을 만들 수 있습니다.

이 게시물에서는 고급 개발을 위해 Spring Boot CLI를 사용자 지정하는 방법을 살펴보겠습니다. CLI를 설치하는 방법, Spring Boot 애플리케이션을 만들고 실행하는 방법, 고유한 개발 요구 사항에 맞게 CLI를 사용자 지정하는 방법을 다룹니다.

## 스프링 부트 CLI 설치

Spring Boot CLI는 Spring Boot 애플리케이션을 빠르게 만들고 실행하는 데 사용할 수 있는 명령줄 도구입니다. 독립형 실행 JAR 파일 또는 Homebrew 패키지로 사용할 수 있습니다.

Spring Boot CLI를 설치하려면 먼저 Spring Boot 웹 사이트에서 최신 버전의 CLI를 다운로드합니다. 그런 다음 다운로드한 파일의 압축을 풀고 `PATH`에 `spring-boot-cli/bin` 디렉토리를 추가합니다.

또는 Homebrew를 사용하는 경우 다음 명령을 실행하여 Spring Boot CLI를 설치할 수 있습니다.

```
$ brew tap pivotal/tap
$ brew install springboot
```

## 스프링 부트 애플리케이션 만들기

이제 Spring Boot CLI를 설치했으므로 간단한 Spring Boot 애플리케이션을 만들어 보겠습니다. 프로젝트를 위한 새 디렉터리를 만드는 것으로 시작하겠습니다.

```
$ mkdir my-app
$ cd my-app
```

다음으로 프로젝트 디렉터리에 `application.properties`라는 새 파일을 만듭니다. 이 파일에는 Spring Boot 애플리케이션의 구성이 포함됩니다. 애플리케이션이 실행될 때 Spring Boot 배너가 표시되지 않도록 `spring.main.banner-mode` 속성을 `off`로 설정합니다.

```
spring.main.banner-mode=off
```

이제 Spring Boot 애플리케이션을 만들 수 있습니다. `spring` 명령을 사용하여 새로운 `@SpringBootApplication` 클래스를 만듭니다.

```
$ spring init -n com.example.myapp -d web my-app.jar
```

이렇게 하면 프로젝트 디렉토리에 새로운 `my-app.jar` 파일이 생성됩니다. 다음 명령을 실행하여 애플리케이션을 실행할 수 있습니다.

```
$ java -jar my-app.jar
```

애플리케이션이 시작되고 `http://localhost:8080`에서 액세스할 수 있습니다.

## 스프링 부트 CLI 커스터마이징

Spring Boot CLI는 동작을 사용자 지정하기 위한 여러 옵션을 제공합니다. 이러한 옵션은 명령줄 또는 `spring` 구성 파일에서 지정할 수 있습니다.

`spring` 구성 파일은 Spring Boot CLI가 시작될 때 읽는 YAML 파일입니다. 이 파일은 기본 프로젝트 디렉토리 및 기본 패키지 이름과 같은 `spring` 명령에 대한 옵션을 지정하는 데 사용할 수 있습니다.

`spring` 구성 파일을 만들려면 홈 디렉터리에 `.spring-configuration.yaml`이라는 새 파일을 만듭니다. 이 파일의 내용은 시작 시 Spring Boot CLI에서 읽습니다.

다음은 `spring` 구성 파일의 예입니다.

```yaml
spring:
  project:
    default-project-dir: ~/projects
  package:
    default-package-name: com.example
```

이 파일은 기본 프로젝트 디렉토리를 `~/projects`로 설정하고 기본 패키지 이름을 `com.example`로 설정합니다.

이제 새 Spring Boot 애플리케이션을 만들 때 `spring` 명령은 다음 기본값을 사용합니다.

```
$ spring init my-app
```

그러면 `com.example` 패키지 이름을 사용하여 `~/projects/my-app` 디렉토리에 새로운 Spring Boot 애플리케이션이 생성됩니다.

`spring` 명령줄에서 옵션을 지정할 수도 있습니다. 예를 들어 `--project-dir` 옵션을 사용하여 프로젝트 디렉토리를 설정할 수 있습니다.

```
$ spring init --project-dir=~/my-app my-app
```

그러면 `~/my-app` 디렉토리에 새로운 Spring Boot 애플리케이션이 생성됩니다.

## 결론

이 게시물에서는 고급 개발을 위해 Spring Boot CLI를 사용자 정의하는 방법을 살펴보았습니다. CLI를 설치하는 방법, Spring Boot 애플리케이션을 만들고 실행하는 방법, 고유한 개발 요구 사항에 맞게 CLI를 사용자 지정하는 방법을 다루었습니다.