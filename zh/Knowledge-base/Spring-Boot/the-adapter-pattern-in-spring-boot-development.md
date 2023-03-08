---
title: Spring Boot开发中的适配器模式
description: 
published: true
date: 2023-02-01T18:18:13.002Z
tags: 
editor: markdown
dateCreated: 2023-02-01T18:18:11.346Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [The Adapter Pattern in Spring Boot Development***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-adapter-pattern-in-spring-boot-development)
{.links-list}



# Spring Boot开发中的适配器模式

在软件开发中，适配器模式是一种软件设计模式，它允许一个软件组件与它通常不能一起工作的其他软件组件一起工作。它通常用于使现有的软件组件与新的软件组件一起工作，或者使新的软件组件与现有的软件组件一起工作。

适配器模式是一种结构模式，是软件开发中最常用的设计模式之一。适配器模式用于解决接口不兼容的问题。

在本文中，我们将了解如何在 Spring Boot 开发中使用适配器模式。我们还将查看一些代码示例来说明如何在实践中使用适配器模式。

## 什么是适配器模式？

正如我们前面提到的，适配器模式是一种软件设计模式，它允许一个软件组件与它通常不能一起工作的其他软件组件一起工作。

适配器模式也称为包装器模式。适配器模式用于解决接口不兼容的问题。

适配器模式是一种结构模式，是软件开发中最常用的设计模式之一。适配器模式用于解决接口不兼容的问题。

适配器模式有两种类型：类适配器模式和对象适配器模式。

## 类适配器模式

类适配器模式是一种适配器模式，它使用继承将一个类适配到另一个类。

在类适配器模式中，适配器类继承自适配器类。适配器类实现目标接口，并将目标接口方法委托给适配器类。

下面是如何在 Java 中使用类适配器模式的示例。

我们有一个名为 Logger 的类，它是一个适配类。 `Logger` 类有一个名为 `log()` 的方法。

```java
public class Logger {
   public void log(String message) {
      // log the message
   }
}
```

我们还有一个名为“ConsoleLogger”的类，它是一个适配器类。 `ConsoleLogger` 类继承自 `Logger` 类。 `ConsoleLogger` 类实现了 `Logger` 接口，并将 `log()` 方法委托给 `Logger` 类。

```java
public class ConsoleLogger extends Logger implements Logger {
   public void log(String message) {
      super.log(message);
   }
}
```

## 对象适配器模式

对象适配器模式是一种适配器模式，它使用组合将一个对象适配到另一个对象。

在对象适配器模式中，适配器类包含适配器类的一个实例。适配器类实现目标接口，并将目标接口方法委托给适配器类。

下面是如何在 Java 中使用对象适配器模式的示例。

我们有一个名为 Logger 的类，它是一个适配类。 `Logger` 类有一个名为 `log()` 的方法。

```java
public class Logger {
   public void log(String message) {
      // log the message
   }
}
```

我们还有一个名为“ConsoleLogger”的类，它是一个适配器类。 `ConsoleLogger` 类包含 `Logger` 类的一个实例。 `ConsoleLogger` 类实现了 `Logger` 接口，并将 `log()` 方法委托给 `Logger` 类。

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

## 如何在 Spring Boot 中使用适配器模式？

在本节中，我们将了解如何在 Spring Boot 开发中使用适配器模式。

我们将在示例中使用类适配器模式。

### 示例 1

在此示例中，我们将使用适配器模式将 `Logger` 类适配为 `ConsoleLogger` 类。

首先，我们需要创建一个 `Logger` 类。

```java
public class Logger {
   public void log(String message) {
      // log the message
   }
}
```

接下来，我们需要创建一个 ConsoleLogger 类。 `ConsoleLogger` 类继承自 `Logger` 类。 `ConsoleLogger` 类实现了 `Logger` 接口，并将 `log()` 方法委托给 `Logger` 类。

```java
public class ConsoleLogger extends Logger implements Logger {
   public void log(String message) {
      super.log(message);
   }
}
```

现在，我们可以在我们的 Spring Boot 应用程序中使用 ConsoleLogger 类。

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

在 logger() 方法中，我们创建了一个 Logger 类型的 bean，即 ConsoleLogger 类。

现在，我们可以将 `Logger` bean 注入我们的应用程序并使用它来记录消息。

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

在 MyComponent 类中，我们将 Logger bean 注入到 logger 字段中。然后我们使用 `logger` 字段来记录消息。

### 示例 2

在此示例中，我们将使用适配器模式将 `RestTemplate` 类适配为 `MyRestTemplate` 类。

首先，我们需要创建一个“RestTemplate”类。

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

接下来，我们需要创建一个 MyRestTemplate 类。 `MyRestTemplate` 类继承自 `RestTemplate` 类。 `MyRestTemplate` 类实现了 `RestTemplate` 接口，并将 `getForObject()` 和 `postForObject()` 方法委托给 `RestTemplate` 类。

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

现在，我们可以在我们的 Spring Boot 应用程序中使用 MyRestTemplate 类。

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

在 `restTemplate()` 方法中，我们正在创建一个 `RestTemplate` 类型的 bean，它是 `MyRestTemplate` 类。

现在，我们可以将 `RestTemplate` bean 注入我们的应用程序并使用它来发出 HTTP 请求。

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

在 MyComponent 类中，我们将 RestTemplate bean 注入到 restTemplate 字段中。然后，我们使用“restTemplate”字段向“http://example.com”URL 发出 GET 请求。

## 结论

在本文中，我们了解了如何在 Spring Boot 开发中使用适配器模式。我们还查看了一些代码示例来说明如何在实践中使用适配器模式。