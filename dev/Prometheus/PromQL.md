---
title: PromQL
description: 
published: true
date: 2023-02-17T18:00:35.663Z
tags: prometheus, promql
editor: markdown
dateCreated: 2022-12-26T11:04:42.161Z
---

- [PromQL***English** version of this document is available*](/en/dev/Prometheus/PromQL)
{.links-list}

![prometheus.png](/prometheus.png =500x){.align-center}

## 개요

PromQL(Prometheus Query Language)은 Prometheus 모니터링 시스템에서 데이터를 선택하고 집계하는 데 사용되는 쿼리 언어입니다. 필터링, 집계 및 수학 연산과 같은 메트릭 데이터에 대한 복잡한 쿼리를 수행할 수 있습니다.

PromQL의 기본 문법에 대한 간략한 요약입니다.

- `<metric_name>`: `request_latency_seconds` 또는 `cpu_utilization`과 같은 메트릭의 이름을 나타냅니다.
- `<label_name>`: `host` 또는 `instance_id`와 같은 메트릭과 연결된 레이블을 나타냅니다. 레이블은 메트릭을 식별하고 그룹화하는 데 사용할 수 있는 키-값 쌍입니다.
- `<function>(<vector>)`: `sum(request_latency_seconds)` 또는 `avg(request_latency_seconds)`와 같이 메트릭의 벡터에 적용되는 함수를 말합니다.
- `<vector>`: 메트릭 이름, 레이블 및 정규 표현식의 조합을 사용하여 선택되는 메트릭 집합을 나타냅니다. 예를 들어 `request_latency_seconds{env="production"}`은 이름이 `request_latency_seconds`이고 `env` 레이블이 `production`으로 설정된 모든 지표를 선택합니다.
- `<range vector>`: `[<start_time>:<end_time>]` 구문을 사용하여 지정된 시간 범위에 대한 메트릭 세트를 나타냅니다. 예를 들어 `request_latency_seconds[1h]`는 지난 1시간 동안 이름이 `request_latency_seconds`인 모든 지표를 선택합니다.
- `<offset modifier>`: `<vector> offset <duration>` 구문을 사용하여 지정된 범위 벡터에 적용되는 오프셋을 나타냅니다. 예를 들어 `request_latency_seconds[1h] offset 1h`는 지난 1시간 동안 이름이 `request_latency_seconds`인 모든 측정항목을 선택하지만 시간 범위는 미래로 1시간 이동되었습니다.

산술 연산, 그룹화 및 필터링과 같이 PromQL에서 사용할 수 있는 더 많은 기능과 기능이 있습니다. Prometheus 설명서에서 PromQL 구문 및 기능에 대한 자세한 설명를 찾을 수 있습니다.

- [QUERYING PROMETHEUS*prometheus.io*](https://prometheus.io/docs/prometheus/latest/querying/basics/)
{.links-list}

## 샘플

- `production` 환경의 모든 인스턴스에 대한 `request_latency_seconds` 합계

```
sum(request_latency_seconds{env="production"})
```

- `app=api` 레이블이 있는 모든 인스턴스에 대해 지난 1시간 동안의 평균 `cpu_utilization`

```
avg(cpu_utilization{app="api"}[1h])
```

- 24시간 전부터의 3시간 동안 최대 `memory_usage_bytes`

```
max(memory_usage_bytes[24h] offset 3h)
```

- `host` 레이블로 그룹화된 지난 5분 동안 `request_count` 메트릭의 변경 비율

```
rate(request_count[5m]) by (host)
```

### 더 복잡한 예제

```
sum(
  rate(
    request_latency_seconds{env="production",app="api"}[5m]
  )
  * on(app,instance) group_left request_count{env="production",app="api"}[5m]
) by (app)
```

이 쿼리는 지난 5분 동안 `production` 환경의 `api` 앱에 대한 총 요청 대기 시간(초)을 계산합니다. 먼저 `rate()` 함수를 사용하여 동일한 시간 범위에서 `request_latency_seconds` 지표의 변화율을 계산하여 이를 수행합니다. 그런 다음 이 비율에 `request_count` 측정항목을 곱하고 `on()` 및 `group_left` 함수를 사용하여 `app` 및 `instance` 레이블로 결과를 그룹화합니다. 마지막으로 `sum()` 함수를 사용하여 `app` 레이블로 결과 값을 합산합니다.

이것은 PromQL을 사용하여 작성할 수 있는 복잡한 쿼리 종류의 한 예일 뿐입니다. 이 언어는 강력하고 유연하며 메트릭 데이터에 대해 광범위한 작업을 수행할 수 있습니다.
