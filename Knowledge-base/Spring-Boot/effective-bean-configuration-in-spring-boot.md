---
title: Spring Boot의 효과적인 Bean 구성
description: 
published: true
date: 2023-02-17T18:01:15.470Z
tags: 
editor: markdown
dateCreated: 2023-01-30T00:59:28.638Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Effective Bean Configuration in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/effective-bean-configuration-in-spring-boot)
{.links-list}



## 1. 소개

Bean은 Spring 애플리케이션의 기본 빌딩 블록입니다. Spring 빈은 Spring IoC 컨테이너에 의해 인스턴스화, 조립 및 관리되는 객체입니다. 이러한 빈은 일반적으로 XML 파일 형식으로 컨테이너에 제공하는 구성 메타데이터로 생성됩니다.

Spring Framework는 애플리케이션 내에서 Bean을 구성, 구성 및 관리하기 위한 포괄적인 기능 세트를 제공합니다. 여기에는 종속성 주입, 빈 범위 및 수명 주기 콜백 제공 기능이 포함됩니다.

Spring Boot에서 Bean은 클래스 경로의 내용에 따라 자동으로 구성됩니다. 그러나 이러한 bean의 구성을 추가로 사용자 정의하는 여러 가지 방법이 있습니다. 이 게시물에서는 Spring Boot에서 빈을 구성하는 가장 효과적인 방법 중 일부를 살펴보겠습니다.

## 2. 의존성 주입

의존성 주입은 Spring Framework의 핵심 기능입니다. 시스템의 구성 요소 간에 느슨한 결합을 달성하기 위한 기술입니다. 종속성 주입을 사용하면 특정 구성 요소의 종속성이 외부 엔터티에 의해 해당 구성 요소에 주입됩니다. 이 외부 엔티티는 일반적으로 Spring IoC 컨테이너입니다.

종속성 주입은 두 가지 주요 목표를 달성하는 데 사용됩니다.

* 시스템의 구성 요소 간의 긴밀한 결합을 줄입니다.

* 구성 요소에 대한 종속성 제공을 용이하게 합니다.

Spring Framework는 종속성 주입에 대한 포괄적인 지원을 제공합니다. Spring Boot에서는 종속성 주입이 기본적으로 활성화됩니다. 그러나 Spring Boot에서 의존성 주입을 사용할 때 염두에 두어야 할 몇 가지 사항이 있습니다.

첫째, 종속성 주입을 사용할 때 일반적으로 필드에 @Autowired 주석을 사용하는 것이 좋습니다. 이 주석은 주석이 달린 필드에 종속성을 주입하도록 Spring 컨테이너에 지시합니다. 예를 들어:

```java
@Autowired
private MyBean myBean;
```

위의 예에서 MyBean 종속성은 myBean 필드에 주입됩니다.

명심해야 할 또 다른 사항은 기본적으로 Spring 컨테이너는 필요한 종속성만 주입한다는 것입니다. 즉, 종속성이 필요하지 않은 경우 컨테이너는 종속성을 주입하지 않습니다. 이 동작은 @Primary 주석을 사용하여 변경할 수 있습니다. 이 주석은 빈에서 기본적으로 삽입되어야 함을 나타내기 위해 사용될 수 있습니다. 예를 들어:

```java
@Primary
@Bean
public MyBean myBean() {
    return new MyBean();
}
```

위의 예에서 myBean 빈은 기본적으로 주입됩니다.

## 3. 빈 스코프

Bean 범위는 애플리케이션 내에서 Bean의 가시성과 수명을 제어하는 데 사용됩니다. Spring은 Bean에 대해 다섯 가지 다른 범위를 정의합니다.

* 싱글톤
* 프로토타입
* 요구
* 세션
* 글로벌 세션

Bean의 기본 범위는 싱글톤입니다. 이는 기본적으로 애플리케이션당 하나의 빈 인스턴스만 생성됨을 의미합니다. 다른 범위는 일반적으로 상태를 유지해야 하는 Bean에 사용됩니다. 예를 들어 요청 범위는 일반적으로 단일 HTTP 요청에 대한 상태를 유지해야 하는 Bean에 사용됩니다.

Bean의 범위는 @Scope 주석을 사용하여 구성할 수 있습니다. 예를 들어:

```java
@Scope("request")
@Bean
public MyBean myBean() {
    return new MyBean();
}
```

위의 예에서 myBean 빈은 각 HTTP 요청에 대해 생성됩니다.

## 4. 빈 라이프사이클

Spring bean의 생명주기는 Spring IoC 컨테이너에 의해 관리됩니다. 빈이 처음 생성되면 컨테이너는 빈의 init() 메서드를 호출합니다. 이 메소드는 Bean에 필요한 모든 초기화를 수행하는 데 사용할 수 있습니다. 예를 들어:

```java
@Bean
public MyBean myBean() {
    return new MyBean();
}

@PostConstruct
public void init() {
    // Perform any initialization here
}
```

위의 예에서 init() 메서드는 myBean 빈이 생성된 후에 호출됩니다.

애플리케이션이 종료되면 컨테이너는 각 빈에서 destroy() 메서드를 호출합니다. 이 방법은 필요한 정리를 수행하는 데 사용할 수 있습니다. 예를 들어:

```java
@PreDestroy
public void destroy() {
    // Perform any cleanup here
}
```

위의 예에서 destroy() 메서드는 애플리케이션이 종료되기 전에 호출됩니다.

## 5. 외부 링크

* [Spring Boot 문서 - Bean 구성](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#boot-features-beans)

* [스프링 프레임워크 문서 - 종속성 주입](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#beans-di)

* [Spring Framework 문서 - Bean 범위](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#beans-factory-scopes)

* [스프링 프레임워크 문서 - 빈 라이프사이클](https://docs.spring.io/spring/docs/current/spring-framework-reference/core.html#beans-factory-lifecycle)