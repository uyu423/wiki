---
title: 원격 디버깅을 사용한 스프링 부트 디버깅
description: 
published: true
date: 2023-02-02T20:57:31.800Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:57:27.233Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot Debugging with Remote Debugging***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-debugging-with-remote-debugging)
{.links-list}


# 소개

개발자는 종종 오류를 찾아 수정하기 위해 코드를 디버깅해야 합니다. 원격 디버거 사용을 포함하여 다양한 방법으로 Spring Boot 애플리케이션을 디버깅할 수 있습니다. 이 기사에서는 원격 디버거를 사용하여 Spring Boot 애플리케이션을 디버깅하는 방법을 살펴봅니다.

# 원격 디버깅이란?

원격 디버깅은 개발자가 원격 시스템에서 실행 중인 프로그램을 디버깅할 수 있도록 하는 프로세스입니다. 이렇게 하려면 개발자가 원격 컴퓨터에 액세스할 수 있어야 하며 디버거를 사용하여 연결할 수 있어야 합니다.

# 원격 디버거를 사용하여 Spring Boot 애플리케이션을 디버깅하는 방법

원격 디버거를 사용하여 Spring Boot 애플리케이션을 디버깅하기 위해 따라야 하는 몇 가지 단계가 있습니다. 이러한 각 단계를 자세히 살펴보겠습니다.

## 1. 애플리케이션이 디버그 모드에서 실행 중인지 확인

첫 번째 단계는 Spring Boot 애플리케이션이 디버그 모드에서 실행 중인지 확인하는 것입니다. application.properties 파일에 다음 줄을 추가하면 됩니다.

```
spring.boot.devtools.remote.debug=true
```

## 2. 원격 디버거 시작

다음 단계는 원격 디버거를 시작하는 것입니다. 이는 다음 명령을 실행하여 수행할 수 있습니다.

```
java -Xdebug -Xrunjdwp:server=y,transport=dt_socket,address=8000,suspend=n -jar myapp.jar
```

myapp.jar을 Spring Boot 애플리케이션의 이름으로 바꿉니다.

## 3. 원격 디버거에 연결

마지막 단계는 원격 디버거에 연결하는 것입니다. 이 작업은 Eclipse 또는 IntelliJ와 같은 디버거를 사용하여 수행할 수 있습니다. Eclipse에서 Debug Perspective로 이동하여 Remote Java Application을 선택하십시오. 연결 탭에서 Spring Boot 애플리케이션이 포함된 프로젝트를 선택합니다. 연결 탭에서 Spring Boot 애플리케이션이 포함된 프로젝트를 선택합니다. 연결 탭에서 Spring Boot 애플리케이션이 포함된 프로젝트를 선택합니다. 연결 탭에서 Spring Boot 애플리케이션이 포함된 프로젝트를 선택합니다. 연결 탭에서 Spring Boot 애플리케이션이 포함된 프로젝트를 선택합니다.

IntelliJ에서 실행 > 구성 편집으로 이동합니다. 원격 탭에서 Spring Boot 애플리케이션이 포함된 프로젝트를 선택합니다. 연결 탭에서 Spring Boot 애플리케이션이 포함된 프로젝트를 선택합니다.

# 결론

이 기사에서는 원격 디버거를 사용하여 Spring Boot 애플리케이션을 디버깅하는 방법을 살펴보았습니다. 이를 위해 따라야 할 단계도 거쳤습니다.