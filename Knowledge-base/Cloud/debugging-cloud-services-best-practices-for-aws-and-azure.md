---
title: 클라우드 서비스 디버깅: AWS 및 Azure 모범 사례
description: 
published: true
date: 2023-02-19T05:06:25.562Z
tags: 
editor: markdown
dateCreated: 2023-02-19T05:06:24.204Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Debugging Cloud Services: Best Practices for AWS and Azure***English** document is available*](/en/Knowledge-base/Cloud/debugging-cloud-services-best-practices-for-aws-and-azure)
{.links-list}


# 클라우드 서비스 디버깅: AWS 및 Azure 모범 사례

클라우드는 애플리케이션을 실행하기에 좋은 장소입니다. 그러나 문제가 발생하면 클라우드 기반 애플리케이션을 디버깅하기 어려울 수 있습니다. 이 문서에서는 AWS 및 Azure에서 클라우드 서비스를 디버깅하기 위한 몇 가지 모범 사례를 공유합니다.

## 로깅

클라우드 기반 애플리케이션을 디버깅할 때 수행할 수 있는 가장 중요한 작업 중 하나는 로깅을 활성화하는 것입니다. AWS와 Azure 모두 뛰어난 로깅 기능을 제공합니다.

### AWS 클라우드트레일

AWS CloudTrail은 AWS 계정에 대한 가시성을 제공하는 서비스입니다. 이를 통해 계정 활동 및 API 호출을 기록, 모니터링 및 유지할 수 있습니다. CloudTrail은 AWS Management Console, AWS SDK, 명령줄 도구 및 기타 AWS 서비스를 통해 수행된 작업을 포함하여 AWS 계정 활동의 이벤트 기록을 제공합니다. 이 이벤트 기록은 보안 분석, 리소스 변경 추적 및 규정 준수 감사를 간소화합니다.

AWS 계정에서 CloudTrail 로깅을 활성화하려면 [CloudTrail 콘솔](https://console.aws.amazon.com/cloudtrail/home)을 방문하십시오. **Create Trail** 버튼을 클릭하고 트레일 이름을 입력합니다. 그런 다음 **모든 이벤트** 확인란을 선택하고 **트레일 만들기**를 클릭합니다.

### Azure 활동 로그

Azure 활동 로그는 Azure 리소스에서 수행된 작업에 대한 정보를 제공합니다. "내 Azure 리소스는 어떻게 되었습니까?"라는 질문에 답하는 데 사용할 수 있습니다. Azure 활동 로그는 스토리지 계정에 기록되며 Log Analytics 서비스를 사용하여 활동 로그를 쿼리할 수 있습니다.

Azure 활동 로그를 활성화하려면 Azure Portal에서 [활동 로그](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) 블레이드를 방문하세요. **진단 로깅 켜기** 버튼을 클릭하고 **Log Analytics로 보내기** 옵션을 선택합니다.

## 모니터링

로깅 외에도 클라우드 기반 애플리케이션을 모니터링하는 것이 중요합니다. AWS와 Azure 모두 뛰어난 모니터링 기능을 제공합니다.

### AWS 클라우드워치

AWS CloudWatch는 AWS 리소스 및 애플리케이션에 대한 모니터링을 제공하는 서비스입니다. CloudWatch는 로그, 지표 및 이벤트의 형태로 모니터링 및 운영 데이터를 수집합니다. CloudWatch를 사용하여 경보를 설정하고 AWS 리소스의 변경 사항에 대응할 수 있습니다.

CloudWatch 경보를 생성하려면 [CloudWatch 콘솔](https://console.aws.amazon.com/cloudwatch/home)을 방문하십시오. **경보 생성** 버튼을 클릭하고 모니터링하려는 **지표**를 선택합니다. 그런 다음 **Statistic**, **Period** 및 **Unit**을 선택합니다. 마지막으로 **Threshold**를 입력하고 **Create Alarm**을 클릭합니다.

### 애저 모니터

Azure Monitor는 Azure 리소스 및 애플리케이션에 대한 모니터링을 제공하는 서비스입니다. Azure Monitor는 로그, 메트릭 및 이벤트 형식으로 모니터링 및 진단 데이터를 수집합니다. Azure Monitor를 사용하여 경고를 설정하고 Azure 리소스의 변경 사항에 응답할 수 있습니다.

Azure Monitor 경고를 생성하려면 Azure Portal에서 [Azure Monitor](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview) 블레이드를 방문하세요. **알림 규칙 추가** 버튼을 클릭하고 모니터링할 **측정항목**을 선택합니다. 그런 다음 **연산자**, **임계값** 및 **기간**을 선택합니다. 마지막으로 **알림 규칙 추가** 버튼을 클릭합니다.

## 결론

이 문서에서는 AWS 및 Azure에서 클라우드 서비스를 디버깅하기 위한 몇 가지 모범 사례를 공유했습니다. 로깅 및 모니터링은 모두 클라우드 기반 애플리케이션을 디버깅하는 데 도움이 되는 중요한 도구입니다.