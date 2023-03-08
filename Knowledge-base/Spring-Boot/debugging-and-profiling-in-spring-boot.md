---
title: Spring Boot에서 디버깅 및 프로파일링
description: 
published: true
date: 2023-02-17T18:02:55.976Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:24:04.993Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Debugging and Profiling in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/debugging-and-profiling-in-spring-boot)
{.links-list}


# Spring Boot에서 디버깅 및 프로파일링

소프트웨어 개발은 어렵고 시간이 많이 소요될 수 있습니다. 프로세스를 최대한 원활하게 만드는 데 도움이 되는 도구를 갖추는 것이 중요합니다. 이 기사에서는 디버깅과 프로파일링이라는 두 가지 도구를 살펴보겠습니다.

디버깅은 소프트웨어의 오류를 찾아 수정하는 프로세스입니다. 코드와 데이터 모두에서 오류를 찾는 데 사용할 수 있습니다. 프로파일링은 소프트웨어를 최적화하는 데 사용할 수 있는 기술입니다. 병목 현상을 찾고 성능을 개선하는 데 사용할 수 있습니다.

Spring Boot는 웹 애플리케이션 개발에 널리 사용되는 프레임워크입니다. "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다. 또한 디버깅 및 프로파일링에 도움이 되는 다양한 도구를 제공합니다.

## 스프링 부트 애플리케이션 디버깅

Spring Boot 애플리케이션을 디버깅하는 몇 가지 방법이 있습니다. 이 섹션에서는 가장 인기 있는 두 가지인 spring-boot-devtools 모듈 사용과 원격 디버깅 사용을 살펴보겠습니다.

### spring-boot-devtools 모듈 사용

spring-boot-devtools 모듈을 사용하여 디버깅 환경을 개선할 수 있습니다. 자동 재시작, 라이브 재로드 및 원격 디버깅과 같은 기능을 제공합니다.

spring-boot-devtools 모듈을 사용하려면 프로젝트에 의존성으로 추가하세요:

```xml
<dependencies>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
  </dependency>
</dependencies>
```

이 작업을 완료하면 application.properties 파일에 다음 속성을 추가하여 모듈의 기능을 활성화할 수 있습니다.

```
spring.devtools.restart.enabled=true
spring.devtools.livereload.enabled=true
spring.devtools.remote.debug.local=false
```

첫 번째 속성인 spring.devtools.restart.enabled는 자동 재시작 기능을 활성화합니다. 이 기능은 클래스 경로의 파일이 변경되면 애플리케이션을 자동으로 다시 시작합니다. 두 번째 속성인 spring.devtools.livereload.enabled는 실시간 재로드 기능을 활성화합니다. 이 기능은 애플리케이션을 다시 시작하지 않고 변경된 리소스를 다시 로드합니다.

세 번째 속성인 spring.devtools.remote.debug.local은 원격 디버깅을 활성화합니다. 이 기능을 사용하면 원격 IDE에서 애플리케이션을 디버그할 수 있습니다. 이 기능을 사용하려면 속성 값을 true로 설정하고 다음 속성을 추가해야 합니다.

```
spring.devtools.remote.debug.port=8000
```

이 속성은 원격 디버깅에 사용될 포트를 설정합니다. 이 작업을 완료하면 디버그 모드에서 애플리케이션을 시작할 수 있습니다. IntelliJ IDEA에서는 실행 -> 구성 편집으로 이동하여 이 작업을 수행할 수 있습니다. 구성 편집 대화 상자에서 + 버튼을 클릭하고 원격을 선택합니다. 원격 구성 대화 상자에서 포트를 8000으로 설정하고 적용을 클릭합니다.

이제 IntelliJ IDEA에서 애플리케이션을 디버그할 수 있습니다. 이렇게 하려면 디버그 도구 창을 열고 + 버튼을 클릭합니다. 구성 추가 대화 상자에서 원격을 선택하고 확인을 클릭하십시오. 원격 구성 대화 상자에서 포트를 8000으로 설정하고 디버그를 클릭합니다.

### 원격 디버깅 사용

