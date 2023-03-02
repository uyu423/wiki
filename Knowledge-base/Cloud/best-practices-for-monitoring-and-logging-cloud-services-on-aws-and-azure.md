---
title: AWS 및 Azure에서 클라우드 서비스 모니터링 및 로깅 모범 사례
description: 
published: true
date: 2023-03-02T08:20:49.960Z
tags: 
editor: markdown
dateCreated: 2023-03-02T08:20:49.960Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Best Practices for Monitoring and Logging Cloud Services on AWS and Azure***English** document is available*](/en/Knowledge-base/Cloud/best-practices-for-monitoring-and-logging-cloud-services-on-aws-and-azure)
{.links-list}
# AWS 및 Azure에서 클라우드 서비스 모니터링 및 로깅 모범 사례

클라우드 채택이 계속 증가함에 따라 AWS 및 Azure와 같은 플랫폼에서 클라우드 서비스를 모니터링 및 로깅하는 것은 최적의 성능을 보장하고 문제를 식별 및 해결하며 보안을 유지하는 데 중요한 구성 요소가 되었습니다. 이러한 플랫폼의 방대함과 복잡성은 효과적으로 모니터링하고 관리하기 어려울 수 있습니다. 하지만 적절한 도구와 모범 사례를 사용하면 클라우드 환경의 안정성, 가동 시간 및 보안을 보장할 수 있습니다. 이 문서에서는 AWS 및 Azure에서 클라우드 서비스를 모니터링하고 기록하는 모범 사례에 대한 포괄적인 가이드를 제공합니다.

## 클라우드 기반 모니터링 및 로깅 서비스 사용

AWS 및 Azure용으로 설계된 클라우드 네이티브 모니터링 및 로깅 서비스는 클라우드 환경을 더 잘 모니터링하는 데 도움이 되는 다양한 기능을 제공합니다. AWS는 AWS 리소스 및 애플리케이션의 실시간 모니터링을 제공하는 모니터링 및 관찰 서비스인 Amazon CloudWatch를 제공합니다. CloudWatch를 사용하면 리소스 사용률, 애플리케이션 성능 및 운영 상태를 모니터링할 수 있습니다. Azure는 전체 스택 모니터링과 Azure 리소스 및 애플리케이션의 성능 및 상태에 대한 통합 가시성을 제공하는 Azure Monitor를 제공합니다. CloudWatch와 Azure Monitor 모두 문제를 사전에 식별하고 해결하는 데 도움이 되는 기본 제공 경보, 알림 및 대시보드를 제공합니다.

## 모니터링 및 로깅 표준 정의

클라우드 서비스에 대한 모니터링 및 로깅 표준을 정의하면 일관성을 유지하는 데 도움이 되며 조직의 모든 이해 관계자가 모니터링 및 로깅할 항목을 이해할 수 있습니다. 메트릭과 로그를 표준화하면 문제를 쉽게 식별하고 해결할 수 있으며 클라우드 환경 성능에 대한 높은 수준의 보기를 제공합니다. 모니터링 및 로깅 표준을 정의할 때 다음을 고려하십시오.

- 모니터링할 메트릭 및 로그 정의: 클라우드 환경의 성능 및 보안에 중요한 메트릭 및 로그를 결정합니다. 메트릭의 예로는 CPU 사용률, 네트워크 처리량 및 메모리 사용량이 있습니다. 로그에는 애플리케이션 로그, 시스템 로그 및 보안 로그가 포함될 수 있습니다.
- 임계값 및 경보 설정: 각 메트릭 및 로그에 대한 임계값을 정의하고 임계값을 초과할 때 트리거되도록 경보를 설정합니다. 잠재적인 문제에 신속하게 대응하려면 사전에 경보를 설정해야 합니다.
- 기록 간격 설정: 로그를 수집하고 저장할 빈도를 설정합니다. 이는 비용을 관리하고 클라우드 환경의 성능을 유지하는 데 중요합니다.

## 자동화된 모니터링 및 로깅 구현

모니터링 및 로깅 작업을 자동화하면 프로세스를 간소화하고 수동 개입을 줄일 수 있습니다. AWS와 Azure 모두 모니터링 및 로깅 작업을 자동화하는 데 도움이 되는 자동화 도구를 제공합니다. 예를 들어 AWS CloudFormation을 사용하면 CloudWatch 경보 및 로깅 구성을 포함하여 인프라를 코드로 정의할 수 있습니다. 마찬가지로 Azure Resource Manager를 사용하면 경고 규칙, 메트릭 수집 및 로그 수집을 비롯한 Azure Monitor 설정을 자동화할 수 있습니다.

## 보안 및 규정 준수 보장

모니터링 및 로깅 클라우드 서비스는 보안 위험을 식별 및 완화하고 규정 요구 사항을 준수하는 데 도움이 될 수 있습니다. AWS와 Azure는 둘 다 안전하고 규정을 준수하는 클라우드 환경을 달성하는 데 도움이 되는 보안 및 규정 준수 서비스를 제공합니다. AWS는 클라우드 환경에 대한 위협 탐지 및 지속적인 모니터링을 제공하는 Amazon GuardDuty를 제공합니다. Azure는 통합 보안 관리 및 고급 위협 방지 기능을 제공하는 Azure Security Center를 제공합니다.

## 모니터링 및 로깅 데이터 중앙 집중화

여러 클라우드 서비스 또는 여러 클라우드 공급자와 작업할 때 모니터링 및 로깅 데이터를 중앙 집중화하는 것이 필수적입니다. 데이터를 중앙 집중화하면 클라우드 환경의 성능에 대한 단일 통합 보기를 제공하고 모든 문제를 쉽게 식별할 수 있습니다. AWS와 Azure는 모두 중앙 집중식 로깅 및 모니터링 서비스를 제공합니다. AWS CloudTrail은 여러 AWS 서비스에서 API 호출에 대한 단일 정보 소스를 제공합니다. Azure Log Analytics는 여러 Azure 리소스 및 서비스의 로그를 저장하고 분석하기 위한 중앙 위치를 제공합니다.

## 결론

AWS 및 Azure에서 클라우드 서비스를 모니터링하고 로깅하는 것은 클라우드 환경을 관리하고 보호하는 데 필수적인 구성 요소입니다. 이 문서에 설명된 모범 사례를 따르면 최적의 성능을 보장하고 문제를 사전에 식별 및 해결하며 클라우드 환경의 보안 및 규정 준수를 유지할 수 있습니다. 클라우드 네이티브 모니터링 및 로깅 서비스를 활용하고, 모니터링 및 로깅 표준을 정의하고, 모니터링 및 로깅 작업을 자동화하고, 보안 및 규정 준수를 보장하고, 모니터링 및 로깅 데이터를 중앙 집중화하면 가용성이 높고 안전하며 성능이 우수한 클라우드 환경을 구현할 수 있습니다.

## 외부 리소스

- [AWS CloudWatch](https://aws.amazon.com/cloudwatch/)
- [Azure 모니터](https://azure.microsoft.com/en-us/services/monitor/)
- [AWS CloudFormation](https://aws.amazon.com/cloudformation/)
- [Azure 리소스 관리자](https://azure.microsoft.com/en-us/features/resource-manager/)
- [Amazon GuardDuty](https://aws.amazon.com/guardduty/)
- [Azure 보안 센터](https://azure.microsoft.com/en-us/services/security-center/)
- [AWS CloudTrail](https://aws.amazon.com/cloudtrail/)
- [Azure Log Analytics](https://azure.microsoft.com/en-us/services/log-analytics/)