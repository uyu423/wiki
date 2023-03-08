---
title: 使用 JUnit 在 Spring Boot 中进行单元测试
description: 
published: true
date: 2023-02-01T17:27:43.340Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:27:41.255Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Unit Testing in Spring Boot with JUnit***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/unit-testing-in-spring-boot-with-junit)
{.links-list}


# 在 Spring Boot 中使用 JUnit 进行单元测试

单元测试是一种软件测试方法，其中测试软件的各个单元/组件以验证每个单元是否按预期工作。单元是应用程序中最小的可测试部分。在 Spring Boot 中，单元测试通常使用 JUnit 编写。

JUnit 是一种流行的 Java 测试框架。它是一个托管在 Github 上的开源项目。 JUnit 在测试驱动开发的发展中一直很重要，并且是单元测试框架家族之一，统称为 xUnit，起源于 SUnit。

在本文中，我们将了解如何使用 JUnit 对 Spring Boot 应用程序进行单元测试。我们将编写一个简单的测试来测试 RestController 端点。本文的示例代码可以在 Github 上找到。

## 设置项目

我们将从设置一个简单的 Spring Boot 项目开始。我们将使用 Spring Initializr 来生成我们的项目。我们将选择以下依赖项：

- 网络
- JPA
- H2数据库
- 龙目岛

Lombok 是一个库，可用于减少 Java 应用程序中的样板代码。我们将使用它来减少我们需要为测试编写的代码量。

生成项目后，我们可以将其导入到我们选择的 IDE 中。我将使用 IntelliJ IDEA。

## 编写单元测试

现在我们已经设置了项目，我们可以编写单元测试了。我们将从为我们的测试创建一个新包开始，`com.example.demo.controller`。在这个包中，我们将创建一个新类“DemoControllerTest”。

此类将使用“@RunWith(SpringRunner.class)”和“@WebMvcTest(DemoController.class)”进行注释。 `@RunWith` 注释告诉 JUnit 使用 `SpringRunner` 类来运行我们的测试。 @WebMvcTest 注释用于测试 Spring MVC 控制器。它将自动配置 Spring MVC，并将禁用完全自动配置。

在我们的 DemoControllerTest 类中，我们将为我们的 MockMvc 对象创建一个 @Autowired 字段。 `MockMvc` 用于向我们的控制器执行 HTTP 请求并断言响应。我们还将创建一个用“@BeforeEach”注释的“@Before”方法。此方法将用于初始化我们的“MockMvc”对象。

```java
@RunWith(SpringRunner.class)
@WebMvcTest(DemoController.class)
public class DemoControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @BeforeEach
    public void setup() {
        mockMvc = MockMvcBuilders.webAppContextSetup(webApplicationContext)
                .build();
    }
}
```

在我们的 setup 方法中，我们使用 MockMvcBuilders 静态工厂方法来创建 MockMvc 实例。我们使用 `webAppContextSetup` 方法并传入我们的 `WebApplicationContext`。这将创建一个由 `WebApplicationContext` 支持的 `MockMvc` 实例。

现在我们已经设置了 `MockMvc` 对象，我们可以编写测试方法了。我们将使用“@Test”注释我们的方法。在我们的测试方法中，我们将使用 MockMvc 对象对我们的 /demo 端点执行 HTTP GET 请求。然后我们将断言响应状态为“200 OK”并且响应内容包含字符串“Hello, world!”。

```java
@Test
public void testDemoEndpoint() throws Exception {
    mockMvc.perform(get("/demo"))
            .andExpect(status().isOk())
            .andExpect(content().string(containsString("Hello, world!")));
}
```

我们在 `MockMvc` 对象上使用 `perform` 方法来执行 HTTP 请求。我们使用 `get` 方法创建一个 `GET` 请求。然后我们使用 `andExpect` 方法断言响应状态和内容。

## 运行测试

我们现在可以运行我们的测试。我们可以使用 ./mvnw test 命令从命令行运行我们的测试。我们还可以从我们的 IDE 中运行我们的测试。

## 结论

在本文中，我们了解了如何使用 JUnit 对 Spring Boot 应用程序进行单元测试。我们编写了一个简单的测试来测试 RestController 端点。