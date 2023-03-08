---
title: Spring Boot 개발의 어댑터 패턴
description: 
published: true
date: 2023-02-01T18:18:12.993Z
tags: 
editor: markdown
dateCreated: 2023-02-01T18:18:11.344Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [The Adapter Pattern in Spring Boot Development***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-adapter-pattern-in-spring-boot-development)
{.links-list}



# Spring Boot 개발의 어댑터 패턴

소프트웨어 개발에서 어댑터 패턴은 소프트웨어 구성 요소가 일반적으로 작동할 수 없는 다른 소프트웨어 구성 요소와 작동할 수 있도록 하는 소프트웨어 디자인 패턴입니다. 기존 소프트웨어 구성 요소가 새 소프트웨어 구성 요소와 함께 작동하도록 하거나 새 소프트웨어 구성 요소가 기존 소프트웨어 구성 요소와 함께 작동하도록 만드는 데 자주 사용됩니다.

어댑터 패턴은 구조적 패턴의 일종으로 소프트웨어 개발에서 가장 많이 사용되는 디자인 패턴 중 하나입니다. 어댑터 패턴은 호환되지 않는 인터페이스 문제를 해결하는 데 사용됩니다.

이번 글에서는 Spring Boot 개발에서 어댑터 패턴을 어떻게 사용하는지 살펴보도록 하겠습니다. 또한 어댑터 패턴이 실제로 어떻게 사용될 수 있는지 설명하기 위해 몇 가지 코드 예제를 살펴보겠습니다.

## 어댑터 패턴이란?

앞에서 언급했듯이 어댑터 패턴은 소프트웨어 구성 요소가 일반적으로 작동할 수 없는 다른 소프트웨어 구성 요소와 작동할 수 있도록 하는 소프트웨어 설계 패턴입니다.

어댑터 패턴은 래퍼 패턴이라고도 합니다. 어댑터 패턴은 호환되지 않는 인터페이스 문제를 해결하는 데 사용됩니다.

어댑터 패턴은 구조적 패턴의 일종으로 소프트웨어 개발에서 가장 많이 사용되는 디자인 패턴 중 하나입니다. 어댑터 패턴은 호환되지 않는 인터페이스 문제를 해결하는 데 사용됩니다.

어댑터 패턴에는 클래스 어댑터 패턴과 개체 어댑터 패턴의 두 가지 유형이 있습니다.

## 클래스 어댑터 패턴

클래스 어댑터 패턴은 상속을 사용하여 한 클래스를 다른 클래스에 적응시키는 일종의 어댑터 패턴입니다.

클래스 어댑터 패턴에서 어댑터 클래스는 어댑터 클래스에서 상속됩니다. 어댑터 클래스는 대상 인터페이스를 구현하고 대상 인터페이스 메서드를 Adaptee 클래스에 위임합니다.

다음은 Java에서 클래스 어댑터 패턴을 사용할 수 있는 방법의 예입니다.

Adaptee 클래스인 `Logger`라는 클래스가 있습니다. `Logger` 클래스에는 `log()`라는 메서드가 있습니다.

```java
public class Logger {
   public void log(String message) {
      // log the message
   }
}
```

어댑터 클래스인 `ConsoleLogger`라는 클래스도 있습니다. `ConsoleLogger` 클래스는 `Logger` 클래스에서 상속됩니다. `ConsoleLogger` 클래스는 `Logger` 인터페이스를 구현하고 `log()` 메서드를 `Logger` 클래스에 위임합니다.

```java
public class ConsoleLogger extends Logger implements Logger {
   public void log(String message) {
      super.log(message);
   }
}
```

## 객체 어댑터 패턴

개체 어댑터 패턴은 구성을 사용하여 한 개체를 다른 개체에 적응시키는 어댑터 패턴 유형입니다.

개체 어댑터 패턴에서 어댑터 클래스는 Adaptee 클래스의 인스턴스를 포함합니다. 어댑터 클래스는 대상 인터페이스를 구현하고 대상 인터페이스 메서드를 Adaptee 클래스에 위임합니다.

