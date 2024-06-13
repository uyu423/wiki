---
title: Correct SpringBoot WebClient URI assembly usage
description: 
published: true
date: 2024-06-13T09:45:39.129Z
tags: java, kotlin, springboot, webclient
editor: markdown
dateCreated: 2024-06-13T09:45:39.129Z
---

# Spring Boot 2.x

- There is a known issue when composing a URI with WebClient as shown below:

```java
webClient.get()
  .uri(
    uriBuilder -> uriBuilder.path("/v1/api/user/{id}").build(idNo)
  )
// ...
```

- In this case, the `uri()` method parameter passes the fully constructed URI through the uriBuilder.
- This can lead to excessive metric collection and potentially high memory usage.
  - Example: `/v1/api/user/1234`, `/v1/api/user/2345` ...
- To collect metrics correctly, the URI should be collected in the template form `/v1/api/user/{idNo}`.
- To achieve this, pass the URI template and its arguments directly to the `uri()` method as shown below:

```java
webClient.get()
  .uri("/v1/api/user/{id}", idNo)
// ...
```

- By enabling Spring Boot Actuator, you can observe the difference through the `http.client.requests` metric.

## Related Links
- [Avoiding memory leaks with Spring Boot WebClient*bol.Techlab*](https://techlab.bol.com/en/blog/avoiding-memory-leaks-with-spring-boot-webclient/)
- [High memory usage in JVM level...*stackoverflow*](https://stackoverflow.com/questions/73984968/high-memory-usage-in-jvm-level-org-springframework-boot-actuate-autoconfigure)
- [Expose Metrics of Spring WebClient using Spring Boot Actuator*rieckpil.de*](https://rieckpil.de/expose-metrics-of-spring-webclient-using-spring-boot-actuator/)
{.links-list}

# Spring Boot 3.x

- From Boot 3.x onwards, this issue has been acknowledged, and metrics collection is not performed if the URI is determined to be dynamically generated.
- When calling WebClient with the code that was problematic in 2.x, you will see that the `uri` tag value of the `http.client.requests` metric remains "none".
- To avoid potential side effects in future metric or log collection, avoid generating URL strings through `uriBuilder` and passing them to `uri()` as you would in 2.x.

## Related Links

- [Why the URI tag gets “none” value in http_client_request metrics with Spring Boot 3*medium.com/@wei.shen168*](https://medium.com/@wei.shen168/why-the-uri-tag-gets-none-value-in-http-client-request-metrics-with-spring-boot-3-9aacc346ff52)
{.links-list}

# Conclusion

- Simply avoid using `UriBuilder.path` to maintain peace of mind.

## For simple fixed string URLs

```java
webClient.get().uri("/v1/api/simple")...
```

## When path variables are needed

```java
webClient.get().uri("/v1/api/{id}", id)...
```

## When query parameters are also needed

```java
webClient.get()
  .uri(uriBuilder -> uriBuilder
    .path("/v1/api/{id}")
    .queryParam("queryParam1", queryParam1)
    .build(id)
  )
  ...
```