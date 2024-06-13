---
title: 올바른 SpringBoot WebClient URI 사용법
description: 
published: true
date: 2024-06-13T09:43:40.932Z
tags: java, kotlin, springboot, webclient
editor: markdown
dateCreated: 2024-06-13T09:43:40.932Z
---

# Spring Boot 2.x

- WebClient 에서 아래와 같이 uri 를 조합했을 떄 발생하는 유명한 이슈가 있음

```java
webClient.get()
  .uri(
    uriBuilder -> uriBuilder.path("/v1/api/user/{id}").build(idNo)
  )
// ...
```

- 이 경우에 `uri()` 메서드 파라미터로 uriBuilder를 통해 완성된 uri 가 넘어가게됨
- 따라서 메트릭이 과도하게 수집되어 과도한 메모리 점유 가능성 있음
  - ex: `/v1/api/user/1234`, `/v1/api/user/2345` ...
- 메트릭이 올바르게 수집되려면 `/v1/api/user/{idNo}` uri template 형태로 수집되어야함
- 그러려면 아래와 같이 `uri()` 메서드 자체에 완성된 uri 가 아닌 uri template과 그 인자들을 직접 념겨줘야함

```java
webClient.get()
  .uri("/v1/api/user/{id}", idNo)
// ...
```

- Spring Boot Actuator 를 활성화 시켜서 `http.client.requests` metric 를 통해 차이를 확인할 수 있음

## 관련 링크
- [Avoiding memory leaks with Spring Boot WebClient*bol.Techlab*](https://techlab.bol.com/en/blog/avoiding-memory-leaks-with-spring-boot-webclient/)
- [High memory usage in JVM level...*stackoverflow*](https://stackoverflow.com/questions/73984968/high-memory-usage-in-jvm-level-org-springframework-boot-actuate-autoconfigure)
- [Expose Metrics of Spring WebClient using Spring Boot Actuator*rieckpil.de*](https://rieckpil.de/expose-metrics-of-spring-webclient-using-spring-boot-actuator/)
{.links-list}


# Spring Boot 3.x

- Boot 3.x 부터는 위 이슈가 인지 되었는지 uri 가 동적으로 생성 판단될 경우 metric 수집을 하지 않음
- 2.x 에서 이슈가 된 코드로 WebClient 호출해보면 `http.client.requets` metric의 uri tag value가 "none" 으로 남는 것을 확인 할 수 있음
- 향후에 메트릭 지표나 로그 수집시 다른 사이드 이펙트가 있을 수 있음므로, 2.x 와 마찬가지로 uriBuilder 를 통해 url string 생성 후 `uri()` 로 전달하는 것을 지양해야함

## 관련 링크

- [Why the URI tag gets “none” value in http_client_request metrics with Spring Boot 3*medium.com/@wei.shen168*](https://medium.com/@wei.shen168/why-the-uri-tag-gets-none-value-in-http-client-request-metrics-with-spring-boot-3-9aacc346ff52)
{.links-list}

# 결론

- 그냥 `UriBuilder.path` 를 사용하지 않는 것이 심신에 도움이된다.

## 단순 고정 String URL 의 경우

```java
webClient.get().uri("/v1/api/simple")...
```

## path variable 필요한 경우

```java
webClient.get().uri("/v1/api/{id}", id)...
```

## query param 까지 필요한 경우

```java
webClient.get()
  .uri("/v1/api/{id}", uriBuilder -> uriBuilder
	  .queryParam("queryParam1", queryParam1)
  	.build(id)
  )
  ...
```