---
title: The Adapter Pattern in Spring Boot Development
description: 
published: true
date: 2023-02-01T18:18:15.383Z
tags: 
editor: markdown
dateCreated: 2023-02-01T18:18:11.339Z
---

- [El patrón de adaptador en el desarrollo de Spring Boot***Spanish** version of this document is available*](/es/Knowledge-base/Spring-Boot/the-adapter-pattern-in-spring-boot-development)
{.links-list}
- [Spring Boot 개발의 어댑터 패턴***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/the-adapter-pattern-in-spring-boot-development)
{.links-list}
- [Spring Boot开发中的适配器模式***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/the-adapter-pattern-in-spring-boot-development)
{.links-list}



# The Adapter Pattern in Spring Boot Development

In software development, the adapter pattern is a software design pattern that allows a software component to work with other software components that it cannot normally work with. It is often used to make existing software components work with new software components, or to make new software components work with existing software components.

The adapter pattern is a type of structural pattern, and is one of the most commonly used design patterns in software development. The adapter pattern is used to solve the problem of incompatible interfaces.

In this article, we will take a look at how to use the adapter pattern in Spring Boot development. We will also look at some code examples to illustrate how the adapter pattern can be used in practice.

## What is the Adapter Pattern?

As we mentioned earlier, the adapter pattern is a software design pattern that allows a software component to work with other software components that it cannot normally work with.

The adapter pattern is also known as the wrapper pattern. The adapter pattern is used to solve the problem of incompatible interfaces.

The adapter pattern is a type of structural pattern, and is one of the most commonly used design patterns in software development. The adapter pattern is used to solve the problem of incompatible interfaces.

There are two types of adapter pattern: class adapter pattern and object adapter pattern.

## Class Adapter Pattern

The class adapter pattern is a type of adapter pattern that uses inheritance to adapt one class to another.

In the class adapter pattern, the adapter class inherits from the adaptee class. The adapter class implements the target interface, and delegates the target interface methods to the adaptee class.

Here is an example of how the class adapter pattern can be used in Java.

We have a class called `Logger`, which is an adaptee class. The `Logger` class has a method called `log()`.

```java
public class Logger {
   public void log(String message) {
      // log the message
   }
}
```

We also have a class called `ConsoleLogger`, which is an adapter class. The `ConsoleLogger` class inherits from the `Logger` class. The `ConsoleLogger` class implements the `Logger` interface, and delegates the `log()` method to the `Logger` class.

```java
public class ConsoleLogger extends Logger implements Logger {
   public void log(String message) {
      super.log(message);
   }
}
```

## Object Adapter Pattern

The object adapter pattern is a type of adapter pattern that uses composition to adapt one object to another.

In the object adapter pattern, the adapter class contains an instance of the adaptee class. The adapter class implements the target interface, and delegates the target interface methods to the adaptee class.

Here is an example of how the object adapter pattern can be used in Java.

We have a class called `Logger`, which is an adaptee class. The `Logger` class has a method called `log()`.

```java
public class Logger {
   public void log(String message) {
      // log the message
   }
}
```

We also have a class called `ConsoleLogger`, which is an adapter class. The `ConsoleLogger` class contains an instance of the `Logger` class. The `ConsoleLogger` class implements the `Logger` interface, and delegates the `log()` method to the `Logger` class.

```java
public class ConsoleLogger {
   private Logger logger;

   public ConsoleLogger(Logger logger) {
      this.logger = logger;
   }

   public void log(String message) {
      logger.log(message);
   }
}
```

## How to Use the Adapter Pattern in Spring Boot?

In this section, we will take a look at how to use the adapter pattern in Spring Boot development.

We will use the class adapter pattern in our examples.

### Example 1

In this example, we will use the adapter pattern to adapt a `Logger` class to the `ConsoleLogger` class.

First, we need to create a `Logger` class.

```java
public class Logger {
   public void log(String message) {
      // log the message
   }
}
```

Next, we need to create a `ConsoleLogger` class. The `ConsoleLogger` class inherits from the `Logger` class. The `ConsoleLogger` class implements the `Logger` interface, and delegates the `log()` method to the `Logger` class.

```java
public class ConsoleLogger extends Logger implements Logger {
   public void log(String message) {
      super.log(message);
   }
}
```

Now, we can use the `ConsoleLogger` class in our Spring Boot application.

```java
@SpringBootApplication
public class Application {

   public static void main(String[] args) {
      SpringApplication.run(Application.class, args);
   }

   @Bean
   public Logger logger() {
      return new ConsoleLogger();
   }
}
```

In the `logger()` method, we are creating a bean of type `Logger`, which is the `ConsoleLogger` class.

Now, we can inject the `Logger` bean into our application and use it to log messages.

```java
@Component
public class MyComponent {

   private Logger logger;

   @Autowired
   public MyComponent(Logger logger) {
      this.logger = logger;
   }

   public void doSomething() {
      logger.log("Doing something");
   }
}
```

In the `MyComponent` class, we are injecting the `Logger` bean into the `logger` field. We are then using the `logger` field to log a message.

### Example 2

In this example, we will use the adapter pattern to adapt a `RestTemplate` class to the `MyRestTemplate` class.

First, we need to create a `RestTemplate` class.

```java
public class RestTemplate {

   public void getForObject(String url, Class responseType) {
      // GET request to the given URL
   }

   public void postForObject(String url, Object request, Class responseType) {
      // POST request to the given URL
   }
}
```

Next, we need to create a `MyRestTemplate` class. The `MyRestTemplate` class inherits from the `RestTemplate` class. The `MyRestTemplate` class implements the `RestTemplate` interface, and delegates the `getForObject()` and `postForObject()` methods to the `RestTemplate` class.

```java
public class MyRestTemplate extends RestTemplate implements RestTemplate {

   public void getForObject(String url, Class responseType) {
      super.getForObject(url, responseType);
   }

   public void postForObject(String url, Object request, Class responseType) {
      super.postForObject(url, request, responseType);
   }
}
```

Now, we can use the `MyRestTemplate` class in our Spring Boot application.

```java
@SpringBootApplication
public class Application {

   public static void main(String[] args) {
      SpringApplication.run(Application.class, args);
   }

   @Bean
   public RestTemplate restTemplate() {
      return new MyRestTemplate();
   }
}
```

In the `restTemplate()` method, we are creating a bean of type `RestTemplate`, which is the `MyRestTemplate` class.

Now, we can inject the `RestTemplate` bean into our application and use it to make HTTP requests.

```java
@Component
public class MyComponent {

   private RestTemplate restTemplate;

   @Autowired
   public MyComponent(RestTemplate restTemplate) {
      this.restTemplate = restTemplate;
   }

   public void doSomething() {
      restTemplate.getForObject("http://example.com", String.class);
   }
}
```

In the `MyComponent` class, we are injecting the `RestTemplate` bean into the `restTemplate` field. We are then using the `restTemplate` field to make a GET request to the `http://example.com` URL.

## Conclusion

In this article, we have taken a look at how to use the adapter pattern in Spring Boot development. We have also looked at some code examples to illustrate how the adapter pattern can be used in practice.