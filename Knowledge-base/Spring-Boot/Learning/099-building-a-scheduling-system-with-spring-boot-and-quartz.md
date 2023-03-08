---
title: 099: Spring Boot와 Quartz로 스케줄링 시스템 구축하기
description: 
published: true
date: 2023-02-06T03:32:28.776Z
tags: 
editor: markdown
dateCreated: 2023-02-06T03:32:27.106Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [099: Building a Scheduling System with Spring Boot and Quartz***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/099-building-a-scheduling-system-with-spring-boot-and-quartz)
{.links-list}


# 099: Spring Boot와 Quartz로 스케줄링 시스템 구축하기

Quartz는 애플리케이션에서 작업을 예약하기 위해 Spring Boot와 통합할 수 있는 강력하고 널리 사용되는 예약 라이브러리입니다. 이번 포스트에서는 Spring Boot와 Quartz로 스케줄링 시스템을 구축하는 방법에 대해 알아보겠습니다.

## 전제 조건

시작하기 전에 컴퓨터에 다음을 설치해야 합니다.

- 자바 8
- 메이븐 3.x

## 프로젝트 설정

프로젝트를 설정하여 시작하겠습니다. 예제에서는 Spring Boot를 사용할 것이므로 다음 종속성을 포함하는 새 Maven 프로젝트를 생성해야 합니다.

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-quartz</artifactId>
    </dependency>
</dependencies>
```

## 석영 구성

다음으로 Quartz를 구성해야 합니다. 다음 내용으로 `src/main/resources` 디렉토리에 `quartz.properties`라는 새 파일을 생성하여 이를 수행할 수 있습니다.

```properties
org.quartz.scheduler.instanceName=MyScheduler
org.quartz.scheduler.instanceId=AUTO

org.quartz.threadPool.threadCount=5

org.quartz.jobStore.class=org.quartz.simpl.RAMJobStore
```

몇 가지 기본 설정으로 Quartz를 구성합니다. Quartz 구성에 대한 자세한 내용은 [Quartz 설명서](http://www.quartz-scheduler.org/documentation/quartz-2.x/configuration/)를 참조하십시오.

## 직업 만들기

이제 Quartz를 구성했으므로 작업을 생성해 보겠습니다. Quartz의 작업은 `org.quartz.Job` 인터페이스를 구현하는 간단한 Java 클래스입니다. 이 예에서는 단순히 메시지를 콘솔에 출력하는 작업을 생성합니다.

```java
public class MyJob implements Job {

    @Override
    public void execute(JobExecutionContext context) throws JobExecutionException {
        System.out.println("Hello, world!");
    }

}
```

## 작업 일정 잡기

이제 일이 생겼으니 일정을 잡아야 합니다. 이를 수행하는 방법에는 코드를 통해 또는 주석을 통해 두 가지가 있습니다.

### 코드를 통해 작업 예약

코드를 통해 작업을 예약하려면 다음을 수행해야 합니다.

1. 작업 실행 시기를 정의하는 `org.quartz.Trigger` 인스턴스를 생성합니다.
2. Quartz 스케줄러에 작업 및 트리거를 등록합니다.

다음은 이를 수행하는 방법의 예입니다.

```java
@Component
public class MyJobScheduler {

    @Autowired
    private Scheduler scheduler;

    public void scheduleJob() throws SchedulerException {
        JobDetail job = JobBuilder.newJob(MyJob.class)
            .withIdentity("myJob", "group1")
            .build();

        Trigger trigger = TriggerBuilder.newTrigger()
            .withIdentity("myTrigger", "group1")
            .startNow()
            .withSchedule(SimpleScheduleBuilder.simpleSchedule()
                .withIntervalInSeconds(5)
                .repeatForever())
            .build();

        scheduler.scheduleJob(job, trigger);
    }
}
```

위의 코드에서 `MyJob` 인스턴스가 5초마다 실행되도록 예약하는 `MyJobScheduler` 구성 요소를 만들었습니다.

### 주석을 통한 작업 예약

또는 주석을 통해 작업을 예약할 수 있습니다. 이렇게 하려면 `@DisallowConcurrentExecution` 및 `@Scheduled`로 `MyJob` 클래스에 주석을 달기만 하면 됩니다.

```java
@DisallowConcurrentExecution
@Scheduled(cron = "0/5 * * * * ?")
public class MyJob implements Job {

    @Override
    public void execute(JobExecutionContext context) throws JobExecutionException {
        System.out.println("Hello, world!");
    }

}
```

위의 코드에서 한 번에 하나의 작업 인스턴스만 실행되도록 `@DisallowConcurrentExecution`을 사용하여 `MyJob` 클래스에 주석을 달았습니다. 또한 작업 실행 시기를 정의하는 cron 표현식을 사용하는 `@Scheduled`로 주석을 달았습니다. 이 경우 5초마다 작업을 실행합니다.

## 예제 실행

이제 프로젝트를 설정했으므로 실행하고 실제 작업을 살펴보겠습니다! 이렇게 하려면 `MyJobScheduler` 클래스에서 `main` 메소드를 실행하기만 하면 됩니다. 다음 출력이 표시되어야 합니다.

```
Hello, world!
Hello, world!
Hello, world!
...
```

## 결론

이번 포스팅에서는 Spring Boot와 Quartz로 스케줄링 시스템을 구축하는 방법에 대해 알아보았습니다. Quartz를 구성하는 방법과 코드 또는 주석을 통해 작업을 예약하는 방법을 살펴보았습니다.

Quartz에 대한 자세한 내용은 [Quartz 설명서](http://www.quartz-scheduler.org/documentation/quartz-2.x/)를 참조하십시오.