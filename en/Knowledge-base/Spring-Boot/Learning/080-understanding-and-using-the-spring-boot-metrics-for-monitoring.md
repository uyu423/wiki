---
title: 080: Understanding and Using the Spring Boot Metrics for Monitoring
description: 
published: true
date: 2023-02-05T11:32:21.268Z
tags: 
editor: markdown
dateCreated: 2023-02-05T11:32:19.685Z
---

- [080: Comprensión y uso de las métricas de Spring Boot para el monitoreo***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/080-understanding-and-using-the-spring-boot-metrics-for-monitoring)
{.links-list}
- [080：了解和使用 Spring Boot 指标进行监控***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/080-understanding-and-using-the-spring-boot-metrics-for-monitoring)
{.links-list}
- [080: 모니터링을 위한 Spring Boot 메트릭 이해 및 사용***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/080-understanding-and-using-the-spring-boot-metrics-for-monitoring)
{.links-list}


# Introduction

Monitoring is a critical part of any software development process. It allows developers to identify and diagnose issues with their applications in production.

Spring Boot provides a number of built-in metrics for monitoring applications. In this post, we'll take a look at what Spring Boot metrics are and how to use them for monitoring your applications.

# What are Spring Boot Metrics?

Spring Boot metrics are a set of tools for monitoring Spring-based applications. They provide insight into the runtime behavior of applications and can be used to identify performance bottlenecks.

Spring Boot metrics are designed to be used with a variety of monitoring tools, such as Prometheus, Graphite, and StatsD.

# How to Use Spring Boot Metrics

Spring Boot provides a number of ways to configure and use metrics. In this section, we'll take a look at a few of the most important configuration options.

## Enabling Metrics

Metrics are disabled by default in Spring Boot. To enable metrics, you need to add the following property to your application's `application.properties` file:

```
spring.metrics.enable=true
```

## Configuring Metrics

Spring Boot allows you to configure a number of aspects of the metrics system. For example, you can configure the default registry, the metric name prefix, and the export format.

The following property can be used to configure the default registry:

```
spring.metrics.default-registry=my-registry
```

The following property can be used to configure the metric name prefix:

```
spring.metrics.prefix=my-prefix
```

The following property can be used to configure the export format:

```
spring.metrics.export.format=json
```

## Exporting Metrics

Spring Boot supports a number of ways to export metrics. The most common way is to use the `/metrics` endpoint. This endpoint exposes metrics in the Prometheus format by default.

You can also use the `/metrics/{name}` endpoint to export a single metric. For example, the following endpoint would export the `jvm.memory.used` metric:

```
/metrics/jvm.memory.used
```

# Conclusion

In this post, we've looked at Spring Boot metrics and how to use them for monitoring your applications. We've also seen how to enable and configure metrics, and how to export metrics for use with monitoring tools.