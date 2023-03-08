---
title: Spring Boot 和使用 Spring WebFlux 的响应式编程
description: 
published: true
date: 2023-02-01T03:18:35.867Z
tags: 
editor: markdown
dateCreated: 2023-02-01T03:18:31.790Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Spring Boot and Reactive Programming with Spring WebFlux***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-reactive-programming-with-spring-webflux)
{.links-list}


  此博客的目标受众是想要了解 Spring Boot 和使用 Spring WebFlux 进行响应式编程的 IT 开发专业人士。


# Spring Boot 和使用 Spring WebFlux 的响应式编程

Spring Boot 是一种流行的 Java 应用程序框架，允许开发人员快速创建和部署 Web 应用程序。 Spring Boot 建立在 Spring Framework 之上并使用 Java 平台。

响应式编程是一种编程范式，有助于编写响应速度更快、更有弹性的代码。它是一种非阻塞和异步的事件驱动编程风格。

Spring WebFlux 是一种基于 Spring Framework 构建的 Web 应用程序的反应式编程模型。它是完全非阻塞的，支持背压，并使用事件循环执行模型。

在本文中，我们将了解如何使用 Spring Boot 和 Spring WebFlux 来创建响应式 Web 应用程序。我们还将研究如何使用 Reactive Streams API 来创建事件流。

## 设置 Spring Boot 项目

我们需要做的第一件事是创建一个新的 Spring Boot 项目。我们可以使用 Spring Initializr 网站来生成一个包含我们需要的依赖项的项目。

我们需要选择以下依赖项：

* Web - 用于网络应用程序
* Reactive Web - 用于反应式编程模型
* Lombok - 用于简化样板代码

