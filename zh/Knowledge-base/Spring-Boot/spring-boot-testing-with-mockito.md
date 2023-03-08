---
title: 使用 Mockito 进行 Spring Boot 测试
description: 
published: true
date: 2023-02-02T00:23:22.466Z
tags: 
editor: markdown
dateCreated: 2023-02-02T00:23:20.928Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot Testing with Mockito***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-testing-with-mockito)
{.links-list}


# 使用 Mockito 进行 Spring Boot 测试

Spring Boot 提供了一种为应用程序编写测试的好方法。在本文中，我们将了解如何使用 Mockito 测试您的 Spring Boot 应用程序。

Mockito 是一个强大的 Java 模拟框架。它在 Spring 社区中非常受欢迎。 Mockito 允许我们编写与外部世界隔离的测试。当我们想在不依赖外部服务的情况下测试我们的业务逻辑时，这一点非常重要。

## 设置 Mockito

首先，我们需要将 Mockito 依赖项添加到我们的 pom.xml 中：

```xml
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-core</artifactId>
    <version>2.0.0-beta.19</version>
    <scope>test</scope>
</dependency>
```

我们现在可以创建一个“MockitoJUnitRunner”来运行我们的测试：

```java
import org.junit.runner.RunWith;
import org.mockito.runners.MockitoJUnitRunner;

@RunWith(MockitoJUnitRunner.class)
public class MyTest {
}
```

## 在 Spring Boot 中使用 Mockito

Mockito 非常容易与 Spring Boot 一起使用。我们可以简单地用 @MockBean 注释我们的测试类来创建一个 Spring Bean 的模拟：

```java
@RunWith(MockitoJUnitRunner.class)
public class MyTest {

    @MockBean
    private MyService myService;
}
```

然后我们可以使用 Mockito 来存根 `MyService` 的方法：

```java
@RunWith(MockitoJUnitRunner.class)
public class MyTest {

    @MockBean
    private MyService myService;

    @Test
    public void testMyService() {
        // given
        given(myService.doSomething()).willReturn("Hello world!");

        // when
        String result = myService.doSomething();

        // then
        assertThat(result).isEqualTo("Hello world!");
    }
}
```

## 结论

在本文中，我们了解了如何使用 Mockito 测试 Spring Boot 应用程序。 Mockito 是一个非常强大的工具，可以帮助我们编写更好的测试。