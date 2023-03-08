---
title: Kubernetes 클러스터의 모니터링 및 로깅
description: 
published: true
date: 2023-02-08T19:32:28.322Z
tags: 
editor: markdown
dateCreated: 2023-02-08T19:32:22.528Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Monitoring and Logging in Kubernetes Clusters***English** document is available*](/en/Knowledge-base/Kubernetes/monitoring-and-logging-in-kubernetes-clusters)
{.links-list}


# Kubernetes 클러스터에서 모니터링 및 로깅

이 기사에서는 Kubernetes 클러스터에서 활동을 모니터링하고 기록하는 방법을 살펴봅니다. 모니터링 및 로깅을 위해 일반적으로 수집되는 데이터 유형에 대한 개요부터 시작한 다음 이 데이터를 수집하는 데 사용할 수 있는 몇 가지 특정 도구 및 기술에 대해 자세히 살펴보겠습니다.

## 모니터링 및 로깅을 위해 수집되는 데이터 유형

모니터링 및 로깅을 위해 수집되는 데이터에는 시스템 데이터와 애플리케이션 데이터의 두 가지 주요 유형이 있습니다.

시스템 데이터에는 CPU 및 메모리 사용량, 네트워크 트래픽 및 디스크 활동과 같은 Kubernetes 클러스터의 노드에 대한 정보가 포함됩니다. 이 데이터는 일반적으로 Prometheus와 같은 도구를 사용하여 수집됩니다.

애플리케이션 데이터에는 요청 및 응답 시간, 오류율, 가장 느린 요청과 같은 Kubernetes 클러스터에서 실행 중인 애플리케이션에 대한 정보가 포함됩니다. 이 데이터는 일반적으로 Fluentd와 같은 도구를 사용하여 수집됩니다.

## 시스템 데이터 수집

Prometheus는 시스템 데이터 수집을 위한 인기 있는 오픈 소스 도구입니다. Prometheus는 모든 유형의 시스템에서 데이터를 수집하는 데 사용할 수 있지만 특히 Kubernetes를 잘 지원합니다.

Prometheus는 HTTP 엔드포인트에서 메트릭을 스크랩하여 데이터를 수집합니다. 기본적으로 Kubernetes는 `/metrics` 엔드포인트에서 Prometheus 형식으로 여러 메트릭을 노출합니다. 이러한 메트릭은 Prometheus에서 스크랩하여 Kubernetes 클러스터의 상태 및 성능에 대한 귀중한 통찰력을 제공할 수 있습니다.

기본 제공 메트릭 외에도 Kubernetes는 로그 데이터를 수집하기 위해 Prometheus에서 스크랩할 수 있는 `/logs` 엔드포인트도 노출합니다. 이 데이터는 경고를 생성하거나 클러스터에서 실행 중인 애플리케이션의 상태를 시각화하는 데 사용할 수 있습니다.

## 애플리케이션 데이터 수집

Fluentd는 애플리케이션 데이터 수집을 위한 인기 있는 오픈 소스 도구입니다. Fluentd는 모든 유형의 애플리케이션에서 데이터를 수집하는 데 사용할 수 있지만 특히 Kubernetes를 잘 지원합니다.

Fluentd는 로그 파일을 구문 분석하여 데이터를 수집합니다. 기본적으로 Kubernetes는 `/var/log/containers` 디렉터리의 파일에 모든 로그 데이터를 기록합니다. Fluentd는 이 디렉터리를 감시하고 로그 데이터를 구문 분석하여 요청 및 응답 시간, 오류율, 가장 느린 요청과 같은 유용한 정보를 추출하도록 구성할 수 있습니다.

그런 다음 이 데이터를 추가 분석을 위해 데이터베이스에 저장하거나 경고를 생성하는 데 사용할 수 있습니다. Fluentd는 또한 다양한 출력 형식을 지원하므로 데이터를 다른 도구 및 시스템과 쉽게 통합할 수 있습니다.

## 결론

이 기사에서는 Kubernetes에서 모니터링 및 로그인을 위해 시스템 및 애플리케이션 데이터를 수집하는 방법을 살펴보았습니다. Prometheus를 사용하여 시스템 데이터를 수집하는 방법과 Fluentd를 사용하여 애플리케이션 데이터를 수집하는 방법을 살펴보았습니다.

이 두 도구는 모두 구성이 가능하며 다양한 입력 및 출력 형식을 지원합니다. 따라서 다른 도구 및 시스템과 쉽게 통합할 수 있습니다.

## 참조

1. 프로메테우스: https://prometheus.io/
2. Fluentd: https://www.fluentd.org/
3. 쿠버네티스 모니터링: https://kubernetes.io/docs/concepts/cluster-administration/monitoring/