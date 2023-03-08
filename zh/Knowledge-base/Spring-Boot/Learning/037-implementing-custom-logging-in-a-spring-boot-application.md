---
title: 037：在 Spring Boot 应用程序中实现自定义日志记录
description: 
published: true
date: 2023-02-04T05:32:25.749Z
tags: 
editor: markdown
dateCreated: 2023-02-04T05:32:24.127Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [037: Implementing custom logging in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/037-implementing-custom-logging-in-a-spring-boot-application)
{.links-list}


# 在 Spring Boot 应用程序中实现自定义日志记录

在本文中，我们将了解如何在 Spring Boot 应用程序中实现自定义日志记录。我们将涵盖以下主题：

* 为 Spring Boot 应用程序配置 Log4j2
* 创建自定义 Log4j2 appender
* 使用自定义附加程序将事件记录到数据库

## 为 Spring Boot 应用程序配置 Log4j2

Log4j2 是一个流行的 Java 应用程序日志记录库。 Spring Boot 开箱即用地提供了对 Log4j2 的支持。为了为 Spring Boot 应用程序配置 Log4j2，我们需要将 Log4j2 配置文件添加到类路径中。 Log4j2 配置文件必须命名为 log4j2.xml 或 log4j2.yaml。

这是一个简单的 Log4j2 配置文件，它将所有消息记录到控制台：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="warn">
  <Appenders>
    <Console name="Console" target="SYSTEM_OUT">
      <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
  </Appenders>
  <Loggers>
    <Root level="info">
      <AppenderRef ref="Console"/>
    </Root>
  </Loggers>
</Configuration>
```

在 Log4j2 配置文件中，我们需要指定要使用的附加程序。在这个例子中，我们使用一个控制台附加程序，它将所有消息记录到控制台。我们还需要指定我们想要使用的记录器。在此示例中，我们使用根记录器并引用我们之前定义的控制台附加程序。

## 创建自定义 Log4j2 appender

为了将事件记录到数据库中，我们需要创建一个自定义的 Log4j2 appender。 Log4j2 appender 是一个插件，它允许我们指定我们希望将日志写入的位置。在我们的例子中，我们想将日志写入数据库。

我们的自定义 appender 需要实现以下接口：

```java
public interface Appender {
 
    void start();
 
    void stop();
 
    boolean isStarted();
 
    void append(LogEvent event);
 
    Layout getLayout();
 
    void setLayout(Layout layout);
 
    ErrorHandler getErrorHandler();
 
    void setErrorHandler(ErrorHandler errorHandler);
 
    Name getName();
 
    boolean ignoresThrowable();
}
```

我们可以从创建自定义 appender 的框架实现开始：

```java
public class DatabaseAppender implements Appender {
 
    @Override
    public void start() {
 
    }
 
    @Override
    public void stop() {
 
    }
 
    @Override
    public boolean isStarted() {
        return false;
    }
 
    @Override
    public void append(LogEvent event) {
 
    }
 
    @Override
    public Layout getLayout() {
        return null;
    }
 
    @Override
    public void setLayout(Layout layout) {
 
    }
 
    @Override
    public ErrorHandler getErrorHandler() {
        return null;
    }
 
    @Override
    public void setErrorHandler(ErrorHandler errorHandler) {
 
    }
 
    @Override
    public Name getName() {
        return null;
    }
 
    @Override
    public boolean ignoresThrowable() {
        return false;
    }
}
```

在 start() 方法中，我们需要初始化我们的数据库连接。在 stop() 方法中，我们需要关闭数据库连接。在 append() 方法中，我们需要将日志事件插入到数据库中。

## 使用自定义附加程序将事件记录到数据库

现在我们有了自定义 appender，我们需要配置 Log4j2 来使用它。我们可以通过将以下内容添加到我们的 Log4j2 配置文件来做到这一点：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration status="warn">
  <Appenders>
    <Console name="Console" target="SYSTEM_OUT">
      <PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
 
    <DatabaseAppender name="DatabaseAppender">
      <ConnectionString>jdbc:mysql://localhost:3306/test</ConnectionString>
      <DriverClassName>com.mysql.jdbc.Driver</DriverClassName>
      <UserName>root</UserName>
      <Password>root</Password>
    </DatabaseAppender>
  </Appenders>
 
  <Loggers>
    <Root level="info">
      <AppenderRef ref="Console"/>
      <AppenderRef ref="DatabaseAppender"/>
    </Root>
  </Loggers>
</Configuration>
```

在 Log4j2 配置文件中，我们添加了一个 <DatabaseAppender> 元素。这个元素有一些我们需要设置的属性：

* ConnectionString：我们数据库的 JDBC 连接字符串
* DriverClassName: JDBC驱动类的名称
* UserName: 数据库用户名
* 密码：数据库密码

我们还向根记录器添加了一个 <AppenderRef> 元素。这个元素引用了我们的 DatabaseAppender。

现在我们已经配置了自定义 appender，我们可以使用它来将事件记录到我们的数据库中。