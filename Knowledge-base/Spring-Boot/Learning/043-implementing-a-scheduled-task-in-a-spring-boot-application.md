---
title: 043: Spring Boot 애플리케이션에서 예약된 작업 구현
description: 
published: true
date: 2023-02-04T09:32:17.557Z
tags: 
editor: markdown
dateCreated: 2023-02-04T09:32:12.331Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [043: Implementing a scheduled task in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/043-implementing-a-scheduled-task-in-a-spring-boot-application)
{.links-list}


# Spring Boot 애플리케이션에서 예약된 작업 구현

이 게시물에서는 Spring Boot 애플리케이션에서 예약된 작업을 구현하는 방법을 살펴보겠습니다. Spring Boot는 예약된 작업을 실행하는 간단하고 편리한 방법을 제공합니다.

## 예약 작업

Spring Boot는 주기적으로 실행해야 하는 작업으로 표시하기 위해 메서드에 사용할 수 있는 @Scheduled 주석을 제공합니다. 예를 들어 @Scheduled 주석을 사용하여 매분 작업을 실행할 수 있습니다.

```java
@Scheduled(cron = "0 * * * * ?")
public void runEveryMinute() {
    // do something
}
```

위의 예에서는 cron 표현식을 사용하여 작업을 예약합니다. Cron 표현식은 작업을 실행해야 하는 시기를 지정하는 편리한 방법입니다. cron 식에 대한 자세한 내용은 [CronTrigger](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/scheduling/support/CronTrigger.html) javadocs를 참조하세요.

## Spring Boot 애플리케이션에서 작업 실행

Spring Boot 애플리케이션에서 작업을 실행하려면 메인 클래스에 @EnableScheduling 주석을 추가하기만 하면 됩니다.

```java
@SpringBootApplication
@EnableScheduling
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

## 추가 정보

- Spring Boot에서 작업 예약에 대한 자세한 내용은 [Spring Boot 설명서](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-scheduling.html)를 참조하세요.
- @Scheduled 주석 사용에 대한 자세한 내용은 [Spring 설명서](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/scheduling/annotation/Scheduled.html)를 참조하십시오. .