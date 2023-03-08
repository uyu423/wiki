---
title: VisualVM을 사용한 스프링 부트 프로파일링
description: 
published: true
date: 2023-01-31T20:57:39.329Z
tags: 
editor: markdown
dateCreated: 2023-01-31T20:57:35.629Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Spring Boot Profiling with VisualVM***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-profiling-with-visualvm)
{.links-list}



# VisualVM을 사용한 스프링 부트 프로파일링

Spring Boot는 마이크로서비스 및 기타 프로덕션 등급 애플리케이션을 구축하기 위한 훌륭한 프레임워크입니다. Spring Boot 사용의 이점 중 하나는 Tomcat 서버가 포함되어 있어 응용 프로그램을 독립 실행형 jar로 쉽게 배포할 수 있다는 것입니다.

그러나 임베디드 서버를 사용할 때의 단점 중 하나는 성능 문제를 해결하기 어려울 수 있다는 것입니다. 이 기사에서는 VisualVM을 사용하여 Spring Boot 애플리케이션을 프로파일링하는 방법을 살펴보겠습니다.

## VisualVM이란?

VisualVM은 Java 애플리케이션에 대한 자세한 정보를 볼 수 있는 그래픽 인터페이스를 제공하는 도구입니다. JVM에서 실행 중인 애플리케이션을 모니터링하고 문제를 해결하는 데 사용할 수 있습니다.

## VisualVM 설치

VisualVM은 Oracle JDK에 포함되어 있으므로 JDK가 설치되어 있으면 이미 VisualVM이 있는 것입니다. JDK가 설치되어 있지 않은 경우 [Oracle 웹 사이트](https://www.oracle.com/java/technologies/visualvm.html)에서 VisualVM을 다운로드할 수 있습니다.

## 스프링 부트 애플리케이션 프로파일링

이제 VisualVM을 설치했으므로 이를 사용하여 Spring Boot 애플리케이션을 프로파일링하는 방법을 살펴보겠습니다.

먼저 Spring Boot 애플리케이션을 시작해야 합니다. 이 예시에서는 [Spring PetClinic](https://github.com/spring-projects/spring-petclinic) 샘플 애플리케이션을 사용하겠습니다.

애플리케이션이 실행되면 VisualVM을 열고 실행 중인 애플리케이션에 연결할 수 있습니다. 이렇게 하려면 "파일" 메뉴를 클릭하고 "JMX 연결 추가"를 선택합니다.

![VisualVM JMX 연결 추가](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-add-jmx-connection.png)

"JMX 연결 추가" 대화 상자에서 실행 중인 애플리케이션의 호스트와 포트를 입력합니다. 기본 호스트는 "localhost"이고 기본 포트는 "1099"입니다.

![VisualVM JMX 연결 추가 대화 상자](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-add-jmx-connection-dialog.png)

실행 중인 애플리케이션에 연결하려면 "확인"을 클릭하십시오.

VisualVM이 실행 중인 애플리케이션에 연결되면 "애플리케이션" 탭에 애플리케이션이 표시되어야 합니다.

![VisualVM 애플리케이션 탭](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-applications-tab.png)

애플리케이션 프로파일링을 시작하려면 "애플리케이션" 탭에서 애플리케이션을 선택하고 "프로파일" 버튼을 클릭하십시오.

![VisualVM 프로필 버튼](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-profile-button.png)

"프로파일 애플리케이션" 대화창에서 "CPU" 프로파일링 유형을 선택하고 "시작"을 클릭하십시오.

![VisualVM 프로필 애플리케이션 대화 상자](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-profile-application-dialog.png)

프로파일링 세션이 시작되면 VisualVM을 사용하여 스레드 활동, 메모리 사용량 및 실행 중인 애플리케이션에 대한 기타 정보를 볼 수 있습니다.

![VisualVM 모니터 탭](https://github.com/spring-projects/spring-petclinic/raw/master/docs/images/visualvm-monitor-tab.png)

응용 프로그램 프로파일링을 마치면 "파일" 메뉴를 선택하고 "종료"를 선택하여 프로파일링 세션을 중지할 수 있습니다.

## 결론

이 기사에서는 VisualVM을 사용하여 Spring Boot 애플리케이션을 프로파일링하는 방법을 살펴보았습니다. VisualVM은 Spring Boot 애플리케이션의 성능 문제를 해결하는 데 사용할 수 있는 강력한 도구입니다.