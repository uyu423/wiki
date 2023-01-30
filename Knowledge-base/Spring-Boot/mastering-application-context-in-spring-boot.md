---
title: Spring Boot에서 애플리케이션 컨텍스트 마스터하기
description: 
published: true
date: 2023-01-30T01:00:45.137Z
tags: 
editor: markdown
dateCreated: 2023-01-30T01:00:45.137Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Mastering Application Context in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/mastering-application-context-in-spring-boot)
{.links-list}




Spring Boot에서 ApplicationContext는 스프링 프레임워크의 핵심입니다. 애플리케이션의 모든 빈과 리소스를 관리하는 역할을 합니다. ApplicationContext는 또한 등록된 리스너에 대한 이벤트 게시를 담당합니다.

ApplicationContext는 상위 컨텍스트와 하위 컨텍스트의 두 부분으로 나뉩니다. 상위 컨텍스트는 구성 로드 및 Spring 주석 초기화를 담당합니다. 자식 컨텍스트는 빈과 리소스를 로드하는 역할을 합니다.

Spring Boot는 ApplicationContext를 초기화하는 두 가지 방법을 제공합니다.

1. @SpringBootApplication 주석 사용
2. ApplicationContextInitializer 사용

@SpringBootApplication 주석은 클래스를 Spring Boot 애플리케이션으로 표시하는 데 사용됩니다. 이 주석은 Spring 빈을 자동 구성하고 ApplicationContext를 자동 초기화하는 데 사용됩니다.

ApplicationContextInitializer는 ApplicationContext를 초기화하는 데 사용됩니다. 이 인터페이스는 ApplicationContext에 사용자 지정자를 추가하는 데 사용됩니다. ApplicationContextInitializer는 beanFactoryPostProcessor가 호출되기 전에 ApplicationContext를 초기화하는 데 사용됩니다.

ApplicationContext를 초기화할 때 Spring Boot는 먼저 @SpringBootApplication 주석을 검색한 다음 ApplicationContextInitializer에 대한 클래스 경로를 스캔합니다. 둘 다 발견되면 ApplicationContextInitializer가 먼저 호출되고 @SpringBootApplication이 두 번째로 호출됩니다.

@SpringBootApplication 주석을 사용하여 ApplicationContext를 구성할 수 있습니다. @SpringBootApplication에는 다음 속성이 있습니다.

1. basePackages: 이 속성은 주석이 달린 클래스를 검색할 기본 패키지를 지정하는 데 사용됩니다. 기본적으로 @SpringBootApplication은 클래스 경로의 모든 패키지를 스캔합니다.

2. 제외: 이 속성은 검사에서 제외할 패키지를 지정하는 데 사용됩니다.

3. includeFilters: 이 속성은 스캔에 포함할 필터를 지정하는 데 사용됩니다.

4. excludeFilters: 이 속성은 검사에서 제외할 필터를 지정하는 데 사용됩니다.

5. resourcePatterns: 이 속성은 스캔에 포함할 리소스 패턴을 지정하는 데 사용됩니다.

6. useDefaultFilters: 이 속성은 기본 필터를 사용할지 여부를 지정하는 데 사용됩니다. 기본 필터는 주석이 달린 클래스, 자원 및 Bean을 스캔하는 데 사용됩니다.

7. lazyInit: 이 속성은 빈이 지연 초기화되어야 하는지 여부를 지정하는 데 사용됩니다. 기본적으로 빈은 열심히 초기화됩니다.

ApplicationContext는 ApplicationContextInitializer를 사용하여 사용자 지정할 수 있습니다. ApplicationContextInitializer는 ApplicationContext에 사용자 지정자를 추가하는 데 사용할 수 있습니다. ApplicationContextInitializer는 beanFactoryPostProcessor가 호출되기 전에 ApplicationContext를 초기화하는 데 사용됩니다.

ApplicationContextInitializer는 ApplicationContext를 사용자 지정하는 데 사용할 수 있는 콜백 인터페이스입니다. ApplicationContextInitializer는 ApplicationContext가 생성되기 전에 호출됩니다.

ApplicationContextInitializer에는 다음과 같은 메서드가 있습니다.

1. initialize(): 이 메서드는 ApplicationContext를 초기화하는 데 사용됩니다.

2. getOrdered(): 이 메서드는 ApplicationContextInitializer의 순서를 가져오는 데 사용됩니다.

Spring.factories 파일에 ApplicationContextInitializer를 추가하여 ApplicationContext를 사용자 정의할 수 있습니다. ApplicationContextInitializer는 ServiceLoader를 사용하여 로드됩니다.

spring.factories 파일은 META-INF/spring.factories 폴더에 있습니다. spring.factories 파일에는 다음이 포함됩니다.

1. org.springframework.context.ApplicationContextInitializer: 이것은 ApplicationContextInitializer 클래스의 목록입니다.

2. org.springframework.context.support.AbstractApplicationContext: AbstractApplicationContext 클래스 목록입니다.

spring.factories 파일을 사용하여 ApplicationContext를 사용자 정의할 수 있습니다. spring.factories 파일은 ApplicationContextInitializer를 ApplicationContext에 추가하는 데 사용할 수 있습니다.

spring.factories 파일을 사용하여 ApplicationContext를 사용자 정의할 수 있습니다. spring.factories 파일은 ApplicationContextInitializer를 ApplicationContext에 추가하는 데 사용할 수 있습니다. spring.factories 파일을 사용하여 ApplicationContext를 사용자 정의할 수 있습니다. spring.factories 파일은 ApplicationContextInitializer를 ApplicationContext에 추가하는 데 사용할 수 있습니다.

Spring.factories 파일에 ApplicationContextInitializer를 추가하여 ApplicationContext를 사용자 정의할 수 있습니다. ApplicationContextInitializer는 ServiceLoader를 사용하여 로드됩니다.

Spring.factories 파일에 ApplicationContextInitializer를 추가하여 ApplicationContext를 사용자 정의할 수 있습니다. ApplicationContextInitializer는 ServiceLoader를 사용하여 로드됩니다. ApplicationContextInitializer는 ApplicationContext가 생성되기 전에 호출됩니다.

ApplicationContextInitializer에는 다음과 같은 메서드가 있습니다.

1. initialize(): 이 메서드는 ApplicationContext를 초기화하는 데 사용됩니다.

2. getOrdered(): 이 메서드는 ApplicationContextInitializer의 순서를 가져오는 데 사용됩니다.

Spring.factories 파일에 ApplicationContextInitializer를 추가하여 ApplicationContext를 사용자 정의할 수 있습니다. ApplicationContextInitializer는 ServiceLoader를 사용하여 로드됩니다. ApplicationContextInitializer는 ApplicationContext가 생성되기 전에 호출됩니다. ApplicationContextInitializer에는 다음과 같은 메서드가 있습니다.

1. initialize(): 이 메서드는 ApplicationContext를 초기화하는 데 사용됩니다.

2. getOrdered(): 이 메서드는 ApplicationContextInitializer의 순서를 가져오는 데 사용됩니다.