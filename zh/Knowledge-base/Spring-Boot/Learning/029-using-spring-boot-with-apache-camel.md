---
title: 029：将 Spring Boot 与 Apache Camel 结合使用
description: 
published: true
date: 2023-02-03T21:32:17.247Z
tags: 
editor: markdown
dateCreated: 2023-02-03T21:32:15.346Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [029: Using Spring Boot with Apache Camel***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/029-using-spring-boot-with-apache-camel)
{.links-list}


# 将 Spring Boot 与 Apache Camel 结合使用

随着 Camel 2.0 的发布，引入了一组新的注释，使 Camel 更易于与 Spring Framework 一起使用。在这篇文章中，我们将看看如何将 Spring Boot 与 Camel 结合使用。

我们将从一个将 HTTP 请求路由到日志的简单示例开始。首先，我们需要将以下依赖项添加到我们的 pom.xml 中：

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-spring-boot-starter</artifactId>
    <version>2.22.0</version>
</dependency>
```

现在我们可以创建一个 `@Configuration` 类来设置 Camel：

```java
@Configuration
public class MyRouteBuilder extends RouteBuilder {

    @Override
    public void configure() {
        from("jetty:http://0.0.0.0:8080/myapp")
            .to("log:requests");
    }
}
```

最后，我们需要一个 `application.properties` 文件来配置 Jetty 服务器：

```properties
server.port=8080
```

就是这样！我们现在可以运行我们的应用程序并使用浏览器或 `curl` 访问 `http://localhost:8080/myapp`。我们应该在控制台中看到记录的请求。

当然，这个例子很简单。 Camel 提供了大量的组件，可用于构建更复杂的应用程序。有关将 Camel 与 Spring Boot 结合使用的更多信息，请查看 [文档](http://camel.apache.org/spring-boot.html)。