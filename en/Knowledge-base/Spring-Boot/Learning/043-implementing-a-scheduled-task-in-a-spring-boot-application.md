---
title: 043: Implementing a scheduled task in a Spring Boot application
description: 
published: true
date: 2023-02-04T09:32:13.984Z
tags: 
editor: markdown
dateCreated: 2023-02-04T09:32:12.342Z
---

- [043: Implementando una tarea programada en una aplicación Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/043-implementing-a-scheduled-task-in-a-spring-boot-application)
{.links-list}
- [043：在Spring Boot应用中实现定时任务***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/043-implementing-a-scheduled-task-in-a-spring-boot-application)
{.links-list}
- [043: Spring Boot 애플리케이션에서 예약된 작업 구현***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/043-implementing-a-scheduled-task-in-a-spring-boot-application)
{.links-list}


# Implementing a scheduled task in a Spring Boot application

In this post, we'll go over how to implement a scheduled task in a Spring Boot application. Spring Boot provides a simple and convenient way to run scheduled tasks.

## Scheduling Tasks

Spring Boot provides a @Scheduled annotation that can be used on methods to mark them as tasks that should be run periodically. For example, we can use the @Scheduled annotation to run a task every minute:

```java
@Scheduled(cron = "0 * * * * ?")
public void runEveryMinute() {
    // do something
}
```

In the example above, we are using a cron expression to schedule the task. Cron expressions are a convenient way to specify when a task should be run. For more information on cron expressions, see the [CronTrigger](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/scheduling/support/CronTrigger.html) javadocs.

## Running Tasks in a Spring Boot Application

To run the task in our Spring Boot application, we just need to annotate our main class with the @EnableScheduling annotation:

```java
@SpringBootApplication
@EnableScheduling
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

## Additional Information

- For more information on scheduling tasks in Spring Boot, see the [Spring Boot documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-scheduling.html).
- For more information on using the @Scheduled annotation, see the [Spring documentation](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/scheduling/annotation/Scheduled.html).