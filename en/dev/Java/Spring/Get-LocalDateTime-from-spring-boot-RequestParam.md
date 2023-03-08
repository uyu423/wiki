---
title: [Spring Boot] Getting LocalDateTime with @RequestParam
description: 
published: true
date: 2023-02-17T18:00:18.939Z
tags: english, springboot
editor: markdown
dateCreated: 2022-12-24T19:39:41.600Z
---

- [[Spring Boot] @RequestParam 에서 LocalDateTime 받기***Korean** version of this document is available*](/ko/dev/Java/Spring/Get-LocalDateTime-from-spring-boot-RequestParam)
{.links-list}

## Issue

### API
```java
@GetMapping("/v1/something/find-all")
public List<Object> findAllSomething(
   @RequestParam LocalDateTime localDateTime
) {
   return Collections. emptyList();
}
```

### Caller

```java
public List<Object> getAllSomething(LocalDateTime localDateTime) {
   return webClient.get()
       .uri("/v1/something/find-all", uriBuilder -> uriBuilder
           .queryParam("localDateTime", localDateTime)
           .build())
       .retrieve()
       .bodyToFlux(Object.class)
       .collectList()
       .block();
}
```

- If you configure as above and call the API, `ConversionFailedException` occurs.

```
org.springframework.web.method.annotation.MethodArgumentTypeMismatchException: Failed to convert value of type 'java.lang.String' to required type 'java.time.LocalDateTime'; nested exception is org.springframework.core.convert.ConversionFailedException: Failed to convert from type [java.lang.String] to type [@org.springframework.web.bind.annotation.RequestParam @org.springframework.format.annotation.DateTimeFormat java.time.LocalDateTime] for value '2022-12-07T00:36:43.689561'; nested exception is java.lang.IllegalArgumentException: Parse attempt failed for value [2022-12-07T00:36:43.689561]
at org.springframework.web.method.annotation.AbstractNamedValueMethodArgumentResolver.resolveArgument(AbstractNamedValueMethodArgumentResolver.java:133)
at org.springframework.web.method.support.HandlerMethodArgumentResolverComposite.resolveArgument(HandlerMethodArgumentResolverComposite.java:122)
at org.springframework.web.method.support.InvocableHandlerMethod.getMethodArgumentValues(InvocableHandlerMethod.java:179)
at org.springframework.web.method.support.InvocableHandlerMethod.invokeForRequest(InvocableHandlerMethod.java:146)
at org.springframework.web.servlet.mvc.method.annotation.ServletInvocableHandlerMethod.invokeAndHandle(ServletInvocableHandlerMethod.java:117)
at org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter.invokeHandlerMethod(RequestMappingHandlerAdapter.java:895)
at org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter.handleInternal(RequestMappingHandlerAdapter.java:808)
at org.springframework.web.servlet.mvc.method.AbstractHandlerMethodAdapter.handle(AbstractHandlerMethodAdapter.java:87)
at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:1067)
at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:963)
at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:1006)
at org.springframework.web.servlet.FrameworkServlet.doGet(FrameworkServlet.java:898)
  
```

## Solution

- `RequestParam` passed as HTTP Query String is treated as String.
- Set additional annotations that spring boot can refer to `String` -> `LocalDateTime` type conversion.

### API
```java
@GetMapping("/v1/something/find-all")
public List<Object> findAllSomething(
   @RequestParam @DateTimeFormat(pattern = "yyyy-MM-dd'T'HH:mm:ss") LocalDateTime localDateTime
) {
   return Collections. emptyList();
}
```

### Caller

- Even in the Caller, match the `DateTimeFormat` specified in the API as much as possible.

```java
public static final DateTimeFormatter ISO_LOCAL_DATE_TIME_WITHOUT_NANO_FORMATTER = DateTimeFormatter.ofPattern("yyyy-MM-dd'T'HH:mm:ss");

public List<Object> getAllSomething(LocalDateTime localDateTime) {
   return webClient. get()
       .uri("/v1/something/find-all", uriBuilder -> uriBuilder
           .queryParam("localDateTime", localDateTime.format(ISO_LOCAL_DATE_TIME_WITHOUT_NANO_FORMATTER))
           .build())
       .retrieve()
       .bodyToFlux(Object.class)
       .collectList()
       .block();
}
```

> In fact, if you organize the formatting only in Caller and blow out the nano seconds, the API seems to be called normally, but if you can, both are matched.