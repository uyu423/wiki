---
title: Spring Boot의 관점 지향 프로그래밍
description: 
published: true
date: 2023-02-08T09:33:11.442Z
tags: 
editor: markdown
dateCreated: 2023-02-08T09:33:05.471Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Aspect-Oriented Programming in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/aspect-oriented-programming-in-spring-boot)
{.links-list}


# 스프링 부트에서의 관점 지향 프로그래밍

AOP(Aspect-Oriented Programming)는 교차 절단 문제의 분리를 허용하여 모듈성을 높이는 것을 목표로 하는 프로그래밍 패러다임입니다. AOP는 엔터프라이즈 애플리케이션을 구현하는 데 사용되는 Spring AOP의 핵심을 구성합니다.

## AOP란?

측면 지향 프로그래밍은 개발자가 로깅, 보안 및 트랜잭션 관리와 같은 교차 절단 문제를 모듈화할 수 있도록 하는 패러다임입니다. 이는 이러한 문제를 관점이라는 별도의 모듈로 캡슐화하여 수행됩니다. 그런 다음 Aspect는 컴파일 타임, 로드 타임 또는 런타임에 기본 애플리케이션 코드로 짜여질 수 있습니다.

AOP는 OOP(객체 지향 프로그래밍)와 직교하며 함께 사용할 수 있습니다. 실제로 AOP의 많은 이점은 상속 및 구성과 같은 OOP 기술을 사용하여 얻을 수 있습니다. 그러나 AOP는 나중에 논의할 OOP에 비해 많은 이점을 제공합니다.

## AOP의 장점

### 1. 향상된 모듈성

앞에서 언급했듯이 AOP의 주요 이점 중 하나는 모듈성 증가입니다. 교차 절단 문제를 별도의 측면으로 모듈화하면 코드를 더 모듈화하고 이해하기 쉽게 만들 수 있습니다.

### 2. 코드 중복 감소

AOP의 또 다른 이점은 코드 중복 감소입니다. 교차 절단 문제는 종종 응용 프로그램 전체의 여러 위치에서 구현됩니다. 예를 들어 로깅 측면을 고려하십시오. 코드의 다양한 지점에서 메서드 호출을 기록하고 싶을 수 있습니다. AOP가 없으면 이러한 각 위치에서 로깅 코드를 복제해야 합니다. AOP를 사용하면 로깅 코드를 단일 측면으로 캡슐화하고 애플리케이션 전체에서 재사용할 수 있습니다.

### 3. 가독성 및 유지 관리성 향상

AOP는 또한 코드의 가독성과 유지 관리성을 향상시킬 수 있습니다. 다음 예를 고려하십시오.

```java
public void foo() {
  // do something
  bar();
  // do something else
}

public void bar() {
  // do something
}
```

이 예제에서 foo() 메서드는 bar() 메서드를 호출합니다. foo()에 로깅 코드를 추가하려면 bar() 호출 전후에 추가해야 합니다. AOP를 사용하면 이 로깅 코드를 aspect로 캡슐화하여 foo()와 bar() 모두에 적용할 수 있습니다. 그러면 다음 코드가 생성됩니다.

```java
public void foo() {
  // do something
  // logging code
  bar();
  // logging code
  // do something else
}

public void bar() {
  // logging code
  // do something
  // logging code
}
```

보시다시피 로깅 코드는 이제 aspect에서 중앙 집중화되어 foo() 및 bar() 메소드를 더 쉽게 읽고 유지 관리할 수 있습니다.

### 4. 향상된 테스트 가능성

AOP는 측면을 모의할 수 있도록 하여 코드의 테스트 가능성을 향상시킬 수도 있습니다. 예를 들어 데이터베이스를 사용하는 시스템을 생각해 보십시오. 시스템에 대한 몇 가지 단위 테스트를 작성하고 싶을 수 있지만 실제로 데이터베이스에 도달하고 싶지는 않습니다. AOP를 사용하면 데이터베이스 액세스 측면을 조롱하고 데이터베이스에 도달하지 않고 단위 테스트를 작성할 수 있습니다.

## AOP의 단점

AOP는 많은 이점을 제공하지만 몇 가지 단점도 있습니다.

### 1. 복잡성 증가

