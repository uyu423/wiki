---
title: 063：使用 JUnit 和 Mockito 测试 Spring Boot 应用程序
description: 
published: true
date: 2023-02-05T01:32:27.948Z
tags: 
editor: markdown
dateCreated: 2023-02-05T01:32:25.523Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [063: Testing a Spring Boot Application with JUnit and Mockito***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/063-testing-a-spring-boot-application-with-junit-and-mockito)
{.links-list}


# 063：使用 JUnit 和 Mockito 测试 Spring Boot 应用程序

在本文中，我们将学习如何使用 JUnit 和 Mockito 测试 Spring Boot 应用程序。

Spring Boot 可以轻松创建独立的、生产级的基于 Spring 的应用程序，您可以“直接运行”。我们将在此示例中使用 Spring Boot 来简化操作。

JUnit 是一种流行的 Java 测试框架。 Mockito 是 Java 的模拟框架，允许您创建模拟对象和存根方法。

## 设置项目

首先，我们将使用 [Spring Initializr](https://start.spring.io/) 创建一个新的 Spring Boot 项目。我们将我们的项目命名为“spring-boot-junit-mockito-example”。

![Spring Initializr](https://i.imgur.com/HgflTDz.png)

接下来，我们将选择“Web”和“Actuator”依赖项。 `Web` 依赖项将添加对 Web 应用程序的支持，而 `Actuator` 依赖项将添加对监视和管理我们的应用程序的支持。

![Spring Initializr 依赖项](https://i.imgur.com/sA6qEjK.png)

生成项目后，我们可以将其导入到我们最喜欢的 IDE 中。我正在使用 [IntelliJ IDEA](https://www.jetbrains.com/idea/)。

## 编写测试

现在我们的项目已经建立，我们可以开始编写测试了。我们将创建一个新的 `src/test/java` 目录并添加一个新的 `SpringBootJunitMockitoExampleApplicationTests.java` 文件。

在这个文件中，我们将添加一个简单的测试来验证我们的 Spring Boot 应用程序是否可以启动。

    @RunWith(SpringRunner.class)
    @SpringBootTest
    公共类 SpringBootJunitMockitoExampleApplicationTests {
    
        @测试
        public void contextLoads() {
        }
    
    }

我们用 @RunWith(SpringRunner.class) 和 @SpringBootTest 注释我们的测试类。 `@RunWith` 注释告诉 JUnit 使用 `SpringRunner` 类来运行我们的测试。 @SpringBootTest 注释告诉 Spring Boot 加载我们的应用程序上下文。

`contextLoads()` 测试方法验证上下文是否可以加载。

我们可以使用 `mvn test` 命令运行我们的测试。

![运行测试](https://i.imgur.com/VkzcTGi.png)

## 编写单元测试

现在我们已经验证了我们的应用程序可以启动，我们可以编写单元测试了。单元测试是验证单个代码单元（例如方法）的行为的测试。

我们将创建一个新的 `src/test/java` 目录并添加一个新的 `CalculatorTest.java` 文件。在这个文件中，我们将为我们的 Calculator 类的 add() 方法添加一个测试。

    @RunWith(MockitoJUnitRunner.class)
    公共类 CalculatorTest {
    
        @InjectMocks
        私人计算器计算器；
    
        @测试
        公共无效测试添加（）{
            assertEquals(5, calculator.add(2, 3));
        }
    
    }

我们用 @RunWith(MockitoJUnitRunner.class) 注释我们的测试类。这告诉 Mockito 使用 MockitoJUnitRunner 类来运行我们的测试。

@InjectMocks 注释将模拟对象注入我们的 Calculator 类。 `@Test` 注解告诉 JUnit `testAdd()` 方法是一个测试。

在 testAdd() 方法中，我们使用 assertEquals() 方法来验证 add() 方法是否返回预期值。

我们可以使用 `mvn test` 命令运行我们的测试。

![运行测试](https://i.imgur.com/5BQ7UgI.png)

## 编写集成测试

现在我们已经验证了我们的 Calculator 类按预期工作，我们可以编写集成测试。集成测试是验证两个或多个代码单元的行为的测试。

我们将创建一个新的 `src/test/java` 目录并添加一个新的 `CalculatorIntegrationTest.java` 文件。在这个文件中，我们将为我们的 Calculator 类的 add() 方法添加一个测试。

    @RunWith(SpringRunner.class)
    @SpringBootTest
    公共类 CalculatorIntegrationTest {
    
        @Autowired
        私人计算器计算器；
    
        @测试
        公共无效测试添加（）{
            assertEquals(5, calculator.add(2, 3));
        }
    
    }

我们用 @RunWith(SpringRunner.class) 和 @SpringBootTest 注释我们的测试类。 `@RunWith` 注释告诉 JUnit 使用 `SpringRunner` 类来运行我们的测试。 @SpringBootTest 注释告诉 Spring Boot 加载我们的应用程序上下文。

`@Autowired` 注释将 `Calculator` bean 注入到我们的测试类中。 `@Test` 注解告诉 JUnit `testAdd()` 方法是一个测试。

在 testAdd() 方法中，我们使用 assertEquals() 方法来验证 add() 方法是否返回预期值。

我们可以使用 `mvn test` 命令运行我们的测试。

![运行测试](https://i.imgur.com/p7Aj0bU.png)

## 结论

在本文中，我们学习了如何使用 JUnit 和 Mockito 测试 Spring Boot 应用程序。我们还了解了如何编写单元测试和集成测试。