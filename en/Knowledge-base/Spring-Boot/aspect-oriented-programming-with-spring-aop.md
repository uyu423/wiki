---
title: Aspect-Oriented Programming with Spring AOP
description: 
published: true
date: 2023-02-07T00:32:38.456Z
tags: 
editor: markdown
dateCreated: 2023-02-07T00:32:32.686Z
---

- [Programación orientada a aspectos con Spring AOP***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/aspect-oriented-programming-with-spring-aop)
{.links-list}
- [使用 Spring AOP 进行面向方面的编程***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/aspect-oriented-programming-with-spring-aop)
{.links-list}
- [Spring AOP를 사용한 관점 지향 프로그래밍***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/aspect-oriented-programming-with-spring-aop)
{.links-list}


# Aspect-Oriented Programming with Spring AOP

Aspect-oriented programming (AOP) is a programming paradigm that aims to increase modularity by allowing the separation of cross-cutting concerns. AOP forms the basis of enterprise application frameworks such as Spring AOP.

Spring AOP is a powerful tool for aspect-oriented programming in Java. It allows you to modularize cross-cutting concerns in separate aspects and apply them to beans deployed in a Spring application context. In this article, we'll take a look at how to use Spring AOP to implement common AOP use cases such as logging, auditing, and performance monitoring.

We'll start with a simple example of how to use Spring AOP to log method execution time. Then we'll see how to use pointcuts and advices to apply aspects to beans in a Spring application context.

## Logging Method Execution Time

Suppose we have a simple service that we want to log the execution time of each method:

```java
public class MyService {

    public void doWork() {
        // do some work
    }
}
```

We can use Spring AOP to log the execution time of each method in this service with the following aspect:

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

The `@Around` annotation indicates that this is an around advice. The pointcut expression `execution(* com.example.myservice.*.*(..))` tells Spring AOP to apply this aspect to all methods in the `com.example.myservice` package.

The `logExecutionTime()` method is the actual advice. It takes a `ProceedingJoinPoint` as an argument, which represents the method being advised. The `logExecutionTime()` method first gets the current time in milliseconds, then calls the `proceed()` method on the join point to execute the advised method, and finally computes the elapsed time and prints it to the console.

To apply this aspect to our `MyService` class, we need to add the `@EnableAspectJAutoProxy` annotation to our configuration:

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

The `@EnableAspectJAutoProxy` annotation enables Spring's auto-proxy mechanism, which proxys beans with aspects so that the aspects are applied to them.

We can then use the `MyService` bean in our application:

```java
public class App {

    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        MyService myService = context.getBean(MyService.class);
        myService.doWork();
    }
}
```

When we run this application, we see the following output:

```
void com.example.myservice.MyService.doWork() executed in 0ms
```

We can also use the `@Around` advice to implement other AOP use cases such as auditing and performance monitoring.

## Applying Aspects to Beans

In the previous section, we saw how to use the `@Around` advice to log method execution time. But what if we want to apply this aspect to only some of the beans in our application? We can do this by using pointcuts andadvices.

A pointcut is a predicate that matches join points. A join point is a point in the execution of a program where an aspect can be plugged in. In Spring AOP, a join point always represents a method invocation.

An advice is associated with a pointcut and is executed when a join point matched by the pointcut is reached. There are four types of advices in Spring AOP:

- `@Before`: executed before the join point
- `@After`: executed after the join point, whether or not it throws an exception
- `@AfterReturning`: executed after the join point completes normally
- `@AfterThrowing`: executed after the join point throws an exception

We can use pointcuts and advices to selectively apply aspects to beans in our application. For example, suppose we want to apply the `LoggingAspect` only to beans whose names start with `myService`. We can do this with the following configuration:

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

Here we've annotated the `loggingAspect()` method with `@Pointcut`, which tells Spring AOP to apply this aspect to all beans whose names start with `myService`. We've also annotated the aspect bean with `@Lazy` and `@Scope("prototype")` to ensure that the aspect is applied only to beans that are instantiated by the application context.

With this configuration in place, the `LoggingAspect` will be applied only to beans whose names start with `myService`.

## Conclusion

In this article, we've seen how to use Spring AOP to implement common AOP use cases such as logging, auditing, and performance monitoring. We've also seen how to use pointcuts and advices to selectively apply aspects to beans in our application context.

With Spring AOP, we can modularize our concerns and apply them to the beans in our application in a consistent and declarative way.