---
title: AWS Auto Scaling: 로드에 따라 자동으로 클라우드 리소스 확장
description: 
published: true
date: 2023-01-31T20:23:51.867Z
tags: 
editor: markdown
dateCreated: 2023-01-31T20:23:50.278Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [AWS Auto Scaling: Automatically Scaling Cloud Resources Based on Load***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-auto-scaling-automatically-scaling-cloud-resources-based-on-load)
{.links-list}


# AWS Auto Scaling: 부하에 따라 자동으로 클라우드 자원을 확장

Auto Scaling은 조직이 수요에 따라 Amazon Web Services(AWS) 리소스를 자동으로 확장하거나 축소하여 비용을 절감하고 필요할 때 리소스를 사용할 수 있도록 하는 클라우드 컴퓨팅 기능입니다.

AWS Auto Scaling은 필요할 때 AWS 리소스를 사용할 수 있고 유휴 리소스에 대해 비용을 지불하지 않도록 하는 비용 효율적인 방법입니다. 트래픽 급증을 처리하는 데 필요한 리소스를 확보하여 애플리케이션의 성능을 개선하는 좋은 방법이기도 합니다.

Auto Scaling은 Amazon Elastic Compute Cloud(EC2), Amazon Elastic Container Service(ECS), Amazon Relational Database Service(RDS) 및 기타 AWS 서비스의 기능입니다.

Auto Scaling을 구성할 때 AWS에서 유지 관리할 최소 및 최대 인스턴스 수를 지정합니다. 그런 다음 AWS는 이러한 한도 내에서 유지하기 위해 필요에 따라 인스턴스를 추가하거나 제거합니다. AWS가 리소스를 확장 또는 축소하는 방법을 결정하는 조정 정책을 지정할 수도 있습니다. 예를 들어 CPU 사용률이 80%를 초과하면 AWS가 더 많은 인스턴스를 추가하도록 지정할 수 있습니다.

AWS Auto Scaling은 AWS 요금을 절약하고 애플리케이션의 성능을 개선할 수 있는 좋은 방법입니다. Auto Scaling의 작동 방식을 이해하고 올바르게 구성하는 것이 중요하지만 올바르게 사용하지 않으면 의도하지 않은 결과가 발생할 수 있습니다.

## AWS Auto Scaling 작동 방식

AWS Auto Scaling은 "플릿"이라고 하는 EC2 인스턴스 그룹을 유지 관리하여 작동합니다. 이 플릿은 플릿을 확장 또는 축소하는 방법을 결정하는 설정 모음인 "자동 확장 그룹"(ASG)에서 관리합니다.

ASG에는 최소 및 최대 인스턴스 수, 원하는 용량 및 조정 정책을 포함하여 구성 가능한 여러 설정이 포함되어 있습니다.

ASG를 만들 때 유지하려는 최소 및 최대 인스턴스 수를 지정해야 합니다. 그런 다음 ASG는 이러한 한도 내에서 유지하기 위해 필요에 따라 플릿을 확장하거나 축소합니다.

ASG가 주어진 시간에 유지하려는 인스턴스 수인 원하는 용량을 지정할 수도 있습니다. ASG는 이 원하는 용량에 도달하기 위해 필요에 따라 플릿을 확장하거나 축소합니다.

ASG에는 여러 조정 정책도 포함되어 있습니다. 이러한 정책은 ASG가 수요 변화에 대응하여 플릿을 확장 또는 축소하는 방법을 결정합니다.

예를 들어 CPU 사용률이 80%를 초과하면 인스턴스를 더 추가하라는 조정 정책을 지정할 수 있습니다. 이 정책은 CPU 사용률이 80%를 초과할 때 ASG가 플릿에 더 많은 인스턴스를 추가하도록 합니다.

또한 RPS(초당 요청 수) 또는 BPS(초당 바이트 수)의 변경에 따라 ASG가 집합을 조정하는 방법을 결정하는 조정 정책을 지정할 수 있습니다.

