---
title: 使用 JUnit 进行 Spring Boot 测试
description: 
published: true
date: 2023-02-07T19:32:31.718Z
tags: 
editor: markdown
dateCreated: 2023-02-07T19:32:25.884Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot Testing with JUnit***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-testing-with-junit)
{.links-list}


# 使用 JUnit 进行 Spring Boot 测试

测试是任何软件开发过程的关键部分。它有助于确保您的代码按预期工作，并有助于尽早发现错误。

JUnit 是一种流行的 Java 单元测试框架。 Spring Boot 为 JUnit 测试提供一流的支持。在本文中，我们将了解如何使用 JUnit 设置和编写 Spring Boot 测试。

## 配置

首先，您需要将以下依赖项添加到您的 `pom.xml`：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

`spring-boot-starter-test` 依赖项包括许多用于编写测试的有用库，包括 JUnit、Hamcrest 和 Mockito。

## 编写测试

Spring Boot 测试可以用 JUnit 4 或 JUnit 5 编写。在本节中，我们将分别查看一个示例。

### 联合 4

下面是一个 JUnit 4 测试的简单示例：

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class MyTest {

    @Test
    public void test() {
        // test code goes here
    }

}
```

@RunWith 注释用于指定要使用的测试框架。 @SpringBootTest 注释告诉 Spring Boot 加载测试的应用程序上下文。

@Test 注释用于将方法标记为测试方法。

### 联合 5

JUnit 5 测试看起来与 JUnit 4 测试相似，但有一些关键差异：

```java
@SpringBootTest
public class MyTest {

    @Test
    public void test() {
        // test code goes here
    }

}
```

首先，不再需要“@RunWith”注解。其次，@Test 注解现在属于 org.junit.jupiter.api 包。

JUnit 5 还引入了一组新的断言，可以在 org.junit.jupiter.api.Assertions 类中找到。例如，可以像这样使用 `assertEquals` 断言：

```java
assertEquals(expected, actual);
```

## 测试 SpringBootApplicationTests

Spring Boot 为编写测试提供了许多有用的注解。在本节中，我们将了解一些最常用的注释。

### @WebMvcTest

@WebMvcTest 注释用于测试 Spring MVC 控制器。它可以这样使用：

```java
@WebMvcTest(MyController.class)
public class MyControllerTest {

    @Autowired
    private MockMvc mvc;

    @Test
    public void test() {
        // test code goes here
    }

}
```

@WebMvcTest 注解只会加载测试 Spring MVC 所需的组件。这对于减少加载应用程序上下文以进行测试所需的时间很有用。

`@Autowired` 注释用于注入 `MockMvc` bean。 `MockMvc` bean 可用于向控制器发送 HTTP 请求并验证响应。

### @DataJpaTest

@DataJpaTest 注释用于测试 Spring Data JPA 存储库。它可以这样使用：

```java
@DataJpaTest
public class MyRepositoryTest {

    @Autowired
    private MyRepository repository;

    @Test
    public void test() {
        // test code goes here
    }

}
```

@DataJpaTest 注释将只加载测试 Spring Data JPA 所需的组件。这对于减少加载应用程序上下文以进行测试所需的时间很有用。

`@Autowired` 注解用于注入 `MyRepository` bean。该 bean 可用于访问数据库中的数据。

### @RestClientTest

@RestClientTest 注释用于测试 Spring RestTemplate 客户端。它可以这样使用：

```java
@RestClientTest(MyClient.class)
public class MyClientTest {

    @Autowired
    private MockRestTemplate template;

    @Test
    public void test() {
        // test code goes here
    }

}
```

@RestClientTest 注解只会加载测试 Spring RestTemplate 所需的组件。这对于减少加载应用程序上下文以进行测试所需的时间很有用。

`@Autowired` 注释用于注入 `MockRestTemplate` bean。 `MockRestTemplate` bean 可用于向客户端发送 HTTP 请求并验证响应。

## 结论

在本文中，我们了解了如何使用 Spring Boot 和 JUnit 设置和编写测试。我们还看到了一些最常用的用于编写测试的注释。