다른 IDE를 사용하는 경우 원격 디버깅을 계속 사용할 수 있습니다. 이렇게 하려면 디버그 모드에서 응용 프로그램을 시작하고 디버깅에 사용할 포트를 지정해야 합니다. IntelliJ IDEA에서는 실행 -> 구성 편집으로 이동하여 이 작업을 수행할 수 있습니다. 구성 편집 대화 상자에서 + 버튼을 클릭하고 원격을 선택합니다. 원격 구성 대화 상자에서 포트를 8000으로 설정하고 적용을 클릭합니다.

이제 IntelliJ IDEA에서 애플리케이션을 디버그할 수 있습니다. 이렇게 하려면 디버그 도구 창을 열고 + 버튼을 클릭합니다. 구성 추가 대화 상자에서 원격을 선택하고 확인을 클릭합니다. 원격 구성 대화 상자에서 포트를 8000으로 설정하고 디버그를 클릭합니다.

## 스프링 부트 애플리케이션 프로파일링

프로파일링은 소프트웨어를 최적화하는 데 사용할 수 있는 기술입니다. 병목 현상을 찾고 성능을 개선하는 데 사용할 수 있습니다. Spring Boot 애플리케이션을 프로파일링하는 몇 가지 방법이 있습니다. 이 섹션에서는 가장 인기 있는 두 가지 방법인 Spring Boot Actuator 사용과 JProfiler 사용에 대해 살펴보겠습니다.

### 스프링 부트 액추에이터 사용

Spring Boot Actuator는 Spring Boot 애플리케이션을 모니터링하고 관리하는 데 사용할 수 있는 도구 세트입니다. 웹 인터페이스, 애플리케이션 모니터링 및 관리를 위한 엔드포인트, 프로파일링 정보 수집을 위한 도구 세트를 비롯한 다양한 기능을 제공합니다.

Spring Boot Actuator를 사용하려면 프로젝트에 종속 항목으로 추가하세요.

```xml
<dependencies>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
  </dependency>
</dependencies>
```

완료하면 http://localhost:8080/actuator로 이동하여 웹 인터페이스에 액세스할 수 있습니다. 웹 인터페이스는 애플리케이션을 모니터링하고 관리하기 위한 다양한 도구를 제공합니다. 또한 프로파일링 정보를 수집하기 위한 일련의 도구를 제공합니다.

프로파일링 도구를 사용하려면 application.properties 파일에 다음 속성을 추가해야 합니다.

```
management.endpoints.web.exposure.include=*
```

이 속성은 액추에이터의 모든 끝점을 노출합니다. 완료하면 /profiler 엔드포인트에 액세스할 수 있습니다. 이 엔드포인트를 사용하면 프로파일링 정보를 수집하고 볼 수 있습니다.

### JProfiler 사용

JProfiler는 Java 프로파일링 도구입니다. 스레드 정보, 메모리 정보, SQL 정보 등 다양한 유형의 정보를 수집하는 데 사용할 수 있습니다. 또한 호출 트리 보기, 핫스팟 보기 및 라이브 메모리 보기를 포함하여 다양한 보기를 제공합니다.

JProfiler를 사용하려면 JProfiler를 설치하고 프로젝트에 종속 항목으로 추가해야 합니다. JProfiler 웹사이트로 이동하여 최신 버전을 다운로드하면 됩니다. 이 작업을 완료하면 프로젝트에 종속 항목으로 추가할 수 있습니다.

```xml
<dependencies>
  <dependency>
    <groupId>org.jprofiler</groupId>
    <artifactId>jprofiler</artifactId>
    <version>11.0.2</version>
  </dependency>
</dependencies>
```

완료하면 프로필 모드에서 애플리케이션을 시작할 수 있습니다. IntelliJ IDEA에서는 실행 -> 구성 편집으로 이동하여 이 작업을 수행할 수 있습니다. 구성 편집 대화 상자에서 + 버튼을 클릭하고 프로필을 선택합니다. 프로필 구성 대화 상자에서 JProfiler 옵션을 선택하고 적용을 클릭합니다.

이제 IntelliJ IDEA에서 애플리케이션을 프로파일링할 수 있습니다. 이렇게 하려면 프로파일 도구 창을 열고 사용하려는 프로파일링 세션을 선택하십시오. 세션에서 수집할 데이터와 사용할 보기를 선택할 수 있습니다.