AOP의 주요 단점 중 하나는 복잡성 증가입니다. AOP는 추가 수준의 추상화를 도입하여 코드를 이해하기 어렵게 만들 수 있습니다.

### 2. 런타임 오버헤드

AOP의 또 다른 단점은 런타임 오버헤드입니다. AOP에 의해 도입된 추가 추상화로 인해 메모리 사용량이 증가하고 성능이 저하될 수 있습니다.

## 언제 AOP를 사용하는가?

그렇다면 다음 프로젝트에서 AOP를 사용해야 할까요? 소프트웨어 개발에서 대부분의 경우와 마찬가지로 답은 "상황에 따라 다릅니다"입니다.

모듈성 증가 또는 코드 중복 감소와 같은 AOP의 이점이 필요한 경우 AOP가 프로젝트에 적합할 수 있습니다. 그러나 성능 요구 사항이 엄격한 프로젝트에서 작업하는 경우 AOP가 최선의 선택이 아닐 수 있습니다.

## 스프링 부트에서 AOP를 사용하는 방법?

Spring AOP는 엔터프라이즈 애플리케이션을 구현하는 데 사용됩니다. AOP Alliance를 기반으로 하며 Java 5 구문을 사용합니다.

Spring Boot에서 AOP를 사용하려면 pom.xml에 spring-boot-starter-aop 종속성을 추가해야 합니다.

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-aop</artifactId>
</dependency>
```

또한 기본 클래스에 @EnableAspectJAutoProxy 주석을 추가하여 Spring Boot 애플리케이션에서 AOP를 활성화해야 합니다.

```java
@SpringBootApplication
@EnableAspectJAutoProxy
public class Application {

  public static void main(String[] args) {
    SpringApplication.run(Application.class, args);
  }

}
```

## 애스펙트 만들기

이제 애플리케이션에 AOP가 구성되었으므로 aspect를 생성해 보겠습니다. Spring AOP의 Aspect는 @Aspect 주석이 달린 일반 Java 클래스를 사용하여 구현됩니다.

다음 예를 고려하십시오.

```java
@Aspect
public class MyAspect {

  // methods and pointcuts go here

}
```

이 예제에서는 MyAspect라는 간단한 aspect를 생성했습니다. Aspect는 많은 메소드와 포인트컷을 포함할 수 있습니다. 메서드와 포인트컷에 대해서는 나중에 자세히 설명하겠습니다.

## 측면 적용

애스펙트를 생성했으면 이를 코드에 적용해야 합니다. 이것은 포인트컷을 사용하여 수행됩니다. 포인트컷은 조인 포인트와 일치하는 조건자입니다. 조인 포인트는 메서드 호출과 같은 프로그램 실행 지점입니다.

Pointcut은 정규식 또는 Java 5 구문을 사용하여 정의할 수 있습니다. 예를 들어 다음 포인트컷은 com.example 패키지의 모든 메소드와 일치합니다.

```java
@Pointcut("execution(* com.example..*.*(..))")
public void myPointcut() {}
```

myPointcut() 메서드는 pointcut에 대한 자리 표시자일 뿐입니다. 이제 @Before 및 @After 주석을 사용하여 코드에 aspect를 적용할 수 있습니다. @Before 어노테이션은 메소드가 호출되기 전에 aspect가 실행되도록 하고 @After 어노테이션은 메소드가 호출된 후에 aspect가 실행되도록 합니다.

다음 예를 고려하십시오.

```java
@Aspect
public class MyAspect {

  @Pointcut("execution(* com.example..*.*(..))")
  public void myPointcut() {}

  @Before("myPointcut()")
  public void before(JoinPoint joinPoint) {
    // do something
  }

  @After("myPointcut()")
  public void after(JoinPoint joinPoint) {
    // do something
  }

}
```

이 예제에서는 com.example 패키지의 모든 메소드와 일치하는 포인트컷을 정의했습니다. 또한 일치하는 메서드가 호출되기 전에 실행될 before() 메서드와 일치하는 메서드가 호출된 후 실행될 after() 메서드도 정의했습니다.

## 결론

이 기사에서는 Aspect 지향 프로그래밍과 Spring Boot에서 어떻게 사용할 수 있는지에 대해 논의했습니다. 또한 Spring Boot에서 관점을 만들고 적용하는 방법도 살펴보았습니다.