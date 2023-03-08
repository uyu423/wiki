---
title: AOP: Spring Boot의 관점 지향 프로그래밍
description: 
published: true
date: 2023-02-17T18:01:29.248Z
tags: 
editor: markdown
dateCreated: 2023-01-30T02:00:50.592Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [AOP: Aspect-Oriented Programming in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/aop-aspect-oriented-programming-in-spring-boot)
{.links-list}


# AOP: 스프링 부트에서의 관점 지향 프로그래밍

Java의 주요 이점 중 하나는 플랫폼 독립성입니다. 그러나 많은 개발자들이 바로 이 기능을 활용하여 보다 간결하고 읽기 쉬운 코드를 작성할 수 있다는 사실을 깨닫지 못하고 있습니다. 여기에서 AOP(Aspect-Oriented Programming)가 등장합니다.

AOP는 관심사 분리(SoC)를 허용하여 모듈성을 높이는 것을 목표로 하는 프로그래밍 패러다임입니다. SoC는 소프트웨어 시스템을 별도의 부분으로 나누어야 하며 각 부분은 별도의 문제를 해결해야 한다는 설계 원칙입니다.

AOP는 코드 구조화에 대한 또 다른 사고 방식을 제공함으로써 객체 지향 프로그래밍(OOP)을 보완합니다. OOP가 객체 개념을 기반으로 한다면 AOP는 측면 개념을 기반으로 합니다.

애스펙트는 관심과 관련된 모듈식 기능 단위입니다. 관심사는 전체적으로 응용 프로그램과 관련된 기능입니다. 예를 들어 보안은 모든 애플리케이션과 관련된 문제입니다.

AOP를 통해 개발자는 문제를 다루는 코드를 모듈화할 수 있습니다. 이렇게 하면 코드를 보다 유지 관리하기 쉽고 이해하기 쉬워집니다. 또한 개발자가 다른 애플리케이션에서 측면을 재사용할 수 있습니다.

Spring Boot는 Java 애플리케이션 개발에 널리 사용되는 프레임워크입니다. Spring 프레임워크 위에 구축되어 개발자의 시간과 노력을 많이 절약해 줍니다.

Spring Boot를 사용하면 "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다. Spring 플랫폼에 대한 독선적인 견해를 취하고 함께 제공되는 모든 상용구 코드를 제거합니다.

Spring Boot는 또한 AOP 애플리케이션을 쉽게 만들 수 있게 해줍니다. 이번 글에서는 Spring Boot에서 AOP를 사용하는 방법에 대해 알아보겠습니다.

간단한 Spring Boot 애플리케이션을 만드는 것부터 시작하겠습니다. 그런 다음 메서드 호출을 기록하는 데 사용할 측면을 만듭니다. 마지막으로 AspectJ를 사용하도록 Spring Boot를 구성하는 방법을 살펴보겠습니다.

## 스프링 부트 애플리케이션 만들기

간단한 Spring Boot 애플리케이션을 만드는 것부터 시작하겠습니다. Spring Initializr를 사용하여 프로젝트를 생성합니다.

https://start.spring.io/로 이동하여 다음 세부 정보를 입력합니다.

* 그룹: com.example
* 아티팩트: aop-demo
* 이름: aop-데모
* 설명: Spring Boot에서 AOP 데모
* 패키지명 : com.example.aop
* 유형: 메이븐 프로젝트
* 포장: 항아리
* 자바 버전: 1.8
* 언어: 자바
* "스타터" 아래의 "웹" 확인란을 선택하십시오.

"프로젝트 생성"을 클릭하여 프로젝트를 다운로드합니다.

프로젝트를 즐겨찾는 IDE로 가져오고 com.example.aop.service라는 새 패키지를 만듭니다. 이 패키지에 CalculatorService라는 새 클래스를 만듭니다.

CalculatorService 클래스에 다음 코드를 추가합니다.

```java
package com.example.aop.service;

public class CalculatorService {

    public int add(int a, int b) {
        return a + b;
    }

    public int subtract(int a, int b) {
        return a - b;
    }

    public int multiply(int a, int b) {
        return a * b;
    }

    public int divide(int a, int b) {
        return a / b;
    }

}
```

이제 더하기, 빼기, 곱하기 및 나누기의 네 가지 메서드가 있는 간단한 CalculatorService를 만들었습니다.

다음으로 이러한 메서드를 REST 끝점으로 노출하는 컨트롤러를 만듭니다.

com.example.aop.controller라는 새 패키지와 이 패키지에 CalculatorController라는 새 클래스를 만듭니다.

