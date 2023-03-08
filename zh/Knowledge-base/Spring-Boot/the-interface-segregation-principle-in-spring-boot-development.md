---
title: Spring Boot开发中的接口隔离原则
description: 
published: true
date: 2023-02-04T02:17:22.379Z
tags: 
editor: markdown
dateCreated: 2023-02-04T02:17:20.760Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [The Interface Segregation Principle in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-interface-segregation-principle-in-spring-boot-development)
{.links-list}


# Spring Boot开发中的接口隔离原则

接口隔离原则 (Interface Segregation Principle, ISP) 是一项软件设计原则，规定不应强迫任何客户端依赖它不使用的方法。

换句话说，最好保持接口小而集中，以便它们可以由需要它们的类实现，而不依赖于未使用的方法。

该原则首先由 Robert C. Martin 在他的《敏捷软件开发、原则、模式和实践》一书中定义。

## 应用接口隔离原则

在设计软件时，重要的是要牢记 ISP，这样接口就不会太大或太笼统。

例如，考虑一个用户服务的接口，它包括创建、更新和删除用户的方法。

```java
public interface UserService {
    
    public void createUser(User user);
    
    public void updateUser(User user);
    
    public void deleteUser(User user);
    
}
```

实现此接口的类需要为所有三种方法提供实现，即使它只需要支持用户创建。

更好的设计是为每种类型的操作提供单独的接口。

```java
public interface UserService {
    
    public void createUser(User user);
    
}

public interface UserUpdateService {
    
    public void updateUser(User user);
    
}

public interface UserDeleteService {
    
    public void deleteUser(User user);
    
}
```

这种设计更符合ISP，因为每个接口都专注于一个特定的任务。

一个只需要支持用户创建的类可以实现 ```UserService``` 接口而不依赖于其他接口。

## Spring Boot 与接口隔离原则

Spring Boot 是用于开发 Java 应用程序的流行框架。

它基于约定优于配置的原则，这意味着它倾向于约定优于显式配置。

这个原则可以应用到接口的设计中。

例如，考虑一个具有 ```UserService``` 接口的 Spring Boot 应用程序。

```java
@Service
public interface UserService {
    
    public void createUser(User user);
    
}
```

```@Service``` 注释用于指示此接口是 Spring 服务。

Spring 会自动为这个接口创建一个 bean，并将它注入到任何需要它的组件中。

这种设计符合 ISP，因为接口专注于特定任务（用户创建），组件没有必要依赖未使用的方法。