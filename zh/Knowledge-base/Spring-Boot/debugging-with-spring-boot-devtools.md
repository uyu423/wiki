---
title: 使用 Spring Boot DevTools 进行调试
description: 
published: true
date: 2023-02-07T02:32:31.471Z
tags: 
editor: markdown
dateCreated: 2023-02-07T02:32:29.838Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Debugging with Spring Boot DevTools***English** document is available*](/en/Knowledge-base/Spring-Boot/debugging-with-spring-boot-devtools)
{.links-list}


# 使用 Spring Boot DevTools 进行调试

Spring Boot 带有许多强大的功能，可以帮助开发人员开发他们的应用程序。 DevTools 是这些功能之一。它可以帮助调试、重新加载等。

## 什么是开发者工具？

DevTools 是一组可以帮助开发的工具。它可以做一些事情，比如在不重启服务器的情况下重新加载你的应用程序，并在文件更改时自动重启服务器。它还可以帮助调试，允许您在 IDE 中调试应用程序。

## 设置开发者工具

要使用 DevTools，您需要将其添加到您的项目中。您可以通过将其添加到您的依赖项来执行此操作。例如，在 Maven 中，您可以将它添加到您的 `pom.xml` 中：

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
    </dependency>
</dependencies>
```

或者，如果您使用的是 Gradle，您可以将其添加到您的 `build.gradle` 中：

```groovy
dependencies {
    compile 'org.springframework.boot:spring-boot-devtools'
}
```

## 使用开发者工具

在项目中配置 DevTools 后，就可以开始使用它了。

### 重新加载你的应用程序

DevTools 最有用的功能之一是能够在不重新启动服务器的情况下重新加载应用程序。为此，您只需在 IDE 中按“Ctrl+F9”（或在 macOS 上按“Cmd+F9”）即可。这将触发您的应用程序的完全重启。

如果您只想重新启动服务器，您可以按 `Ctrl+Shift+F9`（或 macOS 上的 `Cmd+Shift+F9`）。这只会重新启动服务器，而不是应用程序。

### 调试你的应用程序

DevTools 的另一个有用功能是能够在 IDE 中调试应用程序。为此，您需要以调试模式启动您的应用程序。您可以通过将 `--debug` 标志传递给 `spring-boot` CLI 来做到这一点：

```
$ spring-boot --debug
```

或者，您可以在 `application.properties` 中设置 `spring.boot.debug` 属性：

```properties
spring.boot.debug=true
```

一旦您的应用程序以调试模式运行，您就可以将调试器附加到它。例如，在 IntelliJ IDEA 中，您可以通过转到“运行 > 将调试器附加到本地进程”来执行此操作。

## 结论

DevTools 是一个很棒的工具，可以帮助开发。它可以做一些事情，比如在不重启服务器的情况下重新加载你的应用程序，并在文件更改时自动重启服务器。它还可以帮助调试，允许您在 IDE 中调试应用程序。