![Spring Initializr](https://i.imgur.com/Rv4U2in.png)

项目生成后，我们可以将其导入到我们喜欢的 IDE 中。我将使用 IntelliJ IDEA。

## 你好世界

让我们从创建一个简单的 Hello World Web 应用程序开始。我们将创建一个向客户端返回字符串的控制器。

首先，我们需要在 com.example.demo 包中创建一个名为 HelloController.java 的新文件。

```java
package com.example.demo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello, World!";
    }

}
```

在 `HelloController` 类中，我们用 `@RestController` 注释了该类。此注释用于将类标记为 Web 控制器。

我们还用 `@GetMapping` 注释了 `hello()` 方法。此注释用于将 HTTP GET 请求映射到“hello()”方法。

`hello()` 方法返回一个字符串。该字符串将被转换为 JSON 并返回给客户端。

我们现在可以运行应用程序并访问“/hello”端点。我们应该看到以下输出：

```
Hello, World!
```

## 反应流

Reactive Streams 是一种用于非阻塞背压异步流处理的 API。它由四个接口组成：

* Publisher - 发出数据流
* 订阅者 - 消费数据流
* 处理器 - 转换数据流
* 订阅 - 表示发布者和订阅者之间的一对一关系

Reactive Streams 不依赖于任何特定的编程语言或平台。它与语言无关，可以与任何基于 JVM 的语言一起使用。

## 创建流

现在让我们看看如何使用 Reactive Streams API 来创建事件流。我们将使用 `Publisher` 接口来发出整数流。

首先，我们需要在 com.example.demo 包中创建一个名为 Publisher.java 的新文件。

```java
package com.example.demo;

import org.reactivestreams.Publisher;
import org.reactivestreams.Subscriber;
import org.reactivestreams.Subscription;

import java.util.concurrent.atomic.AtomicInteger;

public class Publisher implements org.reactivestreams.Publisher<Integer> {

    private Subscriber<? super Integer> subscriber;
    private AtomicInteger counter;

    public Publisher() {
        this.counter = new AtomicInteger();
    }

    @Override
    public void subscribe(Subscriber<? super Integer> s) {
        this.subscriber = s;
        this.subscriber.onSubscribe(new Subscription() {
            @Override
            public void request(long n) {
                for (int i = 0; i < n; i++) {
                    if (counter.incrementAndGet() > 10) {
                        subscriber.onComplete();
                        break;
                    } else {
                        subscriber.onNext(counter.get());
                    }
                }
            }

            @Override
            public void cancel() {

            }
        });
    }
}
```

在 Publisher 类中，我们从 Publisher 接口实现了 subscribe() 方法。此方法用于将 `Subscriber` 订阅到流。

在 subscribe() 方法中，我们使用匿名的 Subscription 对象。该对象用于从 `Publisher` 请求数据。我们向 `Publisher` 请求 10 个项目。

我们还使用 `AtomicInteger` 来跟踪 `Publisher` 发出的项目数。

## 订阅流

我们现在可以订阅 `Publisher` 发出的事件流。我们将使用 `Publisher` 接口中的 `subscribe()` 方法。

首先，我们需要在 com.example.demo 包中创建一个名为 Subscriber.java 的新文件。

```java
package com.example.demo;

import org.reactivestreams.Subscriber;
import org.reactivestreams.Subscription;

public class Subscriber implements org.reactivestreams.Subscriber<Integer> {

    @Override
    public void onSubscribe(Subscription s) {
        s.request(Long.MAX_VALUE);
    }

    @Override
    public void onNext(Integer integer) {
        System.out.println("Received: " + integer);
    }

    @Override
    public void onError(Throwable t) {
        t.printStackTrace();
    }

    @Override
    public void onComplete() {
        System.out.println("Done!");
    }
}
```

在 `Subscriber` 类中，我们从 `Subscriber` 接口实现了 `onSubscribe()` 方法。此方法用于订阅事件流。

在 `onSubscribe()` 方法中，我们请求来自 `Publisher` 的无限事件流。

我们还实现了 `onNext()`、`onError()` 和 `onComplete()` 方法。当 `Publisher` 发出事件时，将调用这些方法。

## 测试流

我们现在可以测试 `Publisher` 发出的事件流。

首先，我们需要在 com.example.demo 包中创建一个名为 DemoApplicationTests.java 的新文件。

```java
package com.example.demo;

import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class DemoApplicationTests {

    @Test
    public void testStream() {
        Publisher publisher = new Publisher();
        Subscriber subscriber = new Subscriber();
        publisher.subscribe(subscriber);
    }

}
```

在“DemoApplicationTests”类中，我们创建了一个“testStream()”方法。在这个方法中，我们创建了一个 `Publisher` 和 `Subscriber`。然后我们将 `Subscriber` 订阅到 `Publisher`。

如果我们运行测试，我们应该看到以下输出：

```
Received: 1
Received: 2
Received: 3
Received: 4
Received: 5
Received: 6
Received: 7
Received: 8
Received: 9
Received: 10
Done!
```

## 创建响应式 Web 应用程序

现在我们已经了解了如何使用 Reactive Streams API，让我们看看如何使用它来创建反应式 Web 应用程序。

反应式 Web 应用程序是使用反应式编程模型的 Web 应用程序。在反应式编程模型中，应用程序构建为一组小型、独立且并发的进程，这些进程使用消息传递相互通信。

在反应式 Web 应用程序中，Web 应用程序构建为一组小型、独立且并发的进程，这些进程使用消息传递相互通信。

## 你好反应世界

让我们从创建一个简单的“Hello Reactive World”Web 应用程序开始。我们将创建一个向客户端返回字符串的控制器。

首先，我们需要在 com.example.demo 包中创建一个名为 HelloReactiveController.java 的新文件。

```java
package com.example.demo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;
import reactor.core.publisher.Mono;

@RestController
public class HelloReactiveController {

    @GetMapping("/hello-reactive")
    public Mono<String> helloReactive() {
        return Mono.just("Hello, Reactive World!");
    }

}
```

在 HelloReactiveController 类中，我们用 @RestController 注释了该类。此注释用于将类标记为 Web 控制器。

我们还用 `@GetMapping` 注释了 `helloReactive()` 方法。此注释用于将 HTTP GET 请求映射到“helloReactive()”方法。

`helloReactive()` 方法返回一个 `Mono<String>`。 `Mono` 是一个反应流，它发出 0 或 1 个项目。在这种情况下，`Mono` 发出单个字符串。

我们现在可以运行应用程序并访问“/hello-reactive”端点。我们应该看到以下输出：

```
Hello, Reactive World!
```

## 创建反应流

现在我们已经了解了如何创建一个简单的响应式 Web 应用程序，让我们看看如何创建一个更复杂的响应式流。

我们将创建一个由 `Publisher` 发出的整数流。然后，我们将使用“处理器”将整数流转换为字符串流。最后，我们将使用 `Subscriber` 来消费字符串流。

首先，我们需要在 com.example.demo 包中创建一个名为 Publisher.java 的新文件。

```java
package com.example.demo;

import org.reactivestreams.Publisher;
import org.reactivestreams.Subscriber;
import org.reactivestreams.Subscription;

import java.util.concurrent.atomic.AtomicInteger;

public class Publisher implements org.reactivestreams.Publisher<Integer> {

    private Subscriber<? super Integer> subscriber;
    private AtomicInteger counter;

    public Publisher() {
        this.counter = new AtomicInteger();
    }

    @Override
    public void subscribe(Subscriber<? super Integer> s) {
        this.subscriber = s;
        this.subscriber.onSubscribe(new Subscription() {
            @Override
            public void request(long n) {
                for (int i = 0; i < n; i++) {
                    if (counter.incrementAndGet() > 10) {
                        subscriber.onComplete();
                        break;
                    } else {
                        subscriber.onNext(counter.get());
                    }
                }
            }

            @Override
            public void cancel() {

            }
        });
    }
}
```

在 Publisher 类中，我们从 Publisher 接口实现了 subscribe() 方法。此方法用于将 `Subscriber` 订阅到流。

在 subscribe() 方法中，我们使用匿名的 Subscription 对象。该对象用于从 `Publisher` 请求数据。我们向 `Publisher` 请求 10 个项目。

我们还使用 `AtomicInteger` 来跟踪 `Publisher` 发出的项目数。

## 转换流

我们现在可以使用“处理器”将整数流转换为字符串流。我们将使用 `Processor` 接口中的 `map()` 方法将每个整数转换为字符串。

首先，我们需要在 com.example.demo 包中创建一个名为 Processor.java 的新文件。

```java
package com.example.demo;

import org.reactivestreams.Processor;
import org.reactivestreams.Subscriber;
import org.reactivestreams.Subscription;

public class Processor implements org.reactivestreams.Processor<Integer, String> {

    private Subscriber<? super String> subscriber;
    private Subscription subscription;

    @Override
    public void subscribe(Subscriber<? super String> s) {
        this.subscriber = s;
        this.subscriber.onSubscribe(new Subscription() {
            @Override
            public void request(long n) {
                subscription.request(n);
            }

            @Override
            public void cancel() {
                subscription.cancel();
            }
        });
    }

    @Override
    public void onSubscribe(Subscription s) {
        this.subscription = s;
        this.subscription.request(Long.MAX_VALUE);
    }

    @Override
    public void onNext(Integer integer) {
        this.subscriber.onNext(integer.toString());
    }

    @Override
    public void onError(Throwable t) {
        this.subscriber.onError(t);
    }

    @Override
    public void onComplete() {
        this.subscriber.onComplete();
    }
}
```

在 `Processor` 类中，我们实现了 `Processor` 接口中的 `subscribe()` 和 `onSubscribe()` 方法。这些方法用于将 `Subscriber` 订阅到流。

在 subscribe() 方法中，我们使用匿名的 Subscription 对象。该对象用于从 `Publisher` 请求数据。我们正在向 `Publisher` 请求无限制的事件流。

我们还使用 `AtomicInteger` 来跟踪 `Publisher` 发出的项目数。

## 消费流

我们现在可以使用 `Subscriber` 来消费 `Processor` 发出的字符串流。

首先，我们需要在 com.example.demo 包中创建一个名为 Subscriber.java 的新文件。

```java
package com.example.demo;

import org.reactivestreams.Subscriber;
import org.reactivestreams.Subscription;

public class Subscriber implements org.reactivestreams.Subscriber<String> {

    @Override
    public void onSubscribe(Subscription s) {
        s.request(Long.MAX_VALUE);
    }

    @Override
    public void onNext(String s) {
        System.out.println("Received: " + s);
    }

    @Override
    public void onError(Throwable t) {
        t.printStackTrace();
    }

    @Override
    public void onComplete() {
        System.out.println("Done!");
    }
}
```

在 `Subscriber` 类中，我们实现了 `onSubscribe()` 方法