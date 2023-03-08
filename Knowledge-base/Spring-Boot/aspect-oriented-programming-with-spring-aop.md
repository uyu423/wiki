---
title: Spring AOP를 사용한 관점 지향 프로그래밍
description: 
published: true
date: 2023-02-07T00:32:34.259Z
tags: 
editor: markdown
dateCreated: 2023-02-07T00:32:32.682Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Aspect-Oriented Programming with Spring AOP***English** document is available*](/en/Knowledge-base/Spring-Boot/aspect-oriented-programming-with-spring-aop)
{.links-list}


# Spring AOP를 사용한 Aspect 지향 프로그래밍

AOP(Aspect-Oriented Programming)는 교차 절단 문제의 분리를 허용하여 모듈성을 높이는 것을 목표로 하는 프로그래밍 패러다임입니다. AOP는 Spring AOP와 같은 엔터프라이즈 애플리케이션 프레임워크의 기반을 형성합니다.

Spring AOP는 Java에서 Aspect 지향 프로그래밍을 위한 강력한 도구입니다. 이를 통해 교차 절단 문제를 별도의 측면에서 모듈화하고 Spring 애플리케이션 컨텍스트에 배포된 빈에 적용할 수 있습니다. 이 기사에서는 Spring AOP를 사용하여 로깅, 감사 및 성능 모니터링과 같은 일반적인 AOP 사용 사례를 구현하는 방법을 살펴보겠습니다.

메서드 실행 시간을 기록하기 위해 Spring AOP를 사용하는 방법에 대한 간단한 예제부터 시작하겠습니다. 그런 다음 Spring 애플리케이션 컨텍스트에서 bean에 aspect를 적용하기 위해 포인트컷과 어드바이스를 사용하는 방법을 볼 것이다.

## 로깅 방법 실행 시간

각 메서드의 실행 시간을 기록하려는 간단한 서비스가 있다고 가정합니다.

```java
public class MyService {

    public void doWork() {
        // do some work
    }
}
```

Spring AOP를 사용하여 다음 측면에서 이 서비스의 각 메서드 실행 시간을 기록할 수 있습니다.

```java
@Aspect
@Component
public class LoggingAspect {

    @Around("execution(* com.example.myservice.*.*(..))")
    public Object logExecutionTime(ProceedingJoinPoint joinPoint) throws Throwable {
        long start = System.currentTimeMillis();
        Object proceed = joinPoint.proceed();
        long elapsedTime = System.currentTimeMillis() - start;
        System.out.println(joinPoint.getSignature() + " executed in " + elapsedTime + "ms");
        return proceed;
    }
}
```

`@Around` 주석은 이것이 주변 어드바이스임을 나타냅니다. 포인트컷 표현식 `execution(* com.example.myservice.*.*(..))`은 Spring AOP에게 `com.example.myservice` 패키지의 모든 메소드에 이 측면을 적용하도록 지시합니다.

`logExecutionTime()` 메소드는 실제 어드바이스입니다. 권장되는 메서드를 나타내는 인수로 `ProceedingJoinPoint`를 사용합니다. `logExecutionTime()` 메서드는 먼저 현재 시간을 밀리초 단위로 가져온 다음 조인 포인트에서 `proceed()` 메서드를 호출하여 조언된 메서드를 실행하고 마지막으로 경과 시간을 계산하고 콘솔에 인쇄합니다.

이 측면을 `MyService` 클래스에 적용하려면 구성에 `@EnableAspectJAutoProxy` 주석을 추가해야 합니다.

```java
@Configuration
@EnableAspectJAutoProxy
public class AppConfig {

    @Bean
    public MyService myService() {
        return new MyService();
    }

    @Bean
    public LoggingAspect loggingAspect() {
        return new LoggingAspect();
    }
}
```

`@EnableAspectJAutoProxy` 어노테이션은 Spring의 auto-proxy 메커니즘을 활성화합니다. 이는 aspect가 적용되도록 bean을 aspect로 프록시합니다.

그런 다음 애플리케이션에서 `MyService` 빈을 사용할 수 있습니다.

```java
public class App {

    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        MyService myService = context.getBean(MyService.class);
        myService.doWork();
    }
}
```

이 애플리케이션을 실행하면 다음 출력이 표시됩니다.

```
void com.example.myservice.MyService.doWork() executed in 0ms
```

감사 및 성능 모니터링과 같은 다른 AOP 사용 사례를 구현하기 위해 `@Around` 어드바이스를 사용할 수도 있습니다.

## 빈에 Aspect 적용하기

이전 섹션에서 메서드 실행 시간을 기록하기 위해 `@Around` 어드바이스를 사용하는 방법을 살펴보았습니다. 하지만 이 측면을 애플리케이션의 일부 빈에만 적용하려면 어떻게 해야 할까요? 포인트컷과 조언을 사용하여 이를 수행할 수 있습니다.

포인트컷은 조인 포인트와 일치하는 조건자입니다. 조인 포인트는 관점이 연결될 수 있는 프로그램 실행 지점입니다. Spring AOP에서 조인 포인트는 항상 메소드 호출을 나타냅니다.

어드바이스는 포인트컷과 연관되며 포인트컷과 일치하는 조인포인트에 도달할 때 실행됩니다. Spring AOP에는 네 가지 유형의 어드바이스가 있습니다.

- `@Before`: 조인 포인트 이전에 실행
- `@After`: 예외 발생 여부와 관계없이 조인 포인트 이후에 실행됩니다.
- `@AfterReturning`: Join Point가 정상적으로 완료된 후 실행
- `@AfterThrowing`: 조인 포인트가 예외를 던진 후에 실행됨

포인트컷과 어드바이스를 사용하여 애플리케이션에서 빈에 aspect를 선택적으로 적용할 수 있습니다. 예를 들어 이름이 `myService`로 시작하는 빈에만 `LoggingAspect`를 적용한다고 가정합니다. 다음 구성으로 이 작업을 수행할 수 있습니다.

```java
@Configuration
@EnableAspectJAutoProxy
public class AppConfig {

    @Bean
    @Lazy
    @Scope("prototype")
    @Pointcut("bean(*myService*)")
    public LoggingAspect loggingAspect() {
        return new LoggingAspect();
    }
}
```

여기서 우리는 `@Pointcut`을 사용하여 `loggingAspect()` 메소드에 주석을 달았습니다. 이는 이름이 `myService`로 시작하는 모든 빈에 이 관점을 적용하도록 Spring AOP에 지시합니다. 또한 애플리케이션 컨텍스트에 의해 인스턴스화된 빈에만 aspect가 적용되도록 `@Lazy` 및 `@Scope("prototype")`로 aspect bean에 주석을 달았습니다.

이 구성을 사용하면 `LoggingAspect`는 이름이 `myService`로 시작하는 빈에만 적용됩니다.

## 결론

이 기사에서는 Spring AOP를 사용하여 로깅, 감사 및 성능 모니터링과 같은 일반적인 AOP 사용 사례를 구현하는 방법을 살펴보았습니다. 우리는 또한 애플리케이션 컨텍스트에서 bean에 aspect를 선택적으로 적용하기 위해 포인트컷과 어드바이스를 사용하는 방법을 보았다.

Spring AOP를 사용하면 우려 사항을 모듈화하고 일관되고 선언적인 방식으로 애플리케이션의 빈에 적용할 수 있습니다.