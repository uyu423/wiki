---
title: Mockito：在 Spring Boot 中模拟单元测试
description: 
published: true
date: 2023-02-01T17:48:04.870Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:48:00.841Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Mockito: Mocking for Unit Testing in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/mockito-mocking-for-unit-testing-in-spring-boot)
{.links-list}


# Mockito：在 Spring Boot 中模拟单元测试

模拟是单元测试中的一个关键概念，它允许开发人员专注于测试特定代码单元的功能，而不是其依赖性。在 Spring Boot 应用程序的上下文中，Mockito 可用于模拟 bean 和服务以测试特定组件的功能，而无需启动整个 Spring 上下文。

在本文中，我们将了解如何使用 Mockito 在 Spring Boot 应用程序中模拟 bean 和服务。我们还将了解如何配置 Mockito 以自动启动 Spring 上下文。

## 什么是 Mockito？

Mockito 是一个流行的 Java 模拟测试框架。 Mockito 允许开发人员创建和配置要在单元测试中使用的模拟对象。 Mockito 可用于模拟接口、类，甚至最终类和方法。

## 在 Spring Boot 中模拟 Bean 和服务

使用 Mockito 可以轻松地在 Spring Boot 中模拟 bean 和服务。在下面的示例中，我们将模拟一个名为 myBean 的 bean：

```java
@MockBean
MyBean myBean;

@Test
public void testMyBean() {
    // configure mock object
    when(myBean.getName()).thenReturn("Mockito");
    
    // invoke method on mock object
    String name = myBean.getName();
    
    // verify results
    assertThat(name).isEqualTo("Mockito");
}
```

在上面的示例中，我们使用 @MockBean 注释创建了 MyBean 类的模拟对象。然后我们使用 `when` 和 `thenReturn` 方法来配置模拟对象。最后，我们在模拟对象上调用 getName 方法并断言返回值符合预期。

## 在 Spring Boot 中配置 Mockito

可以使用“mockito-core”和“mockito-spring”依赖项在 Spring Boot 中配置 Mockito。在 `pom.xml` 文件中，添加以下依赖项：

```xml
<dependencies>
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-core</artifactId>
        <version>2.13.0</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.mockito</groupId>
        <artifactId>mockito-spring</artifactId>
        <version>1.9.5</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

`mockito-core` 依赖包含 Mockito 库，而 `mockito-spring` 依赖包含 Mockito 和 Spring 之间的集成。

＃＃ 结论

在本文中，我们了解了如何使用 Mockito 在 Spring Boot 应用程序中模拟 bean 和服务。我们还了解了如何配置 Mockito 以自动启动 Spring 上下文。