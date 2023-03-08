---
title: AWS에 스프링 부트 배포
description: 
published: true
date: 2023-02-07T13:32:41.126Z
tags: 
editor: markdown
dateCreated: 2023-02-07T13:32:39.550Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot Deployment on AWS***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-deployment-on-aws)
{.links-list}



# AWS에 스프링 부트 배포

AWS에 Spring Boot 애플리케이션을 배포하려는 개발자는 사용 사례에 따라 다양한 옵션을 사용할 수 있습니다. 이 문서에서는 이러한 옵션 중 일부를 살펴보고 각 옵션을 사용하는 경우에 대한 팁을 제공합니다.

## 엘라스틱 빈스토크

AWS Elastic Beanstalk는 Spring Boot 애플리케이션을 배포하고 확장하기 위한 관리형 서비스를 원하는 개발자에게 좋은 옵션입니다. Elastic Beanstalk는 애플리케이션의 용량 프로비저닝, 로드 밸런싱 및 자동 확장을 처리합니다. 또한 Amazon Relational Database Service(RDS) 및 Amazon Simple Notification Service(SNS)와 같은 다른 AWS 서비스와 통합됩니다.

Elastic Beanstalk를 사용하려면 개발자는 Spring Boot 애플리케이션을 ZIP 또는 WAR 파일로 업로드하기만 하면 됩니다. 그런 다음 Elastic Beanstalk는 애플리케이션을 위한 환경을 자동으로 생성하고 해당 환경에 애플리케이션을 배포합니다.

Elastic Beanstalk는 Spring Boot 애플리케이션을 배포하고 확장하기 위한 관리형 서비스를 원하는 개발자에게 좋은 옵션입니다.

## Amazon Elastic Container Service(ECS)

Amazon ECS는 Spring Boot 애플리케이션을 컨테이너화하려는 개발자에게 좋은 옵션입니다. ECS는 AWS에서 컨테이너화된 애플리케이션을 쉽게 실행하고 확장할 수 있게 해주는 관리형 컨테이너 서비스입니다.

Amazon ECS를 사용하려면 개발자는 먼저 Docker를 사용하여 Spring Boot 애플리케이션을 컨테이너화해야 합니다. 그런 다음 컨테이너화된 애플리케이션을 실행하기 위한 청사진인 ECS 작업 정의를 생성할 수 있습니다. 작업 정의가 생성되면 개발자는 ECS 클러스터에서 작업을 실행할 수 있습니다. 그러면 Amazon ECS가 클러스터에서 작업을 시작하고 사용자가 사용할 수 있도록 합니다.

Amazon ECS는 Spring Boot 애플리케이션을 컨테이너화하려는 개발자에게 좋은 옵션입니다.

## Amazon Elastic Container Registry(ECR)

Amazon ECR은 Spring Boot 애플리케이션용 Docker 이미지를 저장하고 관리하려는 개발자에게 적합한 옵션입니다. ECR은 AWS에서 Docker 이미지를 쉽게 저장, 관리 및 배포할 수 있게 해주는 관리형 Docker 컨테이너 레지스트리 서비스입니다.

Amazon ECR을 사용하려면 개발자는 먼저 Spring Boot 애플리케이션용 리포지토리를 생성해야 합니다. 그런 다음 Docker 이미지를 리포지토리에 푸시할 수 있습니다. 이미지가 푸시되면 개발자는 Amazon ECS 또는 Kubernetes용 Amazon Elastic Container Service(EKS)에 애플리케이션을 배포할 수 있습니다.

Amazon ECR은 Spring Boot 애플리케이션용 Docker 이미지를 저장하고 관리하려는 개발자에게 적합한 옵션입니다.

## Amazon 단순 스토리지 서비스(S3)

Amazon S3는 Spring Boot 애플리케이션을 ZIP 또는 WAR 파일로 저장하려는 개발자에게 좋은 옵션입니다. S3는 AWS에서 파일을 쉽게 저장하고 검색할 수 있게 해주는 관리형 스토리지 서비스입니다.

Amazon S3를 사용하려면 개발자는 Spring Boot 애플리케이션을 ZIP 또는 WAR 파일로 업로드하기만 하면 됩니다. 그런 다음 S3에 파일을 저장하기 위한 컨테이너인 Amazon S3 버킷을 생성할 수 있습니다. 버킷이 생성되면 개발자는 Amazon Elastic Beanstalk 또는 Amazon ECS에 애플리케이션을 배포할 수 있습니다.

Amazon S3는 Spring Boot 애플리케이션을 ZIP 또는 WAR 파일로 저장하려는 개발자에게 좋은 옵션입니다.

## 아마존 관계형 데이터베이스 서비스(RDS)

Amazon RDS는 Spring Boot 애플리케이션에 관계형 데이터베이스를 사용하려는 개발자에게 좋은 옵션입니다. RDS는 AWS에서 관계형 데이터베이스를 쉽게 설정, 운영 및 확장할 수 있게 해주는 관리형 데이터베이스 서비스입니다.

Amazon RDS를 사용하려면 개발자가 먼저 Amazon RDS 인스턴스를 생성해야 합니다. 그런 다음 Spring Boot 애플리케이션용 데이터베이스를 생성할 수 있습니다. 데이터베이스가 생성되면 개발자는 Amazon Elastic Beanstalk 또는 Amazon ECS에 애플리케이션을 배포할 수 있습니다.

Amazon RDS는 Spring Boot 애플리케이션에 관계형 데이터베이스를 사용하려는 개발자에게 좋은 옵션입니다.

## Amazon 단순 알림 서비스(SNS)

Amazon SNS는 Spring Boot 애플리케이션에서 알림을 보내려는 개발자에게 좋은 옵션입니다. SNS는 이메일, SMS 또는 푸시 알림을 통해 사용자에게 쉽게 알림을 보낼 수 있는 관리형 알림 서비스입니다.

Amazon SNS를 사용하려면 개발자가 먼저 Amazon SNS 주제를 생성해야 합니다. 그런 다음 주제에 대한 사용자를 구독할 수 있습니다. 사용자가 구독하면 개발자는 주제에 메시지를 게시할 수 있습니다. 그러면 메시지가 구독자에게 전달됩니다.

Amazon SNS는 Spring Boot 애플리케이션에서 알림을 보내려는 개발자에게 좋은 옵션입니다.