다음은 Java에서 객체 어댑터 패턴을 사용하는 방법의 예입니다.

Adaptee 클래스인 `Logger`라는 클래스가 있습니다. `Logger` 클래스에는 `log()`라는 메서드가 있습니다.

```java
public class Logger {
   public void log(String message) {
      // log the message
   }
}
```

어댑터 클래스인 `ConsoleLogger`라는 클래스도 있습니다. `ConsoleLogger` 클래스는 `Logger` 클래스의 인스턴스를 포함합니다. `ConsoleLogger` 클래스는 `Logger` 인터페이스를 구현하고 `log()` 메서드를 `Logger` 클래스에 위임합니다.

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

## Spring Boot에서 어댑터 패턴을 사용하는 방법은 무엇입니까?

이 섹션에서는 Spring Boot 개발에서 어댑터 패턴을 사용하는 방법을 살펴보겠습니다.

예제에서는 클래스 어댑터 패턴을 사용합니다.

### 예 1

이 예제에서는 어댑터 패턴을 사용하여 `Logger` 클래스를 `ConsoleLogger` 클래스에 적용합니다.

먼저 `Logger` 클래스를 만들어야 합니다.

```java
public class Logger {
   public void log(String message) {
      // log the message
   }
}
```

다음으로 `ConsoleLogger` 클래스를 만들어야 합니다. `ConsoleLogger` 클래스는 `Logger` 클래스에서 상속됩니다. `ConsoleLogger` 클래스는 `Logger` 인터페이스를 구현하고 `log()` 메서드를 `Logger` 클래스에 위임합니다.

```java
public class ConsoleLogger extends Logger implements Logger {
   public void log(String message) {
      super.log(message);
   }
}
```

이제 Spring Boot 애플리케이션에서 `ConsoleLogger` 클래스를 사용할 수 있습니다.

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

`logger()` 메서드에서 `ConsoleLogger` 클래스인 `Logger` 유형의 빈을 생성합니다.

이제 애플리케이션에 `Logger` 빈을 주입하고 이를 사용하여 메시지를 기록할 수 있습니다.

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

`MyComponent` 클래스에서 `Logger` 빈을 `logger` 필드에 주입합니다. 그런 다음 `logger` 필드를 사용하여 메시지를 기록합니다.

### 예 2

이 예제에서는 어댑터 패턴을 사용하여 `RestTemplate` 클래스를 `MyRestTemplate` 클래스에 적용합니다.

먼저 `RestTemplate` 클래스를 만들어야 합니다.

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

다음으로 `MyRestTemplate` 클래스를 만들어야 합니다. `MyRestTemplate` 클래스는 `RestTemplate` 클래스에서 상속됩니다. `MyRestTemplate` 클래스는 `RestTemplate` 인터페이스를 구현하고 `getForObject()` 및 `postForObject()` 메서드를 `RestTemplate` 클래스에 위임합니다.

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

이제 Spring Boot 애플리케이션에서 `MyRestTemplate` 클래스를 사용할 수 있습니다.

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

`restTemplate()` 메서드에서 `MyRestTemplate` 클래스인 `RestTemplate` 유형의 빈을 생성합니다.

이제 애플리케이션에 `RestTemplate` 빈을 주입하고 이를 사용하여 HTTP 요청을 할 수 있습니다.

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

`MyComponent` 클래스에서 `RestTemplate` 빈을 `restTemplate` 필드에 주입합니다. 그런 다음 `restTemplate` 필드를 사용하여 `http://example.com` URL에 GET 요청을 합니다.

## 결론

이 기사에서는 Spring Boot 개발에서 어댑터 패턴을 사용하는 방법을 살펴보았습니다. 어댑터 패턴이 실제로 어떻게 사용될 수 있는지 설명하기 위해 몇 가지 코드 예제도 살펴보았습니다.