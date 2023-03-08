---
title: Spring Test: Testing Framework for Spring Boot
description: 
published: true
date: 2023-02-17T18:16:54.261Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:57:36.260Z
---

- [Spring 테스트: Spring Boot용 테스트 프레임워크***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/spring-test-testing-framework-for-spring-boot)
{.links-list}
- [Spring Test: Spring Boot のテスト フレームワーク***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/spring-test-testing-framework-for-spring-boot)
{.links-list}
- [Spring Test：Spring Boot 的测试框架***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/spring-test-testing-framework-for-spring-boot)
{.links-list}


# Spring Test: Testing Framework for Spring Boot

In this article, we will take a look at the Spring Test testing framework for Spring Boot. We will start with a brief overview of the framework, followed by a tutorial on how to use it. After that, we will discuss some of the more advanced features of the framework.

## Overview

Spring Test is a testing framework for Spring Boot. It is designed to help you write tests for your Spring Boot applications. Spring Test provides a convenient way to write tests for your Spring Boot applications. It also provides a number of features that make it easy to write tests for your applications.

## Tutorial

In this tutorial, we will show you how to use Spring Test to write tests for your Spring Boot applications. We will use the example of a simple application that calculates the factorial of a number.

First, we need to add the following dependency to our project:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

Next, we need to write our test case. We will use the @Test annotation to mark our test case.

```java
@Test
public void testFactorial() {
    ...
}
```

In our test case, we need to inject the dependencies that our application needs. We can do this using the @Autowired annotation.

```java
@Autowired
private FactorialService service;
```

Now, we can write our test case. In our test case, we will call the factorial() method of the FactorialService class. We will assert that the result is correct.

```java
@Test
public void testFactorial() {
    int result = service.factorial(5);
    assertThat(result, is(120));
}
```

Now, we can run our test case using the following command:

```
$ mvn test
```

If our test case passes, we will see the following output:

```
Results :

Tests run: 1, Failures: 0, Errors: 0, Skipped: 0

[INFO] 
[INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ spring-boot-test-example ---
[INFO] 
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running com.example.test.ExampleTest
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.002 sec
[INFO] 
[INFO] Results:
[INFO] 
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
[INFO] 
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 2.142 s
[INFO] Finished at: 2015-05-27T16:33:21+0530
[INFO] Final Memory: 10M/155M
[INFO] ------------------------------------------------------------------------
```

## Assertions

Spring Test provides a number of assertion methods that you can use in your test cases. These assertion methods are defined in the org.springframework.test.util.AssertionErrors class.

Here are some of the most commonly used assertion methods:

* assertTrue(condition)
* assertFalse(condition)
* assertEquals(expected, actual)
* assertNotEquals(expected, actual)
* assertNull(object)
* assertNotNull(object)

You can find the complete list of assertion methods in the JavaDoc for the AssertionErrors class.

## Exception Handling

You can use the @Test(expected = Exception.class) annotation to handle expected exceptions in your test cases.

For example, if we expect the factorial() method to throw an IllegalArgumentException when the input is negative, we can write the following test case:

```java
@Test(expected = IllegalArgumentException.class)
public void testFactorialNegative() {
    service.factorial(-1);
}
```

## Java 8 Lambda Support

Spring Test provides support for Java 8 lambda expressions. You can use lambda expressions to write concise and readable test cases.

For example, the following test case checks if the list of numbers is sorted:

```java
@Test
public void testSort() {
    List<Integer> numbers = Arrays.asList(5, 4, 3, 2, 1);
    Collections.sort(numbers);
    assertThat(numbers, is(Arrays.asList(1, 2, 3, 4, 5)));
}
```

## Assumptions

You can use the Assume class to make assumptions about the state of your application. Assumptions are used to skipped tests if the assumption is not met.

For example, the following test case checks if the number is positive. If the number is negative, the test case is skipped.

```java
@Test
public void testPositive() {
    int number = -1;
    Assume.assumeTrue(number > 0);
    assertThat(number, is(greaterThan(0)));
}
```

## Test Context

The TestContext framework provides a number of features that you can use in your test cases. These features include:

* test execution listeners
* testng support
* test event publishing
* test instance post-processing
* dependency injection for test classes

You can use these features to write sophisticated test cases for your applications.

##Conclusion

In this article, we have looked at the Spring Test testing framework for Spring Boot. We have seen how to use the framework to write tests for our applications. We have also seen some of the more advanced features of the framework.