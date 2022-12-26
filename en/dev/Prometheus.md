---
title: Prometheus
description: 
published: true
date: 2022-12-26T07:46:07.887Z
tags: 
editor: markdown
dateCreated: 2022-12-26T07:46:07.887Z
---

![prometheus.png](/prometheus.png =500x){.align-center}

Prometheus is an open-source systems monitoring and alerting toolkit. One of the key features of Prometheus is its ability to collect metrics from various systems and sources.

## Collecting metrics

The principle behind Prometheus collecting metrics is simple: it uses a pull model, in which the Prometheus server periodically sends HTTP requests to scrape metrics from various endpoints, called "exporters", that are exposed by the monitored systems. The exporters are responsible for providing the metrics data in a specific format, such as a text file, that can be easily parsed by the Prometheus server.

The Prometheus server stores the collected metrics in its internal time-series database, and provides a rich query language and API for querying, analyzing, and visualizing the data. It also includes a alerting engine that can trigger notifications or take automated actions based on the collected metrics and user-defined rules.

Here is a more detailed explanation of the principle of Prometheus collecting metrics:

1. The Prometheus server is responsible for collecting metrics from various systems and sources. It does this by periodically sending HTTP requests, called "scrapes", to exporters that are exposed by the monitored systems. These exporters are responsible for providing the metrics data in a specific format, such as a text file, that can be easily parsed by the Prometheus server.

1. The exporters can be implemented as standalone processes, or as libraries that can be embedded in the monitored systems. They typically expose a HTTP endpoint that serves the metrics data in the Prometheus format, which consists of a set of metric names and corresponding values, along with optional labels that can be used to distinguish different instances or dimensions of the metrics.

1. The Prometheus server stores the collected metrics in its internal time-series database, which is optimized for storing and querying large amounts of time-series data. The database is organized as a set of blocks, each representing a fixed time interval, and each block contains a set of time-series data points that are stored as a matrix of metric names and labels.

1. The Prometheus server provides a rich query language and API for querying, analyzing, and visualizing the collected metrics. The query language, called PromQL, allows users to specify complex queries that filter, aggregate, and transform the metrics data in various ways. The API allows users to perform various operations on the collected metrics, such as retrieving the raw data points, exporting the data to external systems, or creating and managing alerts.

1. The Prometheus server also includes a alerting engine that can trigger notifications or take automated actions based on the collected metrics and user-defined rules. Users can define rules that specify when an alert should be triggered, based on the values of the collected metrics and their thresholds. The alerting engine continuously evaluates the rules against the collected metrics, and sends notifications or performs actions when the rules are met.

Overall, the principle of Prometheus collecting metrics is to provide a flexible and scalable way to monitor various systems and sources, and to enable users to easily query, analyze, and visualize the collected data. It allows users to understand the performance and behavior of their systems, and to identify and resolve issues before they become critical.

## Sample of collecting metrics

1. First, you need to install and configure the Prometheus server, and decide which systems and sources you want to monitor. This can involve setting up exporters on the monitored systems, or using existing exporters that are compatible with Prometheus.

1. Next, you need to specify the targets (i.e., the exporters) that the Prometheus server should scrape for metrics. This is typically done in the Prometheus configuration file, where you can specify the exporter URLs, the scraping intervals, and other options such as authentication or TLS settings.

1. The Prometheus server will then start scraping the specified targets at the configured intervals, and collect the metrics data in its internal time-series database. The collected metrics can be queried and analyzed using the Prometheus query language and API, or visualized using a dashboard tool such as Grafana.

Here is an example of a Prometheus configuration file that specifies two targets to scrape for metrics:

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: my_system
    static_configs:
      - targets: ['localhost:9090', 'localhost:9191']
```

This configuration specifies that the Prometheus server should scrape the targets localhost:9090 and localhost:9191 every 15 seconds, and store the collected metrics in the time-series database. The targets can be exporters that are running on the local machine, or they can be remote exporters that are accessible over the network.

## Sample of metrics data

The syntax of the metrics in the sample code you provided is based on the Prometheus text format, which is a human-readable format that is used to expose metrics data over HTTP. The text format consists of lines of text that represent metric names and corresponding values, along with optional labels that can be used to distinguish different instances or dimensions of the metrics.

- `# HELP` and `# TYPE`: These lines define the metric name and type, and provide a description of the metric. The metric name and type are followed by a space and the metric value. The metric type can be one of four types: `counter`, `gauge`, `histogram`, or `summary`.

- `{label_name="label_value"}`: These lines define the labels of the metric, which are key-value pairs that can be used to distinguish different instances or dimensions of the metric. Labels are enclosed in curly braces, and each label consists of a label name and a label value, separated by an equals sign.

- `_bucket, _sum, _count`: These suffixes are used to define additional fields of a histogram or a summary metric. A histogram includes `_bucket` fields that define the buckets of the histogram, and a `_sum` and `_count` field that represent the sum and count of the metric values. A summary includes `_sum` and `_count` fields, but does not include `_bucket` fields.

```
# HELP http_request_duration_seconds The HTTP request latencies in seconds
# TYPE http_request_duration_seconds histogram
http_request_duration_seconds_bucket{le="0.1", method="GET", status_code="200"} 24054
http_request_duration_seconds_bucket{le="0.2", method="GET", status_code="200"} 33444
http_request_duration_seconds_sum{method="GET", status_code="200"} 53423
http_request_duration_seconds_count{method="GET", status_code="200"} 133988
```

In this example, the metric is a histogram of HTTP request latencies, and it is labeled with the `method` and `status_code` labels. The metric includes `_bucket` fields that define the buckets of the histogram, and a `_sum` and `_count` field that represent the sum and count of the metric values.


> ### Appendix: Infrastructure
> 
> The structure of a Prometheus-based infrastructure typically consists of the following components:
> 
> - **Prometheus server**: The central component of the infrastructure, responsible for collecting metrics from various systems and sources, storing the collected metrics in its internal time-series database, and providing a query language and API for querying, analyzing, and visualizing the data.
> 
> - **Exporters**: Standalone processes or libraries that expose metrics data in the Prometheus format, and that can be scraped by the Prometheus server. Exporters can be implemented for various systems and sources, such as databases, networks, applications, or hardware devices.
> 
> - **Alertmanager**: An optional component that can be used in conjunction with the Prometheus server to trigger notifications or take automated actions based on the collected metrics and user-defined rules. The Alertmanager receives alerts from the Prometheus server, groups them, and sends notifications or performs actions based on the configured policies.
> 
> - **Grafana**: A popular dashboard tool that can be used to visualize the collected metrics and create interactive dashboards. Grafana can be integrated with the Prometheus server or Alertmanager, and can display the metrics data in various charts and graphs.
> 
> - **Monitored systems and sources**: The systems and sources that are being monitored by the Prometheus server, and that expose metrics data through exporters. These can be servers, applications, databases, networks, or other types of systems and sources.
> 
> The structure of a Prometheus-based infrastructure is centered around the Prometheus server, which collects metrics from various systems and sources, and provides a rich query language and API for querying, analyzing, and visualizing the data. The infrastructure can also include additional components such as exporters, Alertmanager, and Grafana, which can be used to extend the functionality and capabilities of the monitoring system.