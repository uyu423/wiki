---
title: Unit Testing in Spring Boot with JUnit
description: 
published: true
date: 2023-02-01T17:27:45.940Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:27:41.271Z
---

- [JUnit を使用した Spring Boot での単体テスト***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/unit-testing-in-spring-boot-with-junit)
{.links-list}
- [JUnit을 사용하여 Spring Boot에서 단위 테스트***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/unit-testing-in-spring-boot-with-junit)
{.links-list}
- [使用 JUnit 在 Spring Boot 中进行单元测试***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/unit-testing-in-spring-boot-with-junit)
{.links-list}
- [Pruebas unitarias en Spring Boot con JUnit***Spanish** version of this document is available*](/es/Knowledge-base/Spring-Boot/unit-testing-in-spring-boot-with-junit)
{.links-list}


# Unit Testing in Spring Boot with JUnit

Unit testing is a software testing method where the individual units/components of a software are tested to verify that each unit works as expected. A unit is the smallest testable part of an application. In Spring Boot, unit tests are usually written using JUnit.

JUnit is a popular testing framework for Java. It is an open source project hosted on Github. JUnit has been important in the development of test-driven development, and is one of a family of unit testing frameworks which is collectively known as xUnit that originated with SUnit.

In this article, we will take a look at how to unit test a Spring Boot application using JUnit. We will write a simple test to test a RestController endpoint. The example code for this article can be found on Github.

## Setting up the Project

We will start by setting up a simple Spring Boot project. We will use the Spring Initializr to generate our project. We will select the following dependencies:

- Web
- JPA
- H2 Database
- Lombok

Lombok is a library which can be used to reduce boilerplate code in Java applications. We will use it to reduce the amount of code we need to write for our tests.

Once the project is generated, we can import it into our IDE of choice. I will be using IntelliJ IDEA.

## Writing the Unit Test

Now that we have our project set up, we can write our unit test. We will start by creating a new package for our tests, `com.example.demo.controller`. In this package, we will create a new class, `DemoControllerTest`.

This class will be annotated with `@RunWith(SpringRunner.class)` and `@WebMvcTest(DemoController.class)`. The `@RunWith` annotation tells JUnit to use the `SpringRunner` class to run our tests. The `@WebMvcTest` annotation is used to test Spring MVC controllers. It will auto-configure Spring MVC, and will disable full auto-configuration.

In our `DemoControllerTest` class, we will create a `@Autowired` field for our `MockMvc` object. `MockMvc` is used to perform HTTP requests to our controller and assert the response. We will also create a `@Before` method annotated with `@BeforeEach`. This method will be used to initialize our `MockMvc` object.

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

In our `setup` method, we use the `MockMvcBuilders` static factory methods to create a `MockMvc` instance. We use the `webAppContextSetup` method and pass in our `WebApplicationContext`. This will create a `MockMvc` instance that is backed by a `WebApplicationContext`.

Now that we have our `MockMvc` object set up, we can write our test method. We will annotate our method with `@Test`. In our test method, we will use the `MockMvc` object to perform an HTTP `GET` request to our `/demo` endpoint. We will then assert that the response status is `200 OK` and that the response content contains the string `Hello, world!`.

```java
@Test
public void testDemoEndpoint() throws Exception {
    mockMvc.perform(get("/demo"))
            .andExpect(status().isOk())
            .andExpect(content().string(containsString("Hello, world!")));
}
```

We use the `perform` method on our `MockMvc` object to perform an HTTP request. We use the `get` method to create a `GET` request. We then use the `andExpect` methods to assert the response status and content.

## Running the Test

We can now run our test. We can run our test from the command line using the `./mvnw test` command. We can also run our test from within our IDE.

## Conclusion

In this article, we have looked at how to unit test a Spring Boot application using JUnit. We have written a simple test to test a RestController endpoint.