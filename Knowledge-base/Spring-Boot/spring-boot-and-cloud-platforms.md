---
title: 스프링 부트와 클라우드 플랫폼
description: 
published: true
date: 2023-02-05T10:55:46.748Z
tags: 
editor: markdown
dateCreated: 2023-02-05T10:55:41.129Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot and Cloud Platforms***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-cloud-platforms)
{.links-list}


# 스프링부트와 클라우드 플랫폼

## 소개

최근 몇 년 동안 많은 조직이 기존의 온프레미스 인프라에서 벗어나면서 클라우드 컴퓨팅이 점차 인기를 얻고 있습니다. 클라우드 플랫폼은 비용 절감, 확장성, 민첩성 향상 등 다양한 이점을 제공합니다.

Spring Boot는 웹 애플리케이션 및 마이크로 서비스를 구축하기 위한 인기 있는 Java 프레임워크입니다. "그냥 실행"할 수 있는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있습니다.

Spring Boot는 클라우드 플랫폼에 배포될 마이크로서비스를 구축하기 위한 훌륭한 선택입니다. 이 기사에서는 가장 인기 있는 클라우드 플랫폼과 Spring Boot 애플리케이션을 배포하는 방법을 살펴보겠습니다.

## 클라우드 플랫폼

선택할 수 있는 여러 가지 클라우드 플랫폼이 있으며 각각 고유한 장점과 단점이 있습니다. 가장 인기 있는 플랫폼은 다음과 같습니다.

* 아마존웹서비스(AWS)
* 마이크로소프트 애저
* 구글 클라우드 플랫폼(GCP)

### 아마존 웹 서비스(AWS)

AWS는 포괄적이고 널리 채택된 클라우드 플랫폼으로 175개 이상의 서비스를 제공합니다. 완전한 클라우드 서비스 세트를 원하고 이를 사용하는 방법을 배우기 위해 시간과 리소스를 기꺼이 투자하려는 조직에 적합한 선택입니다.

AWS는 다음을 포함하여 Spring Boot 애플리케이션에 매우 적합한 다양한 기능을 제공합니다.

* 손쉬운 배포 및 확장을 위한 Elastic Beanstalk
* 관리형 관계형 데이터베이스를 위한 Amazon Relational Database Service(RDS)
* 관리형 메시지 대기열용 Amazon Simple Queue Service(SQS)

### 마이크로소프트 애저

Azure는 컴퓨팅, 스토리지, 네트워킹 등을 포함한 광범위한 서비스를 제공하는 Microsoft의 클라우드 플랫폼입니다. 이미 Microsoft 제품 및 기술을 사용하고 있는 조직에 적합합니다.

Azure는 다음을 포함하여 Spring Boot 애플리케이션에 적합한 다양한 기능을 제공합니다.

* 손쉬운 배포 및 확장을 위한 Azure App Service
* 관리되는 관계형 데이터베이스용 Azure Database for MySQL
* 관리 메시지 큐용 Azure Service Bus

### 구글 클라우드 플랫폼(GCP)

GCP는 컴퓨팅, 스토리지, 네트워킹 등 다양한 서비스를 제공하는 Google의 클라우드 플랫폼입니다. Google 제품 및 기술을 사용하려는 조직에 적합합니다.

GCP는 다음을 포함하여 Spring Boot 애플리케이션에 매우 적합한 다양한 기능을 제공합니다.

* 손쉬운 배포 및 확장을 위한 Google App Engine
* 관리형 관계형 데이터베이스용 Cloud SQL
* 관리 메시지 대기열용 Cloud Pub/Sub

## 스프링 부트 애플리케이션을 클라우드에 배포

이제 가장 인기 있는 클라우드 플랫폼을 살펴보았으므로 Spring Boot 애플리케이션을 배포하는 방법을 살펴보겠습니다.

### 아마존 웹 서비스(AWS)

AWS는 Spring Boot 애플리케이션을 배포하는 데 사용할 수 있는 다양한 서비스를 제공합니다. 이 섹션에서는 가장 인기 있는 두 가지인 Elastic Beanstalk와 Amazon Relational Database Service(RDS)를 살펴보겠습니다.

#### 엘라스틱 빈스토크

Elastic Beanstalk는 AWS에서 Spring Boot 애플리케이션을 쉽게 배포하고 관리할 수 있게 해주는 서비스입니다. AWS 리소스 프로비저닝 및 구성, 애플리케이션 배포, 애플리케이션 상태 관리를 비롯한 모든 어려운 작업을 처리합니다.

Spring Boot 애플리케이션을 Elastic Beanstalk에 배포하려면 먼저 Elastic Beanstalk 환경을 생성해야 합니다. 이는 AWS Management Console, AWS Elastic Beanstalk 명령줄 인터페이스(CLI) 또는 AWS Elastic Beanstalk API를 사용하여 수행할 수 있습니다.

환경을 생성한 후에는 Elastic Beanstalk CLI 또는 Elastic Beanstalk API를 사용하여 애플리케이션을 배포할 수 있습니다.

