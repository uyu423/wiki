---
title: Spring Boot开发中的装饰者模式
description: 
published: true
date: 2023-02-08T16:32:25.881Z
tags: 
editor: markdown
dateCreated: 2023-02-08T16:32:24.338Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [The Decorator Pattern in Spring Boot Development***English** document is available*](/en/Knowledge-base/Spring-Boot/the-decorator-pattern-in-spring-boot-development)
{.links-list}


# Spring Boot开发中的装饰者模式

装饰者模式是一种软件设计模式，允许在不改变现有对象核心功能的情况下修改现有对象。这是通过用包含所需功能的装饰器对象包装原始对象来实现的。

在 Spring Boot 中，装饰器模式可用于在不更改代码的情况下向现有 bean 动态添加新功能。这是通过用包含所需功能的装饰器 bean 包装原始 bean 来完成的。

例如，假设我们有一个包含消息的简单 bean：

```java
public class MessageBean {
  
  private String message;
  
  public MessageBean(String message) {
    this.message = message;
  }
  
  public String getMessage() {
    return message;
  }
}
```

我们可以使用装饰器模式动态地向这个 bean 添加新功能，而无需更改其代码。例如，我们可以创建一个为消息添加时间戳的装饰器 bean：

```java
public class TimestampDecorator implements MessageBean {
  
  private MessageBean messageBean;
  
  public TimestampDecorator(MessageBean messageBean) {
    this.messageBean = messageBean;
  }
  
  @Override
  public String getMessage() {
    return messageBean.getMessage() + " - " + new Date();
  }
}
```

现在，当我们将 MessageBean 注入我们的代码时，我们可以指定我们想要使用 TimestampDecorator：

```java
@Autowired
@Qualifier("timestampDecorator")
private MessageBean messageBean;
```

当我们调用 getMessage() 方法时，这会将当前时间戳添加到消息中：

```java
messageBean.getMessage(); // "Hello World! - Thu Jan 01 00:00:00 EST 1970"
```

Decorator Pattern 是一种有用的方法，可以在不更改代码的情况下向现有 bean 动态添加新功能。这可用于添加时间戳、日志记录、安全性或任何其他所需功能。