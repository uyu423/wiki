---
title: Monitoring and Logging in Kubernetes Clusters
description: 
published: true
date: 2023-02-08T19:32:24.194Z
tags: 
editor: markdown
dateCreated: 2023-02-08T19:32:22.532Z
---

- [Supervisión y registro en clústeres de Kubernetes***Spanish** document is available*](/es/Knowledge-base/Kubernetes/monitoring-and-logging-in-kubernetes-clusters)
{.links-list}
- [Kubernetes 集群中的监控和日志记录***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/monitoring-and-logging-in-kubernetes-clusters)
{.links-list}
- [Kubernetes 클러스터의 모니터링 및 로깅***Korean** document is available*](/ko/Knowledge-base/Kubernetes/monitoring-and-logging-in-kubernetes-clusters)
{.links-list}


# Monitoring and Logging in Kubernetes Clusters

In this article, we'll explore how to monitor and log activity in Kubernetes clusters. We'll start with an overview of the types of data that are typically collected for monitoring and logging, and then we'll dive into some specific tools and techniques that can be used to collect this data.

## Types of Data Collected for Monitoring and Logging

There are two main types of data that are collected for monitoring and logging: system data and application data.

System data includes information about the nodes in the Kubernetes cluster, such as CPU and memory usage, network traffic, and disk activity. This data is typically collected using a tool like Prometheus.

Application data includes information about the applications running in the Kubernetes cluster, such as request and response times, error rates, and slowest requests. This data is typically collected using a tool like Fluentd.

## Collecting System Data

Prometheus is a popular open-source tool for collecting system data. Prometheus can be used to collect data from any type of system, but it has especially good support for Kubernetes.

Prometheus collects data by scraping metrics from HTTP endpoints. By default, Kubernetes exposes a number of metrics in the Prometheus format on the `/metrics` endpoint. These metrics can be scraped by Prometheus to provide valuable insights into the health and performance of the Kubernetes cluster.

In addition to the built-in metrics, Kubernetes also exposes a `/logs` endpoint that can be scraped by Prometheus to collect log data. This data can be used to generate alerts or to visualize the health of the applications running in the cluster.

## Collecting Application Data

Fluentd is a popular open-source tool for collecting application data. Fluentd can be used to collect data from any type of application, but it has especially good support for Kubernetes.

Fluentd collects data by parsing log files. By default, Kubernetes writes all log data to files in the `/var/log/containers` directory. Fluentd can be configured to watch this directory and parse the log data to extract useful information like request and response times, error rates, and slowest requests.

This data can then be stored in a database for further analysis or used to generate alerts. Fluentd also supports a wide variety of output formats, so the data can be easily integrated with other tools and systems.

## Conclusion

In this article, we've explored how to collect system and application data for monitoring and logging in Kubernetes. We've seen how Prometheus can be used to collect system data, and how Fluentd can be used to collect application data.

Both of these tools are highly configurable and support a wide variety of input and output formats. This makes them easy to integrate with other tools and systems.

## References

1. Prometheus: https://prometheus.io/
2. Fluentd: https://www.fluentd.org/
3. Kubernetes Monitoring: https://kubernetes.io/docs/concepts/cluster-administration/monitoring/