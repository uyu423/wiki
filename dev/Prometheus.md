---
title: Prometheus
description: 
published: true
date: 2022-12-26T09:40:30.504Z
tags: prometheus
editor: markdown
dateCreated: 2022-12-26T07:30:09.774Z
---

![prometheus.png](/prometheus.png =500x){.align-center}

## 개요

Prometheus는 최신 인프라스트럭쳐에서 널리 사용되는 인기 있는 오픈소스 시스템 모니터링 및 Alert Toolkit입니다. Prometheus의 주요 기능과 장점은 다음과 같습니다.

- **확장성** (Scalability): Prometheus는 확장 가능하고 효율적으로 설계되었으며 수백만 개의 메트릭과 초당 수십만 개의 샘플을 처리할 수 있습니다. 풀(Pull) 모델을 사용하는데, 이 모델에서 Prometheus 서버는 모니터링되는 시스템에서 노출된 Exporter의 메트릭을 주기적으로 스크랩하고 수집된 메트릭을 내부 시계열 데이터베이스에 저장합니다. 이를 통해 Prometeus는 모니터링되는 시스템을 압도하지 않고 대량의 메트릭 데이터를 수집하고 저장할 수 있습니다.

- **유연성** (Flexibility): Prometheus는 다양한 메트릭 유형 및 레이블을 지원하고 수집된 메트릭을 쿼리, 분석 및 시각화하기 위한 풍부한 쿼리 언어 및 API를 제공합니다. 이를 통해 사용자는 다양한 시스템과 소스를 모니터링하고 시스템의 성능과 동작을 매우 자세하게 이해할 수 있습니다.

- **통합** (Integration): Prometheus는 대시보드용 Grafana, 경고용 Alertmanager 또는 다양한 시스템 및 소스에서 메트릭을 수집하기 위한 다양한 Exporter 및 시스템과 통합할 수 있습니다. 이를 통해 사용자는 특정 요구 사항들을 충족하는 모니터링 인프라를 구축할 수 있습니다.

- **커뮤니티** (Community): Prometheus는 사용자에게 풍부한 리소스와 지원을 제공하는 크고 활동적인 커뮤니티가 있는 오픈 소스 프로젝트입니다. 여기에는 설명서, 자습서, 모범 사례 및 다양한 시스템과 소스를 모니터링하는 데 사용할 수 있는 다양한 Integration 및 Exporter가 포함됩니다.

Prometheus는 최신 인프라에 적합한 기능이 풍부하고 유연한 모니터링 도구입니다. 메트릭 데이터를 수집, 저장 및 쿼리하는 확장 가능하며 효율적인 방법을 제공하고 사용자가 시스템의 성능과 동작을 매우 자세하게 모니터링하고 이해할 수 있도록 합니다.

## 메트릭 수집

Prometheus가 측정항목을 수집하는 원리는 간단합니다. 풀(Pull) 모델을 사용합니다. 풀 모델에서는 Prometheus 서버가 주기적으로 HTTP 요청을 보내 모니터링되는 시스템에 의해 노출되는 "내보내기"라고 하는 다양한 엔드포인트에서 측정항목을 긁어냅니다. 내보내기는 Prometheus 서버에서 쉽게 구문 분석할 수 있는 텍스트 파일과 같은 특정 형식으로 메트릭 데이터를 제공하는 역할을 합니다.

> **풀(Pull) 모델에 대하여**
>
> Prometheus는 다양한 시스템 및 소스에서 메트릭을 수집하기 위해 풀 모델을 사용합니다. 풀 모델에서 Prometheus 서버는 "스크랩"이라고 불리는 HTTP 요청을 모니터링되는 시스템에 의해 노출되는 Exporter로 정기적으로 전송합니다. 내보내기 기능은 Prometheus 서버에서 쉽게 구문 분석할 수 있는 텍스트 파일과 같은 특정 형식으로 메트릭 데이터를 제공하는 역할을 합니다.
>
> - 풀 모델은 모니터링되는 시스템이 메트릭 데이터를 Prometheus 서버로 직접 보내는 푸시 모델에 비해 몇 가지 장점이 있습니다. 예를 들어:
>
> - 풀 모델을 사용하면 Prometheus 서버가 메트릭을 수집하는 속도를 제어하고 서버의 워크로드 및 리소스에 따라 속도를 조정할 수 있습니다. 이렇게 하면 대량의 메트릭 데이터로 인해 서버가 과부하되는 것을 방지할 수 있습니다.
>
> - 풀 모델은 모니터링되는 시스템에서 Prometheus 서버를 분리하고 서버가 내보내기를 노출하는 모든 시스템에서 메트릭을 수집할 수 있도록 합니다. 이는 새로운 시스템과 소스를 지원하도록 쉽게 확장할 수 있으므로 모니터링 인프라를 보다 유연하고 확장 가능하게 만듭니다.
>
> - 풀 모델을 사용하면 Prometheus 서버가 메트릭 데이터를 캐시하고 내부 시계열 데이터베이스에 저장하기 전에 데이터에 대한 변환을 수행할 수 있습니다. 이렇게 하면 서버의 저장 및 처리 요구 사항이 줄어들고 사용자가 메트릭 데이터를 보다 효율적으로 저장하고 쿼리할 수 있습니다.
>
> 풀 모델은 Prometheus 모니터링 시스템의 중요한 측면이며 이를 통해 서버는 확장 가능하고 효율적인 방식으로 다양한 시스템 및 소스에서 메트릭 데이터를 수집하고 저장할 수 있습니다.

