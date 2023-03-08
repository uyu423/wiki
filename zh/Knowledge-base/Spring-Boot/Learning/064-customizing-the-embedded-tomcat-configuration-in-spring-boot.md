---
title: 064: 在 Spring Boot 中自定义嵌入式 Tomcat 配置
description: 
published: true
date: 2023-02-02T16:23:33.376Z
tags: 
editor: markdown
dateCreated: 2023-02-02T16:23:28.844Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [064: Customizing the Embedded Tomcat Configuration in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/064-customizing-the-embedded-tomcat-configuration-in-spring-boot)
{.links-list}


# 在 Spring Boot 中自定义嵌入式 Tomcat 配置

Spring Boot 提供了许多可用于自定义嵌入式 Tomcat 配置的功能。在本文中，我们将了解一些最重要的配置选项。

## 配置 HTTP 端口

您可能想要做的第一件事是更改运行 Tomcat 的 HTTP 端口。默认情况下，Tomcat 将在端口 8080 上运行，但您可以通过在 application.properties 文件中设置 ```server.port``` 属性来更改此设置：

```properties
server.port=8081
```

## 配置 Tomcat 会话超时

另一个常见的自定义是更改会话超时。默认情况下，Tomcat 将使用 30 分钟的会话超时，但您可以通过设置 ```server.session-timeout``` 属性来更改它：

```properties
server.session-timeout=1
```

## 配置 Tomcat 访问日志

Tomcat 还将创建一个访问日志，其中包含有关向服务器发出的所有请求的信息。默认情况下，此日志位于 ```logs``` 目录中，但您可以通过设置 ```server.tomcat.accesslog.directory``` 属性更改位置：

```properties
server.tomcat.accesslog.directory=/var/log/tomcat
```

## 配置 Tomcat URI 编码

默认情况下，Tomcat 将使用 ISO-8859-1 字符集进行 URI 编码。但是，您可以通过设置 ```server.tomcat.uri-encoding``` 属性来更改它：

```properties
server.tomcat.uri-encoding=UTF-8
```

## 配置 Tomcat 连接器

Tomcat 使用连接器来接收请求和发送响应。默认情况下，Tomcat 将使用 AJP 连接器，但您可以通过设置 ```server.tomcat.protocol-header``` 属性来更改它：

```properties
server.tomcat.protocol-header=org.apache.coyote.http11.Http11NioProtocol
```

## 配置 Tomcat 上下文路径

上下文路径是用于访问您的应用程序的路径。默认情况下，这设置为```/```，但您可以通过设置```server.context-path```属性来更改它：

```properties
server.context-path=/myapp
```

## 配置 Tomcat SSL

Tomcat 还支持用于安全通信的 SSL。要配置 SSL，您需要设置 ```server.ssl.key-store```、```server.ssl.key-store-password```、```server.ssl.key-alias ``` 和 ```server.ssl.key-alias-password``` 属性。有关在 Tomcat 中配置 SSL 的更多信息，请参阅 [Tomcat SSL 配置指南](https://tomcat.apache.org/tomcat-8.5-doc/ssl-howto.html)。

## 结论

在本文中，我们了解了在 Spring Boot 中自定义嵌入式 Tomcat 配置的一些最重要的方法。通过更改几个简单的属性，您可以更改 Tomcat 的运行方式以更好地满足您的需要。