Auto Scaling은 AWS 비용을 절감하고 애플리케이션 성능을 향상시키는 좋은 방법입니다. Auto Scaling의 작동 방식을 이해하고 올바르게 구성하는 것이 중요하지만 올바르게 사용하지 않으면 의도하지 않은 결과가 발생할 수 있습니다.

## AWS Auto Scaling 구성

AWS Auto Scaling은 Amazon EC2, Amazon ECS, Amazon RDS 및 기타 AWS 서비스의 기능입니다.

Auto Scaling을 구성할 때 AWS에서 유지 관리할 최소 및 최대 인스턴스 수를 지정합니다. 그런 다음 AWS는 이러한 한도 내에서 유지하기 위해 필요에 따라 인스턴스를 추가하거나 제거합니다. AWS가 리소스를 확장 또는 축소하는 방법을 결정하는 조정 정책을 지정할 수도 있습니다. 예를 들어 CPU 사용률이 80%를 초과하면 AWS가 더 많은 인스턴스를 추가하도록 지정할 수 있습니다.

Auto Scaling의 작동 방식을 이해하고 올바르게 구성하는 것이 중요하지만 올바르게 사용하지 않으면 의도하지 않은 결과가 발생할 수 있습니다.

예를 들어 CPU 사용률이 80% 이상일 때 인스턴스를 더 추가하라는 조정 정책을 지정했지만 추가할 수 있는 인스턴스 수를 제한할 방법이 없는 경우 AWS는 인스턴스를 계속 추가합니다. 지정한 최대 인스턴스 수에 도달했습니다. 이로 인해 예기치 않게 높은 AWS 요금이 청구될 수 있습니다.

이를 방지하기 위해 "확장 계획"을 사용할 수 있습니다. 조정 계획은 ASG가 집합을 확장하거나 축소하는 방법을 결정하는 설정 모음입니다.

조정 계획에는 최소 및 최대 인스턴스 수, 원하는 용량 및 조정 정책을 포함하여 구성 가능한 여러 설정이 포함됩니다.

조정 계획을 사용하여 지정된 기간에 추가할 수 있는 최대 인스턴스 수를 지정하여 추가할 수 있는 인스턴스 수를 제한할 수 있습니다. 예를 들어 24시간 동안 10개 이상의 인스턴스를 추가할 수 없도록 지정할 수 있습니다.

또한 조정 계획을 사용하여 유지 관리해야 하는 최소 인스턴스 수를 지정하여 제거할 수 있는 인스턴스 수를 제한할 수 있습니다. 예를 들어 최소 2개의 인스턴스를 항상 유지 관리하도록 지정할 수 있습니다.

## 결론

AWS Auto Scaling은 필요할 때 AWS 리소스를 사용할 수 있고 유휴 리소스에 대해 비용을 지불하지 않도록 하는 비용 효율적인 방법입니다. 트래픽 급증을 처리하는 데 필요한 리소스를 확보하여 애플리케이션의 성능을 개선하는 좋은 방법이기도 합니다.

Auto Scaling은 Amazon EC2, Amazon ECS, Amazon RDS 및 기타 AWS 서비스의 기능입니다.

Auto Scaling을 구성할 때 AWS에서 유지 관리할 최소 및 최대 인스턴스 수를 지정합니다. 그런 다음 AWS는 이러한 한도 내에서 유지하기 위해 필요에 따라 인스턴스를 추가하거나 제거합니다. AWS가 리소스를 확장 또는 축소하는 방법을 결정하는 조정 정책을 지정할 수도 있습니다.

Auto Scaling의 작동 방식을 이해하고 올바르게 구성하는 것이 중요하지만 올바르게 사용하지 않으면 의도하지 않은 결과가 발생할 수 있습니다.

AWS Auto Scaling에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- [AWS Auto Scaling 설명서](https://docs.aws.amazon.com/autoscaling/latest/userguide/WhatIsAutoScaling.html)
- [Auto Scaling 그룹](https://docs.aws.amazon.com/autoscaling/latest/userguide/AutoScalingGroups.html)
- [확장 계획](https://docs.aws.amazon.com/autoscaling/latest/userguide/ScalingPlans.html)