Prometheus 서버는 수집된 메트릭을 내부 시계열 데이터베이스에 저장하고 데이터 쿼리, 분석 및 시각화를 위한 풍부한 쿼리 언어 및 API를 제공합니다. 또한 수집된 메트릭 및 사용자 정의 규칙을 기반으로 알림을 트리거하거나 자동화된 작업을 수행할 수 있는 경고 엔진이 포함되어 있습니다.

Prometheus 수집 메트릭의 원리에 대한 자세한 설명은 다음과 같습니다.

1. Prometheus 서버는 다양한 시스템 및 소스에서 메트릭을 수집하는 역할을 합니다. 모니터링되는 시스템에서 노출된 Exporter에 "스크랩"이라고 하는 HTTP 요청을 주기적으로 전송하여 이를 수행합니다. 이러한 내보내기는 Prometheus 서버에서 쉽게 구문 분석할 수 있는 텍스트 파일과 같은 특정 형식으로 메트릭 데이터를 제공하는 역할을 합니다.

1. 내보내기는 독립 실행형 프로세스로 구현하거나 모니터링되는 시스템에 내장할 수 있는 라이브러리로 구현할 수 있습니다. 이들은 일반적으로 메트릭의 다른 인스턴스 또는 차원을 구별하는 데 사용할 수 있는 선택적 레이블과 함께 메트릭 이름 및 해당 값 세트로 구성된 Prometheus 형식으로 메트릭 데이터를 제공하는 HTTP 끝점을 노출합니다.

1. Prometheus 서버는 대량의 시계열 데이터를 저장하고 쿼리하는 데 최적화된 내부 시계열 데이터베이스에 수집된 메트릭을 저장합니다. 데이터베이스는 각각 고정된 시간 간격을 나타내는 일련의 블록으로 구성되며 각 블록에는 메트릭 이름 및 레이블의 매트릭스로 저장되는 시계열 데이터 요소 집합이 포함됩니다.

1. Prometheus 서버는 수집된 메트릭을 쿼리, 분석 및 시각화하기 위한 풍부한 쿼리 언어 및 API를 제공합니다. PromQL이라는 쿼리 언어를 사용하면 메트릭 데이터를 다양한 방식으로 필터링, 집계 및 변환하는 복잡한 쿼리를 지정할 수 있습니다. API를 통해 사용자는 원시 데이터 포인트 검색, 데이터를 외부 시스템으로 내보내기 또는 경고 생성 및 관리와 같이 수집된 메트릭에 대해 다양한 작업을 수행할 수 있습니다.

1. Prometheus 서버에는 수집된 지표 및 사용자 정의 규칙을 기반으로 알림을 트리거하거나 자동화된 작업을 수행할 수 있는 경고 엔진도 포함되어 있습니다. 사용자는 수집된 메트릭 값과 해당 임계값을 기반으로 경고가 트리거되어야 하는 시기를 지정하는 규칙을 정의할 수 있습니다. 경고 엔진은 수집된 메트릭에 대해 규칙을 지속적으로 평가하고 규칙이 충족되면 알림을 보내거나 작업을 수행합니다.

전반적으로 Prometheus 수집 메트릭의 원칙은 다양한 시스템과 소스를 모니터링할 수 있는 유연하고 확장 가능한 방법을 제공하고 사용자가 수집된 데이터를 쉽게 쿼리, 분석 및 시각화할 수 있도록 하는 것입니다. 이를 통해 사용자는 시스템의 성능과 동작을 이해하고 문제가 심각해지기 전에 식별하고 해결할 수 있습니다.

## Collecting metrics

The principle behind Prometheus collecting metrics is simple: it uses a pull model, in which the Prometheus server periodically sends HTTP requests to scrape metrics from various endpoints, called "exporters", that are exposed by the monitored systems. The exporters are responsible for providing the metrics data in a specific format, such as a text file, that can be easily parsed by the Prometheus server.

> **About "Pull Model"**
> 
> Prometheus uses a pull model for collecting metrics from various systems and sources. In a pull model, the Prometheus server periodically sends HTTP requests, called "scrapes", to exporters that are exposed by the monitored systems. The exporters are responsible for providing the metrics data in a specific format, such as a text file, that can be easily parsed by the Prometheus server.
> 
> - The pull model has several advantages over a push model, in which the monitored systems send the metrics data directly to the Prometheus server. For example:
> 
> - The pull model allows the Prometheus server to control the rate at which it collects metrics, and to adjust the rate based on the workload and resources of the server. This can help prevent the server from being overwhelmed by a large volume of metrics data.
> 
> - The pull model decouples the Prometheus server from the monitored systems, and allows the server to collect metrics from any system that exposes an exporter. This makes the monitoring infrastructure more flexible and scalable, as it can be easily extended to support new systems and sources.
> 
> - The pull model allows the Prometheus server to cache the metrics data and to perform transformations on the data before storing it in its internal time-series database. This can reduce the storage and processing requirements of the server, and allow users to store and query the metrics data more efficiently.
> 
> The pull model is an important aspect of the Prometheus monitoring system, and it enables the server to collect and store metrics data from various systems and sources in a scalable and efficient way.


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