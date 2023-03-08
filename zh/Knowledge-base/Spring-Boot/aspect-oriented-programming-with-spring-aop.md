---
title: 使用 Spring AOP 进行面向方面的编程
description: 
published: true
date: 2023-02-07T00:32:34.280Z
tags: 
editor: markdown
dateCreated: 2023-02-07T00:32:32.675Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Aspect-Oriented Programming with Spring AOP***English** document is available*](/en/Knowledge-base/Spring-Boot/aspect-oriented-programming-with-spring-aop)
{.links-list}


# 使用 Spring AOP 进行面向方面的编程

面向方面的编程 (AOP) 是一种编程范例，旨在通过允许分离横切关注点来提高模块化。 AOP 构成了诸如 Spring AOP 之类的企业应用程序框架的基础。

Spring AOP 是 Java 中面向方面编程的强大工具。它允许您在单独的方面模块化横切关注点，并将它们应用于部署在 Spring 应用程序上下文中的 bean。在本文中，我们将了解如何使用 Spring AOP 实现常见的 AOP 用例，例如日志记录、审计和性能监控。

我们将从一个简单的示例开始，说明如何使用 Spring AOP 来记录方法执行时间。然后我们将看到如何使用切入点和建议将方面应用到 Spring 应用程序上下文中的 bean。

## 记录方法执行时间

假设我们有一个简单的服务，我们想要记录每个方法的执行时间：

```java
public class MyService {

    public void doWork() {
        // do some work
    }
}
```

我们可以使用 Spring AOP 从以下方面记录此服务中每个方法的执行时间：

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

`@Around` 注释表示这是一个环绕建议。切入点表达式 execution(* com.example.myservice.*.*(..)) 告诉 Spring AOP 将此方面应用于 com.example.myservice 包中的所有方法。

`logExecutionTime()` 方法是实际的建议。它以“ProceedingJoinPoint”作为参数，代表被建议的方法。 `logExecutionTime()` 方法首先获取当前时间（以毫秒为单位），然后调用连接点上的 `proceed()` 方法执行建议的方法，最后计算经过的时间并将其打印到控制台。

要将此方面应用于我们的“MyService”类，我们需要将“@EnableAspectJAutoProxy”注释添加到我们的配置中：

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

`@EnableAspectJAutoProxy` 注释启用 Spring 的自动代理机制，该机制使用方面代理 bean，以便将方面应用于它们。

然后我们可以在我们的应用程序中使用 MyService bean：

```java
public class App {

    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        MyService myService = context.getBean(MyService.class);
        myService.doWork();
    }
}
```

当我们运行这个应用程序时，我们会看到以下输出：

```
void com.example.myservice.MyService.doWork() executed in 0ms
```

我们还可以使用 @Around 通知来实现其他 AOP 用例，例如审计和性能监控。

## 将方面应用到 Bean

在上一节中，我们了解了如何使用“@Around”通知来记录方法执行时间。但是，如果我们只想将这个方面应用到我们应用程序中的某些 bean 怎么办？我们可以通过使用切入点和建议来做到这一点。

切入点是匹配连接点的谓词。连接点是程序执行中可以插入方面的点。在 Spring AOP 中，连接点始终表示方法调用。

建议与切入点相关联，并在到达切入点匹配的连接点时执行。 Spring AOP 中有四种类型的通知：

- `@Before`：在连接点之前执行
- `@After`：在连接点之后执行，无论是否抛出异常
- `@AfterReturning`：在连接点正常完成后执行
- `@AfterThrowing`：在连接点抛出异常后执行

我们可以使用切入点和建议来有选择地将方面应用到我们应用程序中的 bean。例如，假设我们只想将 `LoggingAspect` 应用于名称以 `myService` 开头的 bean。我们可以使用以下配置来做到这一点：

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

这里我们用 @Pointcut 注释了 loggingAspect() 方法，它告诉 Spring AOP 将这个方面应用于名称以 myService 开头的所有 bean。我们还使用 @Lazy 和 @Scope("prototype") 注释了方面 bean，以确保方面仅应用于由应用程序上下文实例化的 bean。

有了这个配置，“LoggingAspect”将只应用于名称以“myService”开头的 bean。

## 结论

在本文中，我们了解了如何使用 Spring AOP 实现常见的 AOP 用例，例如日志记录、审计和性能监控。我们还了解了如何使用切入点和建议来有选择地将方面应用到应用程序上下文中的 bean。

使用 Spring AOP，我们可以模块化我们的关注点，并以一致和声明的方式将它们应用到我们应用程序中的 bean。