CalculatorController 클래스에 다음 코드를 추가합니다.

```java
package com.example.aop.controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import com.example.aop.service.CalculatorService;

@RestController
public class CalculatorController {

    @Autowired
    private CalculatorService calculatorService;

    @GetMapping("/add")
    public int add(@RequestParam("a") int a, @RequestParam("b") int b) {
        return calculatorService.add(a, b);
    }

    @GetMapping("/subtract")
    public int subtract(@RequestParam("a") int a, @RequestParam("b") int b) {
        return calculatorService.subtract(a, b);
    }

    @GetMapping("/multiply")
    public int multiply(@RequestParam("a") int a, @RequestParam("b") int b) {
        return calculatorService.multiply(a, b);
    }

    @GetMapping("/divide")
    public int divide(@RequestParam("a") int a, @RequestParam("b") int b) {
        return calculatorService.divide(a, b);
    }

}
```

이제 CalculatorService의 네 가지 메서드를 REST 끝점으로 노출하는 간단한 CalculatorController를 만들었습니다.

애플리케이션을 Spring Boot 애플리케이션으로 실행하여 테스트할 수 있습니다.

## 애스펙트 만들기

이제 기본 Spring Boot 애플리케이션이 준비되어 실행 중이므로 aspect를 생성하는 방법을 살펴보겠습니다.

앞에서 언급했듯이 애스펙트는 관심사와 관련된 모듈식 기능 단위입니다. 이 예제에서는 메서드 호출을 기록하는 데 사용할 측면을 만들 것입니다.

com.example.aop.aspect라는 새 패키지와 이 패키지에 LoggingAspect라는 새 클래스를 만듭니다.

LoggingAspect 클래스에 다음 코드를 추가합니다.

```java
package com.example.aop.aspect;

import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Component;

@Aspect
@Component
public class LoggingAspect {

    private Logger logger = LoggerFactory.getLogger(this.getClass());

    @Before("execution(* com.example.aop.service.*.*(..))")
    public void logBefore(JoinPoint joinPoint) {

        logger.info("Entering method {} with arguments {}",
                joinPoint.getSignature().getName(),
                joinPoint.getArgs());
    }

}
```

이제 메서드 호출을 기록하는 데 사용할 간단한 측면을 만들었습니다. 이 측면은 com.example.aop.service 패키지의 모든 메서드 호출을 가로채고 로그에 메시지를 인쇄합니다.

## AspectJ를 사용하도록 스프링 부트 구성

이제 aspect가 생겼으니 이를 사용하도록 Spring Boot를 구성하는 방법을 살펴보겠습니다.

Spring Boot는 AspectJ를 사용하여 AOP를 활성화합니다. AspectJ는 AOP의 자바 구현입니다. Java 애플리케이션에 aspect를 짜는 데 사용할 수 있는 컴파일 타임 프레임워크를 제공합니다.

Spring Boot에서 AspectJ를 사용하려면 pom.xml 파일에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-aop</artifactId>
</dependency>
```

또한 기본 애플리케이션 클래스에 @EnableAspectJAutoProxy 주석을 추가해야 합니다.

```java
@SpringBootApplication
@EnableAspectJAutoProxy
public class AopDemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(AopDemoApplication.class, args);
    }
}
```

이 주석은 AspectJ 자동 프록시 생성을 가능하게 하므로 애플리케이션 컨텍스트의 모든 빈이 AOP 프록시가 됩니다.

## 애플리케이션 테스트

이제 동작 중인 aspect를 보기 위해 우리의 애플리케이션을 테스트해보자.

curl을 사용하여 애플리케이션을 테스트할 수 있습니다.

```
curl http://localhost:8080/add?a=1&b=2
```

그러면 다음 응답이 반환됩니다.

```
3
```

또한 로그를 확인하여 동작 중인 측면을 확인할 수 있습니다.

```
2018-11-11 16:27:17.196  INFO 18564 --- [nio-8080-exec-1] c.e.a.aspect.LoggingAspect  : Entering method add with arguments [1, 2]
2018-11-11 16:27:17.196  INFO 18564 --- [nio-8080-exec-1] c.e.a.aspect.LoggingAspect  : Returning value 3
```

우리가 볼 수 있듯이 LoggingAspect는 add 메서드의 호출을 가로채고 메서드 이름과 인수를 기록했습니다. 또한 반환된 값을 기록했습니다.

이것은 Spring Boot에서 AOP를 사용하는 방법에 대한 간단한 예일 뿐입니다. 트랜잭션 관리, 보안 및 캐싱과 같은 AOP의 다른 많은 용도가 있습니다.