---
title: 067：了解 Spring Boot DevTools 以加快开发速度
description: 
published: true
date: 2023-02-03T18:55:33.069Z
tags: 
editor: markdown
dateCreated: 2023-02-03T18:55:28.084Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [067: Understanding the Spring Boot DevTools for Faster Development***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/067-understanding-the-spring-boot-devtools-for-faster-development)
{.links-list}


# 用于更快开发的 Spring Boot DevTools

## 什么是 Spring Boot DevTools？

Spring Boot DevTools 是一组工具，可帮助开发人员创建生产就绪的 Spring 应用程序。这些工具可以与现有的 IDE 结合使用或从命令行使用。 DevTools 提供快速反馈循环并允许开发人员：

- 文件更改时自动重启应用程序
- 在不重启应用程序的情况下重新加载静态资源
- 无需重新启动应用程序即可实时重新加载 Java 类

## 为什么要使用 Spring Boot DevTools？

使用 Spring Boot DevTools 的主要原因是为了改善开发人员在使用 Spring 应用程序时的体验。 DevTools 通过自动执行常见任务并提供快速反馈循环，可以为开发人员节省大量时间。

## 开始使用 Spring Boot DevTools

### 1. 将 DevTools 依赖项添加到您的项目中

第一步是将 DevTools 依赖项添加到您的项目中。如果您使用的是 Maven，则可以将以下依赖项添加到 pom.xml 文件中：

```xml
<dependencies>
  <dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional>
  </dependency>
</dependencies>
```

如果您使用的是 Gradle，则可以将以下依赖项添加到您的 build.gradle 文件中：

```groovy
dependencies {
  compile("org.springframework.boot:spring-boot-devtools")
}
```

### 2. 在您的 IDE 中启用 DevTools

下一步是在您的 IDE 中启用 DevTools。如果您使用的是 Eclipse，则可以将以下行添加到您的 .project 文件中：

```
<buildCommand>
  <name>org.springframework.boot.devtools.eclipse.launch.devtoolsbuilder</name>
  <arguments>
  </arguments>
</buildCommand>
```

如果您使用的是 IntelliJ IDEA，则可以将以下行添加到您的 .iml 文件中：

```
<component name="DevTools">
  <configuration>
    <restartOnClassChange>true</restartOnClassChange>
  </configuration>
</component>
```

### 3. 从命令行使用 DevTools

如果您使用的是命令行，则可以使用以下命令通过 DevTools 启动您的应用程序：

```
java -jar myapp.jar --spring.devtools.restart.enabled=true
```

## 结论

在本文中，我们了解了如何使用 Spring Boot DevTools 来改善开发人员在使用 Spring 应用程序时的体验。 DevTools 通过自动执行常见任务并提供快速反馈循环，可以为开发人员节省大量时间。