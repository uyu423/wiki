---
title: Spring Boot 中的命令查询责任分离 (CQRS) 模式
description: 
published: true
date: 2023-02-01T15:03:44.372Z
tags: 
editor: markdown
dateCreated: 2023-02-01T15:03:42.631Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [The Command Query Responsibility Segregation (CQRS) Pattern in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-command-query-responsibility-segregation-cqrs-pattern-in-spring-boot)
{.links-list}


# Spring Boot 中的命令查询责任分离 (CQRS) 模式

命令查询责任分离 (CQRS) 是一种架构模式，它将处理命令（更改系统状态的请求）的责任与处理查询（从系统返回信息的请求）的责任分开。

这种关注点分离可以提供多种好处，例如改进的性能、可伸缩性和可维护性。

在 CQRS 架构中，命令通常由与处理查询的服务不同的服务处理。这种分离可以用不同的方式实现，但一种常见的方法是使用不同的数据库表来存储命令访问的数据和查询访问的数据。

Spring Boot 是一种用于构建 Web 应用程序的流行 Java 框架。它提供了一种方便的方法来创建独立的、生产级的基于 Spring 的应用程序，这些应用程序可以“直接运行”。

在本文中，我们将了解如何在 Spring Boot 应用程序中实现 CQRS 架构。我们将从查看此类应用程序中涉及的不同组件开始。然后，我们将实现一个使用 CQRS 的简单示例应用程序。

## CQRS 应用程序的组件

CQRS 应用程序通常具有以下组件：

- **命令：**这些是更改系统状态的请求。在我们的示例应用程序中，我们将拥有用于创建和更新任务的命令。
- **查询：**这些是从系统返回信息的请求。在我们的示例应用程序中，我们将查询获取所有任务的列表以及获取特定任务的详细信息。
- **命令服务：**这是处理命令的服务。在我们的示例应用程序中，此服务将负责验证命令并执行它们。
- **查询服务：**这是处理查询的服务。在我们的示例应用程序中，该服务将负责执行查询并将结果返回给调用者。
- **Repository：**这是一个数据访问层，提供访问数据存储的接口。在我们的示例应用程序中，我们将使用存储库来访问任务数据。
- **模型：**这是应用程序的域模型。在我们的示例应用程序中，任务将是唯一的模型对象。


## 使用 Spring Boot 实现 CQRS 应用程序

现在我们已经了解了 CQRS 应用程序的不同组件，让我们实现一个使用 CQRS 的简单示例应用程序。

我们的示例应用程序将是一个任务管理器。用户将能够创建任务并将它们分配给自己或其他用户。他们还可以将任务标记为已完成。

我们将从实施命令服务开始。该服务将负责验证和执行命令。

### 命令服务

命令服务将具有以下方法：

- **createTask(Task task)**：此方法将用于创建任务。
- **updateTask(Task task)**：此方法将用于更新任务。
- **markTaskAsComplete(String taskId)**：此方法将用于将任务标记为已完成。

我们将在一个名为 **TaskCommandService** 的类中实现这些方法。这个类会被注解为**@Service**，这是一个Spring注解，将类标记为服务组件。

```java
@Service
public class TaskCommandService {

    public void createTask(Task task) {
        // validate the task
        // save the task
    }

    public void updateTask(Task task) {
        // validate the task
        // save the task
    }

    public void markTaskAsComplete(String taskId) {
        // validate the task
        // mark the task as complete
        // save the task
    }
}
```

如您所见，**createTask** 和 **updateTask** 方法接受一个 **Task** 对象作为参数。该对象将用于保存正在创建或更新的任务的数据。

**markTaskAsComplete** 方法接受任务 ID 作为参数。此任务 ID 将用于查找要标记为完成的任务。

这些方法中的每一个都以调用 **validate** 方法开始。此验证方法将负责验证传入的数据。我们将在下一节中实现此方法。

### 验证命令

**validate** 方法将负责验证传递给命令服务方法的数据。我们将在名为 **TaskCommandValidator** 的类中实现此方法。这个类会被注解为**@Component**，这是一个Spring注解，将一个类标记为一个组件。

```java
@Component
public class TaskCommandValidator {

    public void validate(Task task) {
        // validate the task
    }

    public void validate(String taskId) {
        // validate the task ID
    }
}
```

