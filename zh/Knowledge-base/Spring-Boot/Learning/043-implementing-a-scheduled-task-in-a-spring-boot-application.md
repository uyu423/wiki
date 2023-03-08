---
title: 043：在Spring Boot应用中实现定时任务
description: 
published: true
date: 2023-02-04T09:32:17.557Z
tags: 
editor: markdown
dateCreated: 2023-02-04T09:32:12.329Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [043: Implementing a scheduled task in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/043-implementing-a-scheduled-task-in-a-spring-boot-application)
{.links-list}


# 在 Spring Boot 应用中实现定时任务

在这篇文章中，我们将讨论如何在 Spring Boot 应用程序中实现计划任务。 Spring Boot 提供了一种简单方便的方式来运行计划任务。

## 调度任务

Spring Boot 提供了一个 @Scheduled 注释，可以在方法上使用它来将它们标记为应该定期运行的任务。例如，我们可以使用@Scheduled 注解每分钟运行一个任务：

```java
@Scheduled(cron = "0 * * * * ?")
public void runEveryMinute() {
    // do something
}
```

在上面的示例中，我们使用 cron 表达式来安排任务。 Cron 表达式是指定何时运行任务的便捷方式。有关 cron 表达式的更多信息，请参阅 [CronTrigger](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/scheduling/support/CronTrigger.html) javadoc。

## 在 Spring Boot 应用程序中运行任务

要在我们的 Spring Boot 应用程序中运行任务，我们只需要使用 @EnableScheduling 注释来注释我们的主类：

```java
@SpringBootApplication
@EnableScheduling
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

## 附加信息

- 有关 Spring Boot 中调度任务的更多信息，请参阅 [Spring Boot 文档](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-scheduling.html)。
- 有关使用 @Scheduled 注释的更多信息，请参阅 [Spring 文档](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/scheduling/annotation/Scheduled.html) .