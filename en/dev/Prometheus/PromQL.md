---
title: PromQL
description: 
published: true
date: 2023-02-17T18:00:34.086Z
tags: prometheus, promql, english
editor: markdown
dateCreated: 2022-12-26T10:55:45.428Z
---

- [PromQL***Korean** version of this document is available*](/ko/dev/Prometheus/PromQL)
{.links-list}

![prometheus.png](/prometheus.png =500x){.align-center}

## Overview

PromQL (Prometheus Query Language) is a query language used to select and aggregate data in the Prometheus monitoring system. It allows you to perform complex queries on your metrics data, such as filtering, aggregation, and math operations.

Here is a brief overview of the basic syntax of PromQL:

- `<metric_name>`: This refers to the name of a metric, such as `request_latency_seconds` or `cpu_utilization`.
- `<label_name>`: This refers to a label associated with a metric, such as `host` or `instance_id`. Labels are key-value pairs that can be used to identify and group metrics.
- `<function>(<vector>)`: This refers to a function applied to a vector of metrics, such as `sum(request_latency_seconds)` or `avg(request_latency_seconds)`.
- `<vector>`: This refers to a set of metrics, often selected using a combination of metric names, labels, and regular expressions. For example, `request_latency_seconds{env="production"}` selects all metrics with the name `request_latency_seconds` and the label `env` set to `production`.
- `<range vector>`: This refers to a set of metrics over a range of time, specified using the `[<start_time>:<end_time>]` syntax. For example, `request_latency_seconds[1h]` selects all metrics with the name `request_latency_seconds` for the past hour.
- `<offset modifier>`: This refers to an offset applied to a range vector, specified using the `<vector> offset <duration>` syntax. For example, `request_latency_seconds[1h] offset 1h` selects all metrics with the name `request_latency_seconds` for the past hour, but with the time range shifted one hour into the future.

There are many more features and functions available in PromQL, such as arithmetic operations, grouping, and filtering. You can find more detailed documentation on the PromQL syntax and features in the Prometheus documentation.

- [QUERYING PROMETHEUS*prometheus.io*](https://prometheus.io/docs/prometheus/latest/querying/basics/)
{.links-list}

## Samples

- Sum the `request_latency_seconds` metric for all instances in the `production` environment:

```
sum(request_latency_seconds{env="production"})
```

- Calculate the average `cpu_utilization` over the past hour for all instances with the `app=api` label:

```
avg(cpu_utilization{app="api"}[1h])
```

- Select the maximum `memory_usage_bytes` over the past 24 hours, shifted 3 hours into the future:

```
max(memory_usage_bytes[24h] offset 3h)
```

- Select the rate of change of the `request_count` metric over the past 5 minutes, grouped by the `host` label:

```
rate(request_count[5m]) by (host)
```

### More Complex Example

```
sum(
  rate(
    request_latency_seconds{env="production",app="api"}[5m]
  )
  * on(app,instance) group_left request_count{env="production",app="api"}[5m]
) by (app)
```

This query calculates the total request latency (in seconds) for the `api` app in the `production` environment, over the past 5 minutes. It does this by first calculating the rate of change of the `request_latency_seconds` metric over the same time range, using the `rate()` function. It then multiplies this rate by the `request_count` metric, grouping the results by the `app` and `instance` labels using the `on()` and `group_left` functions. Finally, it sums the resulting values by the `app` label using the `sum()` function.

This is just one example of the kinds of complex queries you can write using PromQL. The language is powerful and flexible, and allows you to perform a wide range of operations on your metrics data.