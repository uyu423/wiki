---
title: End-to-end Testing with Spring Boot
description: 
published: true
date: 2023-02-01T17:40:28.362Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:40:23.620Z
---

- [Spring Bootを使用したエンドツーエンドテスト***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/end-to-end-testing-with-spring-boot)
{.links-list}
- [Spring Boot를 사용한 종단 간 테스트***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/end-to-end-testing-with-spring-boot)
{.links-list}
- [使用 Spring Boot 进行端到端测试***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/end-to-end-testing-with-spring-boot)
{.links-list}
- [Pruebas de extremo a extremo con Spring Boot***Spanish** version of this document is available*](/es/Knowledge-base/Spring-Boot/end-to-end-testing-with-spring-boot)
{.links-list}


# End-to-end Testing with Spring Boot

When building web applications, end-to-end (E2E) testing is a key part of the development process. By definition, E2E testing is a type of testing that covers the entire application, from start to finish.

In a traditional web application, the front-end code would make a request to the back-end server, which would then process the request and return a response. With a Spring Boot application, the front-end code still makes a request, but the back-end server is now a Spring Boot application.

E2E testing is important because it allows developers to test the entire application, from the user interface (UI) to the back-end server. It also allows developers to test how the application works when it is deployed to a production environment.

There are many different E2E testing frameworks available, but for this article we will focus on Spring Boot and the E2E testing framework that it provides.

## What is Spring Boot?

Spring Boot is a framework that allows developers to quickly create and deploy Spring-based applications. It provides a number of features that make development and deployment easier, such as:

- Embedded Tomcat server
- Automatic configuration
- Starter templates

Spring Boot is a great choice for developing E2E tests because it makes it easy to create and deploy a Spring-based application.

## What is the E2E Testing Framework?

The E2E Testing Framework is a set of tools that allow developers to quickly create and run E2E tests. It is based on the JUnit testing framework and provides a number of features that make E2E testing easier, such as:

- A @SpringBootTest annotation that can be used to configure the Spring Boot application for testing
- A @WebIntegrationTest annotation that can be used to configure the web server for testing
- A @MockBean annotation that can be used to mock beans in the Spring application context

The E2E Testing Framework is a great choice for developing E2E tests because it makes it easy to create and run E2E tests.

## Creating an E2E test

Let's now look at how to create an E2E test using the E2E Testing Framework. We will be testing a simple Spring Boot application that has a single endpoint that returns a list of users.

The first thing we need to do is create a new JUnit test class and annotate it with @SpringBootTest:

```java
@SpringBootTest
public class UserControllerTest {

}
```

The @SpringBootTest annotation is used to configure the Spring Boot application for testing.

Next, we need to create a test method and annotate it with @Test:

```java
@Test
public void testGetUsers() {

}
```

The @Test annotation is used to mark a method as a test method.

In the test method, we need to create an instance of the UserController and invoke the getUsers() method:

```java
@Test
public void testGetUsers() {
    UserController userController = new UserController();
    List<User> users = userController.getUsers();
}
```

The getUsers() method returns a list of users, so we can assert that the list is not empty:

```java
@Test
public void testGetUsers() {
    UserController userController = new UserController();
    List<User> users = userController.getUsers();
    assertThat(users).isNotEmpty();
}
```

We can also assert that the list contains the expected number of users:

```java
@Test
public void testGetUsers() {
    UserController userController = new UserController();
    List<User> users = userController.getUsers();
    assertThat(users).hasSize(2);
}
```

Finally, we can assert that the list contains the expected users:

```java
@Test
public void testGetUsers() {
    UserController userController = new UserController();
    List<User> users = userController.getUsers();
    assertThat(users)
        .contains(new User("user1@example.com", "User 1"),
                  new User("user2@example.com", "User 2"));
}
```

The complete E2E test is shown below:

```java
@SpringBootTest
public class UserControllerTest {

    @Test
    public void testGetUsers() {
        UserController userController = new UserController();
        List<User> users = userController.getUsers();
        assertThat(users)
            .contains(new User("user1@example.com", "User 1"),
                      new User("user2@example.com", "User 2"));
    }
}
```

## Running the E2E test

To run the E2E test, we simply need to run the test class as a JUnit test:

```java
@SpringBootTest
public class UserControllerTest {

    @Test
    public void testGetUsers() {
        UserController userController = new UserController();
        List<User> users = userController.getUsers();
        assertThat(users)
            .contains(new User("user1@example.com", "User 1"),
                      new User("user2@example.com", "User 2"));
    }
}
```

## Conclusion

In this article, we have seen how to create and run an E2E test using the E2E Testing Framework. We have also seen how to use the @SpringBootTest and @Test annotations to configure the Spring Boot application and mark a method as a test method.