---
title: Spring Boot Logging
description: 
published: true
date: 2023-02-01T02:17:24.580Z
tags: 
editor: markdown
dateCreated: 2023-02-01T02:17:20.837Z
---

- [스프링 부트 로깅***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-logging)
{.links-list}
- [Spring Boot ロギング***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/spring-boot-logging)
{.links-list}
- [弹簧引导日志记录***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-logging)
{.links-list}



# Spring Boot Logging

Spring Boot makes it easy to configure logging for your application. By default, Spring Boot will configure the application to use the `java.util.logging` (JUL) logging framework. This can be changed to use Log4j2, Logback, or slf4j by adding the appropriate starter dependency to the project.

In this article, we'll take a look at how to configure logging in Spring Boot. We'll start with a basic example and then move on to more advanced topics.

## Basic Configuration

The simplest way to configure logging in Spring Boot is to add a `logging.level` property to the `application.properties` file. The logging level can be set for specific packages or for specific loggers. For example, the following configuration would set the logging level to `DEBUG` for the `com.example` package:

```
logging.level.com.example=DEBUG
```

If you want to set the logging level for all packages, you can use the `root` logger. For example, the following configuration would set the logging level to `INFO` for all packages:

```
logging.level.root=INFO
```

## Loggers

In addition to setting the logging level, you can also configure the format of the log output. By default, Spring Boot will output the log messages in the `%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n` format.

You can change the format by setting the `logging.pattern.console` property. For example, the following configuration would output the log messages in the `%d [%thread] %-5level %logger{36} - %msg%n` format:

```
logging.pattern.console=%d [%thread] %-5level %logger{36} - %msg%n
```

## Appenders

In addition to the console, Spring Boot can also log to a file. By default, the log messages will be output to a file `spring.log` in the `tmp` directory. You can change the location of the file by setting the `logging.file` property. For example, the following configuration would output the log messages to a file `/var/log/spring.log`:

```
logging.file=/var/log/spring.log
```

## Custom Loggers

If you want to create a custom logger, you can use the `logging.config` property to specify the location of the log4j2.xml file. For example, the following configuration would output the log messages to a file `/var/log/spring.log`:

```
logging.config=log4j2.xml
```

## Advanced Configuration

In addition to the basic configuration, Spring Boot also provides a number of advanced features. For example, you can configure the loggers to output the log messages to multiple files. You can also set the log level for specific classes.

## Logging to Multiple Files

You can configure the loggers to output the log messages to multiple files by setting the `logging.file.name` and `logging.file.max-size` properties. For example, the following configuration would output the log messages to the files `spring.log` and `spring.log.1` in the `tmp` directory:

```
logging.file.name=spring.log
logging.file.max-size=10MB
```

## Logging Level for Classes

You can set the logging level for specific classes by setting the `logging.level.{class}` property. For example, the following configuration would set the logging level to `DEBUG` for the `com.example.MyClass` class:

```
logging.level.com.example.MyClass=DEBUG
```

## Conclusion

In this article, we've taken a look at how to configure logging in Spring Boot. We've seen how to set the logging level and how to change the format of the log output. We've also seen how to output the log messages to multiple files and how to set the logging level for specific classes.