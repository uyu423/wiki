---
title: ElasticBeanstalk EC2 인스턴스를 private subnet 에서 실행시 VPC endpoint 설정
description: EC2 인스턴스를 prviate subnet 에 띄울 경우에 VPC endpoint 를 몇가지 생성해줘야 인스턴스가 정상적으로 프로비저닝 된다.
published: true
date: 2023-02-17T17:59:48.968Z
tags: aws, elasticbeanstalk, vpc, ec2
editor: markdown
dateCreated: 2022-11-26T15:31:40.385Z
---

- [VPC endpoint settings when running ElasticBeanstalk EC2 instances in a private subnet***English** version of this document is available*](/en/dev/AWS/VPC-endpoint-settings-when-running-ElasticBeanstalk-EC2-instances-in-a-private-subnet)
{.links-list}

> Custom VPC를 생성하고 ElasticBeanstalk EC2 인스턴스를 private subnet 에서 구동시키기 위해 정말 많은 삽질을 했다.
> 이후의 실수를 방지하기 위해 기록해둔다.
{.is-info}

# ElasticBeanstalk 구성

- **Public subnet**
  - Load Balancer
- **Private subnet**
  - EC2 (Network - Public IP 할당 off)
  
# VPC Endpoint 구성

- private subnet 에 있는 ElasticBeanstalk EC2 인스턴스들이 AWS 서비스들과 통신할 수 있도록 추가 설정이 필요하다. (이걸 VPC 생성 마법사에서 체크해주면 좋을텐데 안해준다)
- 해당 VPC 에 설정된 모든 private subent 과 연결되도록 **아래 엔드포인트들이 생성**되야한다.
  - `com.amazonaws.{region}.elasticbeanstalk`
  - `com.amazonaws.{region}.elasticbeanstalk-health` (Enhanced Log 를 사용하는 경우)
  - `com.amazonaws.{region}.cloudformation`
  - `com.amazonaws.{region}.ecr.api` (ECR을 사용하는 경우)
  - `com.amazonaws.{region}.ecr.dkr` (ECR을 사용하는 경우)
  - `com.amazonaws.{region}.logs` (CloudWatch)
  - `com.amazonaws.{region}.s3` (Gateway / Interface 둘 다)
  - `com.amazonaws.{region}.sqs`
- 위 엔드포인트 생성시 `Private DNS` 설정이 모두 체크되어야한다. (S3 Interface 제외)
- 실제론 사용하지 않는 서비스들이 추가되었을 수 있다. 그래도 뭐 상관 없는 듯.
- 별도의 Routing Table 설정할 필요는 없다.

# References

- [VPC 환경에서 Elastic Beanstalk 을 사용해야할 때 알아둬야할 것들*YOWU DEV WIKI*](https://wiki.yowu.dev/ko/dev/AWS/Things-to-know-when-using-Elastic-Beanstalk-in-a-VPC-environment)
- [Using Elastic Beanstalk with Amazon VPC*AWS Documents*](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/vpc.html#services-vpc-private-beanstalk)
{.links-list}