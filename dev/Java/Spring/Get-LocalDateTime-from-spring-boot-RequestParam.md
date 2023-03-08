---
title: [Spring Boot] @RequestParam 에서 LocalDateTime 받기
description: 
published: true
date: 2023-02-17T17:59:59.745Z
tags: springboot
editor: markdown
dateCreated: 2022-12-13T15:42:42.513Z
---

- [[Spring Boot] Getting LocalDateTime with @RequestParam***English** version of this document is available*](/en/dev/Java/Spring/Get-LocalDateTime-from-spring-boot-RequestParam)
{.links-list}

## Issue

### API
```java
@GetMapping("/v1/something/find-all")
public List<Object> findAllSomething(
  @RequestParam LocalDateTime localDateTime
) {
  return Collections.emptyList();
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

- 위와 같이 구성하고 API 를 호출하면 `ConversionFailedException`이 발생한다.

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

- HTTP Query String 으로 넘어가는 `RequestParam` 은 String 으로 취급된다.
- `String` -> `LocalDateTime` 형 변환에 spring boot 가 참고할 수 있는 추가 어노테이션을 설정한다.

### API
```java
@GetMapping("/v1/something/find-all")
public List<Object> findAllSomething(
  @RequestParam @DateTimeFormat(pattern = "yyyy-MM-dd'T'HH:mm:ss") LocalDateTime localDateTime
) {
  return Collections.emptyList();
}
```

### Caller

- Caller 에서도 가급적 API 에서 지정한 `DateTimeFormat` 맞춰준다.

```java
public static final DateTimeFormatter ISO_LOCAL_DATE_TIME_WITHOUT_NANO_FORMATTER = DateTimeFormatter.ofPattern("yyyy-MM-dd'T'HH:mm:ss");

public List<Object> getAllSomething(LocalDateTime localDateTime) {
  return webClient.get()
      .uri("/v1/something/find-all", uriBuilder -> uriBuilder
          .queryParam("localDateTime", localDateTime.format(ISO_LOCAL_DATE_TIME_WITHOUT_NANO_FORMATTER))
          .build())
      .retrieve()
      .bodyToFlux(Object.class)
      .collectList()
      .block();
}
```

> 사실 Caller 에서만 포맷팅 정리해서 nano seconds 아래를 날려주면 API 가 정상 호출되는것 같은데, 그래도 웬만하면 둘 다 맞춰준다.