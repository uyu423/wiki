---
title: VPC 환경에서 Elastic Beanstalk 을 사용해야할 때 알아둬야할 것들
description: 
published: true
date: 2022-11-25T20:38:13.079Z
tags: aws, elasticbeanstalk, elasticip, vpc
editor: markdown
dateCreated: 2022-11-25T20:37:51.253Z
---


> AWS 에서 프로젝트를 빌드하면서 Custom VPC 를 생성
> 하지만 VPC 에서 ElasticBeanstalk 환경을 구축하는데 외부 인터넷 연결 문제로 고생을 했다.
> 관련되어 체크해야할 VPC 설정들을 정리함
{.is-info}

# VPC 설정

## DNS 설정

- DNS 확인 활성화 :white_check_mark:
- DNS 호스트 이름 활성화 :white_check_mark:

# Subnet 설정

> 여기서는 모든 케이스가 Internet <-> Public Subnet <-> Private Subnet 로 통신한다고 가정한다. 

## Public Subnet의 경우

- **라우팅 테이블** (Routing Table)
  - 서브넷 상위 VPC 의 CIDR 이 등록되어 있는지 확인
  - `0.0.0.0/0` 이 인터넷 게이트웨이로 등록되어 있는지 확인
- **네트워크 ACL** (Network ACL)
  - 모든 트래픽(유형)이 `0.0.0.0/0`(소스) `Allow` 로 등록되어 있는지 확인
  
### Public Subnet 추가 설정

> VPC 생성할 때 Public Subnet 으로 생성하더라도 아래 설정이 기본 값으로 설정되지 않는다.
> 그로 인해 ElasticBeanstalk 에서 신규 EC2 인스턴스를 생성할 때 Public IP 할당이 일어나지 않아서, EC2가 ElasticBeanstalk 와 통신이 실패하는 문제가 발생한다.
> 해당 이슈 때문에 가장 많은 시간을 소요함 :rage:
> ```
> The EC2 instances failed to communicate with AWS Elastic Beanstalk, either because of configuration problems with the VPC or a failed EC2 instance. Check your VPC configuration and try launching the environment again.
> ```
> .
{.is-warning}

- 자동 할당 IP 설정
  - 퍼블릭 IPv4 주소 자동 할당 활성화 :white_check_mark:

## Private Subnet의 경우


# Security Group 설정

---

- https://notes.webutvikling.org/elastic-beanstalk-in-a-vpc/
{.links-list}
