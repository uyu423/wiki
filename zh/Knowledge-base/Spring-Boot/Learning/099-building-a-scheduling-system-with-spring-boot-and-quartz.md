---
title: 099：使用 Spring Boot 和 Quartz 构建调度系统
description: 
published: true
date: 2023-02-06T03:32:28.970Z
tags: 
editor: markdown
dateCreated: 2023-02-06T03:32:27.106Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [099: Building a Scheduling System with Spring Boot and Quartz***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/099-building-a-scheduling-system-with-spring-boot-and-quartz)
{.links-list}


# 099：使用 Spring Boot 和 Quartz 构建调度系统

Quartz 是一个功能强大且使用广泛的调度库，可以与 Spring Boot 集成以在我们的应用程序中调度任务。在这篇文章中，我们将讨论如何使用 Spring Boot 和 Quartz 构建一个调度系统。

## 先决条件

在开始之前，您需要在您的机器上安装以下软件：

- Java 8
- 行家 3.x

## 设置项目

让我们从设置我们的项目开始。我们将在示例中使用 Spring Boot，因此我们需要创建一个具有以下依赖项的新 Maven 项目：

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-quartz</artifactId>
    </dependency>
</dependencies>
```

## 配置石英

接下来，我们需要配置 Quartz。我们可以通过在 `src/main/resources` 目录中创建一个名为 `quartz.properties` 的新文件来做到这一点，其内容如下：

```properties
org.quartz.scheduler.instanceName=MyScheduler
org.quartz.scheduler.instanceId=AUTO

org.quartz.threadPool.threadCount=5

org.quartz.jobStore.class=org.quartz.simpl.RAMJobStore
```

这将使用一些基本设置配置 Quartz。有关配置 Quartz 的更多信息，请参阅 [Quartz 文档](http://www.quartz-scheduler.org/documentation/quartz-2.x/configuration/)。

## 创建工作

现在我们已经配置了 Quartz，让我们创建一个作业。 Quartz 中的作业是实现 org.quartz.Job 接口的简单 Java 类。对于我们的示例，我们将创建一个简单地向控制台打印消息的作业。

```java
public class MyJob implements Job {

    @Override
    public void execute(JobExecutionContext context) throws JobExecutionException {
        System.out.println("Hello, world!");
    }

}
```

## 安排工作

现在我们有了工作，我们需要安排它。有两种方法可以做到这一点：通过代码或通过注释。

### 通过代码安排工作

要通过代码安排作业，我们需要执行以下操作：

1. 创建一个 org.quartz.Trigger 实例来定义作业何时运行。
2. 使用 Quartz 调度程序注册作业和触发器。

这是如何执行此操作的示例：

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

在上面的代码中，我们创建了一个 MyJobScheduler 组件，它安排一个 MyJob 实例每 5 秒运行一次。

### 通过注解安排工作

或者，我们可以通过注释安排工作。为此，我们只需要用“@DisallowConcurrentExecution”和“@Scheduled”注释我们的“MyJob”类。

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

在上面的代码中，我们用 @DisallowConcurrentExecution 注释了我们的 MyJob 类，以确保一次只有一个作业实例在运行。我们还用“@Scheduled”对其进行了注释，它采用一个 cron 表达式来定义作业何时应该运行。在这种情况下，我们每 5 秒运行一次作业。

## 运行示例

现在我们已经设置了项目，让我们运行它并查看我们的工作！为此，只需运行 MyJobScheduler 类中的 main 方法即可。您应该看到以下输出：

```
Hello, world!
Hello, world!
Hello, world!
...
```

## 结论

在这篇文章中，我们介绍了如何使用 Spring Boot 和 Quartz 构建调度系统。我们已经了解了如何配置 Quartz 以及如何通过代码或注释来安排作业。

有关 Quartz 的更多信息，请参阅 [Quartz 文档](http://www.quartz-scheduler.org/documentation/quartz-2.x/)。