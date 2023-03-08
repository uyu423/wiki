---
title: Spring Boot and Reactive Programming with Spring WebFlux
description: 
published: true
date: 2023-02-01T03:18:33.522Z
tags: 
editor: markdown
dateCreated: 2023-02-01T03:18:31.780Z
---

- [Spring WebFlux를 사용한 Spring Boot 및 반응형 프로그래밍***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-and-reactive-programming-with-spring-webflux)
{.links-list}
- [Spring WebFlux を使用した Spring Boot とリアクティブ プログラミング***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/spring-boot-and-reactive-programming-with-spring-webflux)
{.links-list}
- [Spring Boot 和使用 Spring WebFlux 的响应式编程***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-and-reactive-programming-with-spring-webflux)
{.links-list}


  The target audience for this blog is IT Development professionals who want to learn about Spring Boot and Reactive Programming with Spring WebFlux.


# Spring Boot and Reactive Programming with Spring WebFlux

Spring Boot is a popular Java application framework that allows developers to quickly create and deploy web applications. Spring Boot is built on top of the Spring Framework and uses the Java platform.

Reactive programming is a programming paradigm that helps to write code that is more responsive and resilient. It is an event-driven programming style that is non-blocking and asynchronous.

Spring WebFlux is a reactive programming model for web applications that is built on top of the Spring Framework. It is fully non-blocking, supports backpressure, and uses an event-loop execution model.

In this article, we will look at how to use Spring Boot and Spring WebFlux to create a reactive web application. We will also look at how to use the Reactive Streams API to create a stream of events.

## Setting up a Spring Boot Project

The first thing we need to do is to create a new Spring Boot project. We can use the Spring Initializr website to generate a project with the dependencies we need.

We need to select the following dependencies:

* Web - for the web application
* Reactive Web - for the reactive programming model
* Lombok - for simplifying the boilerplate code

![Spring Initializr](https://i.imgur.com/Rv4U2in.png)

Once the project is generated, we can import it into our favorite IDE. I will be using IntelliJ IDEA.

## Hello World

Let's start by creating a simple Hello World web application. We will create a controller that returns a string to the client.

First, we need to create a new file called `HelloController.java` in the `com.example.demo` package.

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

In the `HelloController` class, we have annotated the class with `@RestController`. This annotation is used to mark a class as a web controller.

We have also annotated the `hello()` method with `@GetMapping`. This annotation is used to map an HTTP GET request to the `hello()` method.

The `hello()` method returns a string. This string will be converted to JSON and returned to the client.

We can now run the application and access the `/hello` endpoint. We should see the following output:

```
Hello, World!
```

## Reactive Streams

Reactive Streams is an API for asynchronous stream processing with non-blocking backpressure. It consists of four interfaces:

* Publisher - emits a stream of data
* Subscriber - consumes a stream of data
* Processor - transforms a stream of data
* Subscription - represents a one-to-one relationship between a Publisher and a Subscriber

Reactive Streams is not tied to any specific programming language or platform. It is language agnostic and can be used with any JVM-based language.

## Creating a Stream

Let's now look at how to use the Reactive Streams API to create a stream of events. We will use the `Publisher` interface to emit a stream of integers.

First, we need to create a new file called `Publisher.java` in the `com.example.demo` package.

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

In the `Publisher` class, we have implemented the `subscribe()` method from the `Publisher` interface. This method is used to subscribe a `Subscriber` to the stream.

In the `subscribe()` method, we are using an anonymous `Subscription` object. This object is used to request data from the `Publisher`. We are requesting 10 items from the `Publisher`.

We are also using an `AtomicInteger` to keep track of the number of items emitted by the `Publisher`.

## Subscribing to a Stream

We can now subscribe to the stream of events emitted by the `Publisher`. We will use the `subscribe()` method from the `Publisher` interface.

First, we need to create a new file called `Subscriber.java` in the `com.example.demo` package.

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

In the `Subscriber` class, we have implemented the `onSubscribe()` method from the `Subscriber` interface. This method is used to subscribe to a stream of events.

In the `onSubscribe()` method, we are requesting an unbounded stream of events from the `Publisher`.

We have also implemented the `onNext()`, `onError()`, and `onComplete()` methods. These methods are called when an event is emitted by the `Publisher`.

## Testing the Stream

We can now test the stream of events emitted by the `Publisher`.

First, we need to create a new file called `DemoApplicationTests.java` in the `com.example.demo` package.

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

In the `DemoApplicationTests` class, we have created a `testStream()` method. In this method, we are creating a `Publisher` and `Subscriber`. We are then subscribing the `Subscriber` to the `Publisher`.

If we run the test, we should see the following output:

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

## Creating a Reactive Web Application

Now that we have seen how to use the Reactive Streams API, let's look at how to use it to create a reactive web application.

A reactive web application is a web application that uses a reactive programming model. In a reactive programming model, an application is built as a set of small, independent, and concurrent processes that communicate with each other using message passing.

In a reactive web application, the web application is built as a set of small, independent, and concurrent processes that communicate with each other using message passing.

## Hello Reactive World

Let's start by creating a simple "Hello Reactive World" web application. We will create a controller that returns a string to the client.

First, we need to create a new file called `HelloReactiveController.java` in the `com.example.demo` package.

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

In the `HelloReactiveController` class, we have annotated the class with `@RestController`. This annotation is used to mark a class as a web controller.

We have also annotated the `helloReactive()` method with `@GetMapping`. This annotation is used to map an HTTP GET request to the `helloReactive()` method.

The `helloReactive()` method returns a `Mono<String>`. A `Mono` is a reactive stream that emits 0 or 1 items. In this case, the `Mono` emits a single string.

We can now run the application and access the `/hello-reactive` endpoint. We should see the following output:

```
Hello, Reactive World!
```

## Creating a Reactive Stream

Now that we have seen how to create a simple reactive web application, let's look at how to create a more complex reactive stream.

We will create a stream of integers that are emitted by a `Publisher`. We will then use a `Processor` to transform the stream of integers into a stream of strings. Finally, we will use a `Subscriber` to consume the stream of strings.

First, we need to create a new file called `Publisher.java` in the `com.example.demo` package.

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

In the `Publisher` class, we have implemented the `subscribe()` method from the `Publisher` interface. This method is used to subscribe a `Subscriber` to the stream.

In the `subscribe()` method, we are using an anonymous `Subscription` object. This object is used to request data from the `Publisher`. We are requesting 10 items from the `Publisher`.

We are also using an `AtomicInteger` to keep track of the number of items emitted by the `Publisher`.

## Transforming the Stream

We can now use a `Processor` to transform the stream of integers into a stream of strings. We will use the `map()` method from the `Processor` interface to transform each integer into a string.

First, we need to create a new file called `Processor.java` in the `com.example.demo` package.

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

In the `Processor` class, we have implemented the `subscribe()` and `onSubscribe()` methods from the `Processor` interface. These methods are used to subscribe a `Subscriber` to the stream.

In the `subscribe()` method, we are using an anonymous `Subscription` object. This object is used to request data from the `Publisher`. We are requesting an unbounded stream of events from the `Publisher`.

We are also using an `AtomicInteger` to keep track of the number of items emitted by the `Publisher`.

## Consuming the Stream

We can now use a `Subscriber` to consume the stream of strings emitted by the `Processor`.

First, we need to create a new file called `Subscriber.java` in the `com.example.demo` package.

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

In the `Subscriber` class, we have implemented the `onSubscribe()` method