---
title: 099: Building a Scheduling System with Spring Boot and Quartz
description: 
published: true
date: 2023-02-06T03:32:32.997Z
tags: 
editor: markdown
dateCreated: 2023-02-06T03:32:27.113Z
---

- [099: Creación de un sistema de programación con Spring Boot y Quartz***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/099-building-a-scheduling-system-with-spring-boot-and-quartz)
{.links-list}
- [099：使用 Spring Boot 和 Quartz 构建调度系统***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/099-building-a-scheduling-system-with-spring-boot-and-quartz)
{.links-list}
- [099: Spring Boot와 Quartz로 스케줄링 시스템 구축하기***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/099-building-a-scheduling-system-with-spring-boot-and-quartz)
{.links-list}


# 099: Building a Scheduling System with Spring Boot and Quartz

Quartz is a powerful and widely used scheduling library that can be integrated with Spring Boot to schedule tasks in our applications. In this post, we'll go over how to build a scheduling system with Spring Boot and Quartz.

## Prerequisites

Before getting started, you'll need to have the following installed on your machine:

- Java 8
- Maven 3.x

## Setting up the project

Let's start by setting up our project. We'll be using Spring Boot for our example, so we'll need to create a new Maven project with the following dependencies:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-quartz</artifactId>
    </dependency>
</dependencies>
```

## Configuring Quartz

Next, we need to configure Quartz. We can do this by creating a new file called `quartz.properties` in the `src/main/resources` directory with the following contents:

```properties
org.quartz.scheduler.instanceName=MyScheduler
org.quartz.scheduler.instanceId=AUTO

org.quartz.threadPool.threadCount=5

org.quartz.jobStore.class=org.quartz.simpl.RAMJobStore
```

This will configure Quartz with a few basic settings. For more information on configuring Quartz, please see the [Quartz documentation](http://www.quartz-scheduler.org/documentation/quartz-2.x/configuration/).

## Creating a job

Now that we have Quartz configured, let's create a job. Jobs in Quartz are simple Java classes that implement the `org.quartz.Job` interface. For our example, we'll create a job that simply prints out a message to the console.

```java
public class MyJob implements Job {

    @Override
    public void execute(JobExecutionContext context) throws JobExecutionException {
        System.out.println("Hello, world!");
    }

}
```

## Scheduling a job

Now that we have a job, we need to schedule it. There are two ways to do this: via code or via annotations.

### Scheduling a job via code

To schedule a job via code, we need to do the following:

1. Create a `org.quartz.Trigger` instance that defines when the job should run.
2. Register the job and trigger with the Quartz scheduler.

Here's an example of how to do this:

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

In the code above, we've created a `MyJobScheduler` component that schedules a `MyJob` instance to run every 5 seconds.

### Scheduling a job via annotations

Alternatively, we can schedule a job via annotations. To do this, we simply need to annotate our `MyJob` class with `@DisallowConcurrentExecution` and `@Scheduled`.

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

In the code above, we've annotated our `MyJob` class with `@DisallowConcurrentExecution` to ensure that only one instance of the job is running at a time. We've also annotated it with `@Scheduled`, which takes a cron expression that defines when the job should run. In this case, we're running the job every 5 seconds.

## Running the example

Now that we have our project set up, let's run it and see our job in action! To do this, simply run the `main` method in the `MyJobScheduler` class. You should see the following output:

```
Hello, world!
Hello, world!
Hello, world!
...
```

## Conclusion

In this post, we've gone over how to build a scheduling system with Spring Boot and Quartz. We've seen how to configure Quartz and how to schedule jobs via code or annotations.

For more information on Quartz, please see the [Quartz documentation](http://www.quartz-scheduler.org/documentation/quartz-2.x/).