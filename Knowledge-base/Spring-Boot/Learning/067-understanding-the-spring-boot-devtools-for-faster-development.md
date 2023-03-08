---
title: 067: 더 빠른 개발을 위한 Spring Boot DevTools 이해
description: 
published: true
date: 2023-02-03T18:55:33.069Z
tags: 
editor: markdown
dateCreated: 2023-02-03T18:55:28.085Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [067: Understanding the Spring Boot DevTools for Faster Development***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/067-understanding-the-spring-boot-devtools-for-faster-development)
{.links-list}


# 빠른 개발을 위한 Spring Boot DevTools

## Spring Boot DevTools가 무엇인가요?

Spring Boot DevTools는 프로덕션 준비가 된 Spring 애플리케이션을 만드는 과정에서 개발자를 돕는 도구 세트입니다. 이러한 도구는 기존 IDE와 함께 사용하거나 명령줄에서 사용할 수 있습니다. DevTools는 빠른 피드백 루프를 제공하고 개발자가 다음을 수행할 수 있도록 합니다.

- 파일이 변경되면 자동으로 응용 프로그램을 다시 시작합니다.
- 애플리케이션을 다시 시작하지 않고 정적 리소스를 다시 로드합니다.
- 애플리케이션을 다시 시작하지 않고 Java 클래스의 실시간 재로드 제공

## Spring Boot DevTools를 사용하는 이유는 무엇입니까?

Spring Boot DevTools를 사용하는 주된 이유는 Spring 애플리케이션으로 작업할 때 개발자 경험을 개선하기 위해서입니다. DevTools는 일반적인 작업을 자동화하고 빠른 피드백 루프를 제공하여 개발자의 시간을 크게 절약할 수 있습니다.

## Spring Boot DevTools 시작하기

### 1. 프로젝트에 DevTools 종속성을 추가합니다.

첫 번째 단계는 DevTools 종속성을 프로젝트에 추가하는 것입니다. Maven을 사용하는 경우 pom.xml 파일에 다음 종속성을 추가할 수 있습니다.

```xml
<dependencies>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional>
  </dependency>
</dependencies>
```

Gradle을 사용하는 경우 build.gradle 파일에 다음 종속성을 추가할 수 있습니다.

```groovy
dependencies {
  compile("org.springframework.boot:spring-boot-devtools")
}
```

### 2. IDE에서 DevTools 활성화

다음 단계는 IDE에서 DevTools를 활성화하는 것입니다. Eclipse를 사용하는 경우 .project 파일에 다음 행을 추가할 수 있습니다.

```
<buildCommand>
  <name>org.springframework.boot.devtools.eclipse.launch.devtoolsbuilder</name>
  <arguments>
  </arguments>
</buildCommand>
```

IntelliJ IDEA를 사용하는 경우 .iml 파일에 다음 행을 추가할 수 있습니다.

```
<component name="DevTools">
  <configuration>
    <restartOnClassChange>true</restartOnClassChange>
  </configuration>
</component>
```

### 3. 명령줄에서 DevTools 사용

명령줄을 사용하는 경우 다음 명령을 사용하여 DevTools로 애플리케이션을 시작할 수 있습니다.

```
java -jar myapp.jar --spring.devtools.restart.enabled=true
```

## 결론

이 게시물에서는 Spring 애플리케이션으로 작업할 때 개발자 경험을 개선하기 위해 Spring Boot DevTools를 사용하는 방법을 살펴보았습니다. DevTools는 일반적인 작업을 자동화하고 빠른 피드백 루프를 제공하여 개발자의 시간을 크게 절약할 수 있습니다.