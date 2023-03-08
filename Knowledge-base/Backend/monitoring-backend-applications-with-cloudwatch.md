---
title: CloudWatch로 백엔드 애플리케이션 모니터링
description: 
published: true
date: 2023-02-10T01:55:35.400Z
tags: 
editor: markdown
dateCreated: 2023-02-10T01:55:33.774Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Monitoring Backend Applications with CloudWatch***English** document is available*](/en/Knowledge-base/Backend/monitoring-backend-applications-with-cloudwatch)
{.links-list}


# CloudWatch로 백엔드 애플리케이션 모니터링

CloudWatch는 AWS 클라우드 리소스 및 AWS에서 실행되는 애플리케이션에 대한 모니터링 서비스입니다. CloudWatch는 애플리케이션의 문제를 해결하고 최적화하는 데 사용할 수 있는 로그, 지표 및 이벤트의 형태로 모니터링 및 운영 데이터를 수집합니다.

이 기사에서는 CloudWatch를 사용하여 백엔드 애플리케이션을 모니터링하는 방법에 중점을 둘 것입니다. 다음 주제를 다룰 것입니다.

- 클라우드워치란?
- CloudWatch 설정
- CloudWatch 경보 생성
- CloudWatch 로그 보기

## 클라우드워치란?

앞서 언급했듯이 CloudWatch는 AWS 클라우드 리소스 및 AWS에서 실행되는 애플리케이션에 대한 모니터링 서비스입니다. CloudWatch를 사용하면 지표를 수집 및 추적하고, 경보를 설정하고, AWS 리소스의 변경 사항에 자동으로 대응할 수 있습니다.

CloudWatch는 애플리케이션을 모니터링하고, 시스템 전체의 성능 변화에 대응하고, 리소스 활용을 최적화하고, 운영 상태에 대한 통합 보기를 얻을 수 있는 데이터 및 실행 가능한 통찰력을 제공합니다.

## CloudWatch 설정

CloudWatch를 사용하려면 먼저 AWS 계정을 설정하고 Amazon CloudWatch Logs 그룹을 생성해야 합니다.

1. AWS 계정을 설정하려면 [https://aws.amazon.com/](https://aws.amazon.com/)으로 이동하고 **Create an AWS Account**를 클릭합니다.

2. 지침에 따라 계정을 만드십시오.

3. 계정을 생성했으면 [https://console.aws.amazon.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)에서 Amazon CloudWatch 콘솔로 이동합니다.

4. 왼쪽 탐색 패널에서 **로그**를 클릭합니다.

5. **로그 그룹 생성**을 클릭합니다.

6. 로그 그룹의 이름을 입력하고 **로그 그룹 생성**을 클릭합니다.

## CloudWatch 경보 생성

경보는 지정한 기간 동안 지표를 감시하고 설정한 임계값에 상대적인 지표 값에 따라 하나 이상의 작업을 수행합니다. 작업은 Amazon SNS 알림 전송에서 AWS Lambda 함수 호출에 이르기까지 무엇이든 될 수 있습니다.

이 섹션에서는 Amazon EC2 인스턴스의 평균 CPU 사용률이 50%를 초과할 때 Amazon SNS 알림을 보내는 경보를 생성합니다.

1. [https://console.aws.amazon.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)에서 Amazon CloudWatch 콘솔로 이동합니다.

2. 왼쪽 탐색 패널에서 **알람**을 클릭합니다.

3. **알람 생성**을 클릭합니다.

4. **CPUUtilization** 지표를 선택하고 **다음**을 클릭합니다.

5. 다음과 같이 알람을 구성합니다.

- **통계**의 경우 **평균**을 선택합니다.
- **기간**에 **60**을 입력합니다.
- **단위**에서 **초**를 선택합니다.
- **임계값**에 **50**을 입력합니다.
- **평가 기간**은 **2**로 입력합니다.
- **누락된 데이터 처리**에서 **누락된 데이터를 위반으로**를 선택합니다.
- **작업**의 경우 **알림 보내기** 작업을 선택합니다.
- **알림 보내기**에서 알림을 받을 Amazon SNS 주제를 선택합니다.

6. **알람 생성**을 클릭합니다.

## CloudWatch 로그 보기

CloudWatch Logs를 사용하면 Amazon EC2 인스턴스, Amazon CloudTrail 또는 기타 소스에서 로그 파일을 모니터링, 저장 및 액세스할 수 있습니다.

이 섹션에서는 Amazon EC2 인스턴스에 대한 CloudWatch 로그를 보는 방법을 보여줍니다.

1. [https://console.aws.amazon.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)에서 Amazon CloudWatch 콘솔로 이동합니다.

2. 왼쪽 탐색 패널에서 **로그**를 클릭합니다.

3. 로그를 보려는 로그 그룹을 선택합니다.

4. 보려는 로그 스트림을 선택합니다.

5. 오른쪽 패널에 로그 스트림이 표시됩니다.

## 참조

- [https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)
- [https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html)
- [https://aws.amazon.com/blogs/aws/new-cloudwatch-logs-agent/](https://aws.amazon.com/blogs/aws/new-cloudwatch-logs-agent/)
- [https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html)