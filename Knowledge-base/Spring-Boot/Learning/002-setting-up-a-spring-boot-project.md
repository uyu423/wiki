---
title: 002: 스프링 부트 프로젝트 설정
description: 
published: true
date: 2023-02-03T07:05:23.450Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:05:18.586Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [002: Setting up a Spring Boot project***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/002-setting-up-a-spring-boot-project)
{.links-list}


# 스프링 부트 프로젝트 설정

이번 포스트에서는 Spring Boot 프로젝트를 설정하는 방법을 살펴보겠습니다.

Spring Boot는 웹 애플리케이션 및 서비스를 구축하는 데 널리 사용되는 프레임워크입니다. Spring 프레임워크 위에 구축되어 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다.

## 전제 조건

시작하기 전에 따라하기 위해 필요한 몇 가지 사항이 있습니다.

- 자바 8 이상
- 텍스트 편집기 또는 IDE
- 메이븐 3.3.9 이상

## 프로젝트 생성

Spring Boot 프로젝트를 생성하는 몇 가지 방법이 있습니다. 이번 포스팅에서는 [Spring Initializr](https://start.spring.io/)를 이용하여 프로젝트를 생성해 보겠습니다.

Spring Initializr 웹 사이트로 이동하여 다음 정보로 양식을 작성하십시오.

- 프로젝트: 메이븐 프로젝트
- 언어: 자바
- 스프링 부트 버전: 2.1.7

"프로젝트 생성" 버튼을 클릭하면 zip 파일이 다운로드됩니다. 선택한 디렉토리에 zip 파일의 내용을 추출하십시오.

## 프로젝트 가져오기

텍스트 편집기 또는 IDE에서 프로젝트를 Maven 프로젝트로 가져옵니다. Eclipse를 사용하는 경우 파일 -> 가져오기 -> 기존 Maven 프로젝트로 이동하여 이 작업을 수행할 수 있습니다.

## 프로젝트 실행

이제 프로젝트가 설정되었으므로 실행할 수 있습니다.

Spring Boot 애플리케이션을 실행하는 몇 가지 방법이 있습니다. 가장 간단한 방법은 Maven 플러그인을 사용하는 것입니다.

```
mvn spring-boot:run
```

다음과 유사한 출력이 표시되어야 합니다.

```
[INFO] Scanning for projects...
[INFO] 
[INFO] ------------------------------------------------------------------------
[INFO] Building myproject 0.0.1-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] >>> spring-boot-maven-plugin:2.1.7.RELEASE:run (default-cli) > test-compile @ myproject >>>
[INFO] 
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ myproject ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /Users/user/Documents/workspace-sts-3.9.10.RELEASE/myproject/src/main/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ myproject ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] >>> spring-boot-maven-plugin:2.1.7.RELEASE:run (default-cli) > compile @ myproject >>>
[INFO] 
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ myproject ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /Users/user/Documents/workspace-sts-3.9.10.RELEASE/myproject/src/main/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ myproject ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] >>> spring-boot-maven-plugin:2.1.7.RELEASE:run (default-cli) > test-compile @ myproject >>>
[INFO] 
[INFO] <<< spring-boot-maven-plugin:2.1.7.RELEASE:run (default-cli) < test-compile @ myproject <<<
[INFO] 
[INFO] 
[INFO] --- spring-boot-maven-plugin:2.1.7.RELEASE:run (default-cli) @ myproject ---
[INFO] Attaching agents: []

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.1.7.RELEASE)

2019-06-07 23:58:45.583  INFO 86848 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2019-06-07 23:58:45.602  INFO 86848 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2019-06-07 23:58:45.602  INFO 86848 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.22]
2019-06-07 23:58:45.697  INFO 86848 --- [ost-startStop-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2019-06-07 23:58:45.697  INFO 86848 --- [ost-startStop-1] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 100 ms
2019-06-07 23:58:46.069  INFO 86848 --- [ost-startStop-1] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2019-06-07 23:58:46.145  INFO 86848 --- [ost-startStop-1] o.s.b.w.servlet.ServletRegistrationBean  : Servlet dispatcherServlet mapped to [/]
2019-06-07 23:58:46.149  INFO 86848 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'characterEncodingFilter' to: [/*]
2019-06-07 23:58:46.149  INFO 86848 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'hiddenHttpMethodFilter' to: [/*]
2019-06-07 23:58:46.149  INFO 86848 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'httpPutFormContentFilter' to: [/*]
2019-06-07 23:58:46.149  INFO 86848 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'requestContextFilter' to: [/*]
2019-06-07 23:58:46.839  INFO 86848 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Shutting down ExecutorService 'applicationTaskExecutor'
2019-06-07 23:58:46.841  INFO 86848 --- [           main] o.apache.catalina.core.StandardService   : Stopping service [Tomcat]
2019-06-07 23:58:46.857  INFO 86848 --- [           main] ConditionEvaluationReportLoggingListener : 

Error starting ApplicationContext. To display the conditions report re-run your application with 'debug' enabled.
2019-06-07 23:58:46.862 ERROR 86848 --- [           main] o.s.boot.SpringApplication               : Application run failed

org.springframework.boot.context.event.ApplicationFailedEvent[source=org.springframework.boot.SpringApplication@4f4f4f4f]

```

이 출력이 표시되면 프로젝트가 시작되어 실행 중임을 의미합니다!