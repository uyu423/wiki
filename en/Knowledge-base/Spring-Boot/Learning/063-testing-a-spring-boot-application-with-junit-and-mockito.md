---
title: 063: Testing a Spring Boot Application with JUnit and Mockito
description: 
published: true
date: 2023-02-05T01:32:31.696Z
tags: 
editor: markdown
dateCreated: 2023-02-05T01:32:25.528Z
---

- [063: Prueba de una aplicación Spring Boot con JUnit y Mockito***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/063-testing-a-spring-boot-application-with-junit-and-mockito)
{.links-list}
- [063：使用 JUnit 和 Mockito 测试 Spring Boot 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/063-testing-a-spring-boot-application-with-junit-and-mockito)
{.links-list}
- [063: JUnit과 Mockito로 Spring Boot 애플리케이션 테스트하기***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/063-testing-a-spring-boot-application-with-junit-and-mockito)
{.links-list}


# 063: Testing a Spring Boot Application with JUnit and Mockito

In this post, we'll learn how to test a Spring Boot application with JUnit and Mockito.

Spring Boot makes it easy to create stand-alone, production-grade Spring-based Applications that you can "just run". We'll use Spring Boot in this example to make things even easier.

JUnit is a popular testing framework for Java. Mockito is a mocking framework for Java that allows you to create mock objects and stub methods.

## Setting up the Project

First, we'll create a new Spring Boot project using the [Spring Initializr](https://start.spring.io/). We'll name our project `spring-boot-junit-mockito-example`.

![Spring Initializr](https://i.imgur.com/HgflTDz.png)

Next, we'll select the `Web` and `Actuator` dependencies. The `Web` dependency will add support for web applications and the `Actuator` dependency will add support for monitoring and managing our application.

![Spring Initializr Dependencies](https://i.imgur.com/sA6qEjK.png)

Once the project has been generated, we can import it into our favorite IDE. I'm using [IntelliJ IDEA](https://www.jetbrains.com/idea/).

## Writing the Tests

Now that our project is set up, we can start writing our tests. We'll create a new `src/test/java` directory and add a new `SpringBootJunitMockitoExampleApplicationTests.java` file.

In this file, we'll add a simple test that verifies that our Spring Boot application can be started.

    @RunWith(SpringRunner.class)
    @SpringBootTest
    public class SpringBootJunitMockitoExampleApplicationTests {
    
        @Test
        public void contextLoads() {
        }
    
    }

We annotate our test class with `@RunWith(SpringRunner.class)` and `@SpringBootTest`. The `@RunWith` annotation tells JUnit to use the `SpringRunner` class to run our tests. The `@SpringBootTest` annotation tells Spring Boot to load our application context.

The `contextLoads()` test method verifies that the context can be loaded.

We can run our tests using the `mvn test` command.

![Running the Tests](https://i.imgur.com/VkzcTGi.png)

## Writing a Unit Test

Now that we've verified that our application can be started, we can write a unit test. A unit test is a test that verifies the behavior of a single unit of code, such as a method.

We'll create a new `src/test/java` directory and add a new `CalculatorTest.java` file. In this file, we'll add a test for the `add()` method of our `Calculator` class.

    @RunWith(MockitoJUnitRunner.class)
    public class CalculatorTest {
    
        @InjectMocks
        private Calculator calculator;
    
        @Test
        public void testAdd() {
            assertEquals(5, calculator.add(2, 3));
        }
    
    }

We annotate our test class with `@RunWith(MockitoJUnitRunner.class)`. This tells Mockito to use the `MockitoJUnitRunner` class to run our tests.

The `@InjectMocks` annotation injects mock objects into our `Calculator` class. The `@Test` annotation tells JUnit that the `testAdd()` method is a test.

In the `testAdd()` method, we use the `assertEquals()` method to verify that the `add()` method returns the expected value.

We can run our tests using the `mvn test` command.

![Running the Tests](https://i.imgur.com/5BQ7UgI.png)

## Writing a Integration Test

Now that we've verified that our `Calculator` class works as expected, we can write an integration test. An integration test is a test that verifies the behavior of two or more units of code.

We'll create a new `src/test/java` directory and add a new `CalculatorIntegrationTest.java` file. In this file, we'll add a test for the `add()` method of our `Calculator` class.

    @RunWith(SpringRunner.class)
    @SpringBootTest
    public class CalculatorIntegrationTest {
    
        @Autowired
        private Calculator calculator;
    
        @Test
        public void testAdd() {
            assertEquals(5, calculator.add(2, 3));
        }
    
    }

We annotate our test class with `@RunWith(SpringRunner.class)` and `@SpringBootTest`. The `@RunWith` annotation tells JUnit to use the `SpringRunner` class to run our tests. The `@SpringBootTest` annotation tells Spring Boot to load our application context.

The `@Autowired` annotation injects the `Calculator` bean into our test class. The `@Test` annotation tells JUnit that the `testAdd()` method is a test.

In the `testAdd()` method, we use the `assertEquals()` method to verify that the `add()` method returns the expected value.

We can run our tests using the `mvn test` command.

![Running the Tests](https://i.imgur.com/p7Aj0bU.png)

## Conclusion

In this post, we've learned how to test a Spring Boot application with JUnit and Mockito. We've also seen how to write unit tests and integration tests.