如您所见，此类有两个验证方法。这些方法之一接受 **Task** 对象作为参数。此方法将用于验证创建和更新任务的数据。

另一个验证方法接受任务 ID 作为参数。此方法将用于验证任务 ID 以将任务标记为已完成。

在实际应用程序中，这些验证方法将包含用于验证数据的逻辑。出于本示例的目的，我们将它们留空。

### 查询服务

查询服务将具有以下方法：

- **getAllTasks()**：此方法将用于获取所有任务的列表。
- **getTaskById(String taskId)**：此方法将用于获取特定任务的详细信息。

我们将在一个名为 **TaskQueryService** 的类中实现这些方法。这个类会被注解为**@Service**。

```java
@Service
public class TaskQueryService {

    public List<Task> getAllTasks() {
        // execute query
        // return results
    }

    public Task getTaskById(String taskId) {
        // execute query
        // return results
    }
}
```

如您所见，**getAllTasks** 方法返回一个**Task** 对象的列表。该列表将包含系统中所有任务的数据。

**getTaskById** 方法返回单个 **Task** 对象。该对象将包含具有指定 ID 的任务的数据。

### 存储库

存储库是一个数据访问层，提供用于访问数据存储的接口。在我们的示例应用程序中，我们将使用存储库来访问任务数据。

我们将在一个名为 **TaskRepository** 的类中实现存储库。这个类将被注解为**@Repository**，这是一个Spring注解，将类标记为存储库组件。

```java
@Repository
public class TaskRepository {

    public void save(Task task) {
        // save the task
    }

    public Task findById(String id) {
        // find the task
        // return the task
    }

    public List<Task> findAll() {
        // find all tasks
        // return the tasks
    }
}
```

如您所见，此存储库具有保存、查找和删除任务的方法。

### 该模型

该模型是应用程序的领域模型。在我们的示例应用程序中，任务将是唯一的模型对象。

我们将在一个名为 **Task** 的类中实现任务模型。此类将使用 **@Entity** 注释，这是将类标记为实体的 JPA 注释。

```java
@Entity
public class Task {

    @Id
    private String id;

    private String name;

    private String description;

    private boolean complete;

    // getters and setters
}
```

正如您所看到的，这个任务模型有四个字段：id、name、description 和 complete。 id字段使用**@Id**注解，这是一个JPA注解，将一个字段标记为实体的主键。

### 把它们放在一起

现在我们已经实现了 CQRS 应用程序的不同组件，让我们将它们放在一起看看它是如何工作的。

我们将从创建任务开始。为此，我们将首先创建一个 **Task** 对象并使用任务数据填充它。然后，我们将把这个对象传递给 **TaskCommandService** 的 **createTask** 方法。

```java
Task task = new Task();
task.setName("Write example");
task.setDescription("Write an example of the CQRS pattern");

taskCommandService.createTask(task);
```

这将在系统中创建一个新任务。

现在，假设我们想要获得所有任务的列表。为此，我们将调用 **TaskQueryService** 的 **getAllTasks** 方法。

```java
List<Task> tasks = taskQueryService.getAllTasks();
```

这将返回系统中所有任务的列表。

最后，假设我们要将任务标记为完成。为此，我们将首先通过 ID 获取任务。然后，我们将调用 **TaskCommandService** 的 **markTaskAsComplete** 方法。

```java
Task task = taskQueryService.getTaskById("1");

taskCommandService.markTaskAsComplete(task.getId());
```

这会将 ID 为“1”的任务标记为已完成。

## 结论

在本文中，我们了解了命令查询责任分离 (CQRS) 模式以及如何在 Spring Boot 应用程序中实现它。

我们还看到了这种模式如何提供多种好处，例如改进的性能、可伸缩性和可维护性。

如果您有兴趣了解有关 CQRS 的更多信息，我推荐以下资源：

- [CQRS：好的、坏的和丑陋的](https://martinfowler.com/bliki/CQRS.html)
- [命令查询职责分离](https://en.wikipedia.org/wiki/Command%E2%80%93query_separation)
- [为什么使用 CQRS？](https://docs.microsoft.com/en-us/azure/architecture/patterns/cqrs)