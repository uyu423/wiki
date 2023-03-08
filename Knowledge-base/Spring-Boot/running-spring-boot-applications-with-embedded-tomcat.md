---
title: 임베디드 Tomcat으로 Spring Boot 애플리케이션 실행
description: 
published: true
date: 2023-02-17T18:02:39.556Z
tags: 
editor: markdown
dateCreated: 2023-01-30T09:54:39.274Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Running Spring Boot Applications with Embedded Tomcat***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/running-spring-boot-applications-with-embedded-tomcat)
{.links-list}


오랫동안 Apache Tomcat 팀은 Tomcat을 더 넓은 범위에 포함하는 방법에 대한 지침이 포함된 [페이지](https://tomcat.apache.org/tomcat-7.0-doc/embedded-howto.html)를 유지 관리했습니다. 응용 프로그램. 이 페이지는 몇 가지 인기 있는 애플리케이션 서버를 다루지만 Spring Boot는 다루지 않습니다. 최근에 Tomcat 팀은 포함된 문서를 기본 Tomcat 문서 사이트로 [이동](https://tomcat.apache.org/tomcat-9.0-doc/setup.html)하고 [추가](https://tomcat.apache .org/tomcat-9.0-doc/faq/index.html) Tomcat에 대한 자주 묻는 질문에 대한 섹션입니다.

Spring Boot 애플리케이션에 Tomcat을 임베드하는 몇 가지 방법이 있습니다. 가장 쉬운 방법은 `spring-boot-starter-tomcat` 종속성을 프로젝트에 추가하는 것입니다. 그러면 Spring Boot가 자동으로 Tomcat을 구성합니다. Spring Boot는 또한 몇 가지 [다른 임베디드 컨테이너](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-developing-web-applications.html#boot-features- 임베디드 컨테이너 지원).

Tomcat 구성에 대해 더 많은 제어를 원하는 경우 `tomcat-embed-core` 종속성을 프로젝트에 추가할 수 있으며 Spring Boot는 자동으로 `TomcatEmbeddedServletContainerFactory`를 구성합니다. 그런 다음 속성을 설정하여 팩터리를 사용자 지정할 수 있습니다. 예를 들어 [포트를 설정](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/context/embedded/tomcat/TomcatEmbeddedServletContainerFactory.html#setPort-int할 수 있습니다. -) Tomcat이 듣는다.

더 많은 제어가 필요한 경우 `Tomcat` 인스턴스를 직접 [인스턴스화](https://tomcat.apache.org/tomcat-9.0-doc/setup.html#Instantiating_Tomcat)하고 [추가](https:// tomcat.apache.org/tomcat-9.0-doc/setup.html#Adding_Connectors_and_Services_ 프로그래밍 방식으로) 커넥터 및 서비스. 그런 다음 Spring Boot는 [래핑](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/context/embedded/tomcat/TomcatEmbeddedServletContainerFactory.html#getTomcatEmbeddedServletContainer-org.apache. catalina.startup.Tomcat-) `TomcatEmbeddedServletContainer`의 Tomcat 인스턴스.

다음은 Spring Boot 애플리케이션에 Tomcat을 포함하는 방법을 보여주는 샘플 프로젝트입니다.

https://github.com/spring-projects/spring-boot/tree/master/spring-boot-samples/spring-boot-sample-tomcat-multi-connectors

샘플 프로젝트에는 포트 8080의 HTTP 커넥터와 포트 8009의 AJP 커넥터 등 두 개의 커넥터가 구성되어 있습니다. AJP 커넥터는 기본적으로 주석 처리되어 있습니다. 이를 사용하려면 `src/main/resources/application.properties`에서 `<Connector>` 요소 주변의 `<!--` 및 `-->` 태그의 주석 처리를 제거하십시오.

그런 다음 다음 명령을 사용하여 샘플 애플리케이션을 빌드하고 실행할 수 있습니다.

```
$ ./mvnw spring-boot:run
```

애플리케이션은 포트 8080에서 시작됩니다. http://localhost:8080/에서 애플리케이션에 액세스할 수 있습니다. http://localhost:8009/에서 AJP 커넥터를 통해 애플리케이션에 액세스할 수도 있습니다.

## 참조

- [Apache Tomcat 문서 -임베디드 HOW-TO](https://tomcat.apache.org/tomcat-7.0-doc/embedded-howto.html)
- [Apache Tomcat 설명서 - 설정](https://tomcat.apache.org/tomcat-9.0-doc/setup.html)
- [Apache Tomcat 문서 - FAQ](https://tomcat.apache.org/tomcat-9.0-doc/faq/index.html)
- [Spring Boot 문서 - 웹 애플리케이션 개발](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-developing-web-applications.html#boot-features-embedded -컨테이너 지원)
- [Spring Boot API 문서 - TomcatEmbeddedServletContainerFactory](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/context/embedded/tomcat/TomcatEmbeddedServletContainerFactory.html)
- [Spring Boot API 문서 - TomcatEmbeddedServletContainer](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/context/embedded/tomcat/TomcatEmbeddedServletContainer.html)
- [임베디드 Tomcat이 포함된 샘플 Spring Boot 애플리케이션](https://github.com/spring-projects/spring-boot/tree/master/spring-boot-samples/spring-boot-sample-tomcat-multi-connectors)