#### 아마존 관계형 데이터베이스 서비스(RDS)

Amazon RDS는 클라우드에서 관계형 데이터베이스를 쉽게 설정, 운영 및 확장할 수 있게 해주는 관리형 관계형 데이터베이스 서비스입니다. 관계형 데이터베이스가 필요한 Spring Boot 애플리케이션에 적합합니다.

Amazon RDS를 Spring Boot 애플리케이션과 함께 사용하려면 먼저 Amazon RDS 인스턴스를 생성해야 합니다. 이는 AWS Management Console, AWS 명령줄 인터페이스(CLI) 또는 AWS API를 사용하여 수행할 수 있습니다.

Amazon RDS 인스턴스를 생성했으면 이를 사용하도록 Spring Boot 애플리케이션을 구성할 수 있습니다.

### 마이크로소프트 애저

Azure는 Spring Boot 애플리케이션을 배포하는 데 사용할 수 있는 다양한 서비스를 제공합니다. 이 섹션에서는 가장 인기 있는 두 가지인 Azure App Service와 Azure Database for MySQL을 살펴보겠습니다.

#### 애저 앱 서비스

Azure App Service는 Azure에서 Spring Boot 애플리케이션을 쉽게 배포하고 관리할 수 있게 해주는 관리형 플랫폼입니다. Azure 리소스 프로비저닝 및 구성, 애플리케이션 배포 및 애플리케이션 상태 관리를 포함하여 모든 어려운 작업을 처리합니다.

Spring Boot 애플리케이션을 Azure App Service에 배포하려면 먼저 Azure App Service 환경을 만들어야 합니다. Azure Portal, Azure CLI 또는 Azure API를 사용하여 이 작업을 수행할 수 있습니다.

Azure App Service 환경을 만든 후에는 Azure CLI 또는 Azure API를 사용하여 애플리케이션을 배포할 수 있습니다.

#### MySQL용 애저 데이터베이스

Azure Database for MySQL은 Azure에서 관계형 데이터베이스를 쉽게 설정, 운영 및 확장할 수 있는 관리형 관계형 데이터베이스 서비스입니다. 관계형 데이터베이스가 필요한 Spring Boot 애플리케이션에 적합합니다.

Spring Boot 애플리케이션에서 Azure Database for MySQL을 사용하려면 먼저 Azure Database for MySQL 서버를 만들어야 합니다. Azure Portal, Azure CLI 또는 Azure API를 사용하여 이 작업을 수행할 수 있습니다.

Azure Database for MySQL 서버를 만든 후에는 이를 사용하도록 Spring Boot 애플리케이션을 구성할 수 있습니다.

### 구글 클라우드 플랫폼(GCP)

GCP는 Spring Boot 애플리케이션을 배포하는 데 사용할 수 있는 다양한 서비스를 제공합니다. 이 섹션에서는 가장 인기 있는 두 가지인 Google App Engine과 MySQL용 Cloud SQL을 살펴보겠습니다.

#### 구글 앱 엔진

Google App Engine은 GCP에서 Spring Boot 애플리케이션을 쉽게 배포하고 관리할 수 있게 해주는 관리형 플랫폼입니다. GCP 리소스 프로비저닝 및 구성, 애플리케이션 배포, 애플리케이션 상태 관리를 포함한 모든 어려운 작업을 처리합니다.

Spring Boot 애플리케이션을 Google App Engine에 배포하려면 먼저 Google App Engine 환경을 만들어야 합니다. 이 작업은 GCP 콘솔, gcloud 명령줄 도구 또는 GCP API를 사용하여 수행할 수 있습니다.

Google App Engine 환경을 만든 후에는 gcloud 명령줄 도구 또는 GCP API를 사용하여 애플리케이션을 배포할 수 있습니다.

#### MySQL용 Cloud SQL

MySQL용 Cloud SQL은 관리형 관계형 데이터베이스 서비스로 GCP에서 관계형 데이터베이스를 쉽게 설정, 운영, 확장할 수 있습니다. 관계형 데이터베이스가 필요한 Spring Boot 애플리케이션에 적합합니다.

Spring Boot 애플리케이션에서 MySQL용 Cloud SQL을 사용하려면 먼저 MySQL용 Cloud SQL 인스턴스를 만들어야 합니다. 이 작업은 GCP 콘솔, gcloud 명령줄 도구 또는 GCP API를 사용하여 수행할 수 있습니다.

MySQL용 Cloud SQL 인스턴스를 만든 후에는 이를 사용하도록 Spring Boot 애플리케이션을 구성할 수 있습니다.

## 결론

이 기사에서는 Spring Boot가 클라우드 플랫폼에 배포될 마이크로서비스를 구축하는 데 탁월한 선택인 이유를 살펴보았습니다. 또한 가장 인기 있는 클라우드 플랫폼과 Spring Boot 애플리케이션을 배포하는 방법을 살펴보았습니다.