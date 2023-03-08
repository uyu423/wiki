---
title: AWS CloudWatch: 클라우드 애플리케이션 모니터링 및 디버깅
description: 
published: true
date: 2023-02-09T16:55:41.912Z
tags: 
editor: markdown
dateCreated: 2023-02-09T16:55:35.635Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS CloudWatch: Monitoring and Debugging Cloud Applications***English** document is available*](/en/Knowledge-base/Cloud/aws-cloudwatch-monitoring-and-debugging-cloud-applications)
{.links-list}


# AWS CloudWatch: 클라우드 애플리케이션 모니터링 및 디버깅

## 소개

CloudWatch는 AWS 클라우드 리소스 및 AWS에서 실행되는 애플리케이션에 대한 모니터링 서비스입니다. CloudWatch는 애플리케이션을 모니터링하고, 시스템 전체의 성능 변화를 이해 및 대응하고, 리소스 활용을 최적화하고, 운영 상태에 대한 통합 보기를 얻기 위한 데이터 및 실행 가능한 통찰력을 제공합니다. CloudWatch를 사용하여 지표를 수집 및 추적하고, 경보를 설정하고, AWS 리소스의 변경 사항에 자동으로 대응할 수 있습니다.

이 기사에서는 CloudWatch의 작동 방식과 이를 사용하여 클라우드 애플리케이션을 모니터링하고 디버깅하는 방법을 살펴보겠습니다.

## CloudWatch 작동 방식

CloudWatch는 Amazon EC2 인스턴스, Amazon DynamoDB 테이블 및 Amazon RDS DB 인스턴스와 같은 AWS 리소스에서 데이터를 수집합니다. 그런 다음 이 데이터는 리소스 및 애플리케이션의 성능을 모니터링하는 데 사용할 수 있는 메트릭을 생성하는 데 사용됩니다.

CloudWatch를 사용하여 리소스 및 애플리케이션에서 로그 데이터를 수집할 수도 있습니다. 이 데이터는 문제를 해결하고 추세를 식별하는 데 사용할 수 있습니다.

## CloudWatch로 모니터링

CloudWatch는 다음 두 가지 방법으로 리소스와 애플리케이션을 모니터링하는 데 사용할 수 있습니다.

- **지표**: CloudWatch 지표는 리소스 및 애플리케이션의 성능을 모니터링하는 데 사용할 수 있는 통계 데이터 포인트입니다. 지표는 CloudWatch에서 수집한 데이터에서 생성됩니다.

- **로그**: CloudWatch 로그는 리소스 및 애플리케이션의 활동 기록입니다. 로그를 사용하여 문제를 해결하고 추세를 식별할 수 있습니다.

## CloudWatch 설정

CloudWatch를 사용하려면 먼저 Amazon CloudWatch Logs 그룹과 Amazon CloudWatch Logs 스트림을 생성해야 합니다.

다음으로 EC2 인스턴스에 CloudWatch Logs 에이전트를 설치해야 합니다. CloudWatch Logs 에이전트는 EC2 인스턴스에서 실행되고 로그 데이터를 CloudWatch로 전송하는 소프트웨어 프로그램입니다.

CloudWatch Logs 에이전트가 EC2 인스턴스에 설치되고 실행되면 CloudWatch로 로그 데이터 전송을 시작할 수 있습니다.

## CloudWatch로 지표 수집

CloudWatch 지표 데이터는 5분 간격으로 수집되며 2주 동안 저장됩니다.

CloudWatch로 지표를 수집하려면 먼저 지표 필터를 생성해야 합니다. 측정항목 필터는 로그 데이터의 패턴과 일치하고 로그 항목에서 측정항목 데이터를 추출합니다.

다음으로 지표 경보를 생성해야 합니다. 지표 경보는 지표를 감시하고 지표가 임계값을 초과하면 작업을 트리거합니다.

## CloudWatch로 로그 수집하기

CloudWatch 로그 데이터는 1분 간격으로 수집되며 14일 동안 저장됩니다.

CloudWatch로 로그를 수집하려면 먼저 로그 그룹을 생성해야 합니다. 로그 그룹은 보존 기간이 동일한 로그 모음입니다.

다음으로 로그 스트림을 생성해야 합니다. 로그 스트림은 단일 소스의 일련의 로그 이벤트입니다.

로그 그룹과 로그 스트림을 생성하면 CloudWatch로 로그 데이터 전송을 시작할 수 있습니다.

## CloudWatch로 알림 보내기

지표 경보가 트리거될 때 CloudWatch를 사용하여 알림을 보낼 수 있습니다. Amazon SNS, Amazon SQS 또는 이메일을 통해 알림을 보낼 수 있습니다.

CloudWatch로 알림을 보내려면 먼저 Amazon SNS 주제를 생성해야 합니다. Amazon SNS 주제는 수신자가 Amazon SNS 메시지를 구독할 수 있도록 하는 논리적 액세스 지점입니다.

다음으로 Amazon SQS 대기열을 생성해야 합니다. Amazon SQS 대기열은 소비자가 메시지를 처리할 때까지 메시지를 저장하는 버퍼입니다.

Amazon SNS 주제와 Amazon SQS 대기열을 생성한 후에는 알림을 보내도록 지표 경보를 구성할 수 있습니다.

## 결론

이 기사에서는 CloudWatch가 작동하는 방식과 이를 사용하여 클라우드 애플리케이션을 모니터링하고 디버깅하는 방법을 살펴보았습니다. 또한 CloudWatch를 설정하는 방법과 CloudWatch를 사용하여 지표 및 로그를 수집하는 방법도 살펴보았습니다. 마지막으로 CloudWatch로 알림을 보내는 방법을 살펴보았습니다.