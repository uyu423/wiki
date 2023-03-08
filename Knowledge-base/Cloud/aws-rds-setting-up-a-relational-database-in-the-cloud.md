---
title: AWS RDS: 클라우드에서 관계형 데이터베이스 설정
description: 
published: true
date: 2023-02-17T18:17:31.891Z
tags: 
editor: markdown
dateCreated: 2023-01-31T02:25:34.333Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [AWS RDS: Setting Up a Relational Database in the Cloud***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-rds-setting-up-a-relational-database-in-the-cloud)
{.links-list}



# AWS RDS: 클라우드에서 관계형 데이터베이스 설정

AWS Relational Database Service(RDS)는 MySQL, MariaDB, Oracle, Microsoft SQL Server 및 PostgreSQL을 비롯한 여러 데이터베이스 엔진을 지원하는 관리형 데이터베이스 서비스입니다. RDS를 사용하면 클라우드에서 관계형 데이터베이스를 쉽게 설정, 운영 및 확장할 수 있습니다.

이 기사에서는 AWS RDS에서 MySQL 데이터베이스를 설정하는 과정을 안내합니다. 또한 데이터베이스를 보호하는 방법과 발생할 수 있는 일반적인 문제를 해결하는 방법에 대한 몇 가지 팁을 제공합니다.

## AWS RDS에서 MySQL 데이터베이스 생성

AWS RDS에서 MySQL 데이터베이스를 생성하려면 먼저 Amazon Web Services(AWS) 계정을 생성해야 합니다. 아직 AWS 계정이 없다면 http://aws.amazon.com/에서 계정을 생성할 수 있습니다.

AWS 계정을 생성한 후 Amazon RDS 홈 페이지로 이동하고 "Launch DB Instance" 버튼을 클릭하여 RDS 콘솔을 시작할 수 있습니다.

다음 페이지에서 "MySQL" 엔진을 선택한 다음 "Standard Create" 옵션을 선택해야 합니다.

![표준 생성 옵션](https://i.imgur.com/1ly7YUV.png)

다음 페이지에서 데이터베이스 인스턴스의 이름과 데이터베이스에 연결하는 데 사용할 사용자 이름 및 암호를 제공해야 합니다.

![데이터베이스 인스턴스](https://i.imgur.com/LxhmJN7.png)

또한 데이터베이스 인스턴스의 크기와 위치할 지역을 선택해야 합니다. 이 예에서는 "db.t2.micro" 인스턴스 유형과 "미국 동부(버지니아 북부)" 리전을 사용합니다.

![데이터베이스 인스턴스 유형](https://i.imgur.com/rVg0U6Z.png)

다음 페이지에서 데이터베이스 인스턴스에 대한 결제 알림 및 태그 지정을 활성화할지 여부를 선택해야 합니다. 이 예에서는 두 옵션을 모두 활성화합니다.

![데이터베이스 인스턴스 태깅](https://i.imgur.com/eiU3Qnl.png)

다음 페이지에서 데이터베이스 인스턴스에 대한 설정을 지정해야 합니다. 이 예에서는 기본 설정을 사용합니다.

![데이터베이스 인스턴스 설정](https://i.imgur.com/xk0tU8S.png)

다음 페이지에서 데이터베이스 인스턴스에 대한 설정을 검토한 다음 "Launch DB Instance" 버튼을 클릭해야 합니다.

![데이터베이스 인스턴스 검토](https://i.imgur.com/TGiukmn.png)

이제 데이터베이스 인스턴스가 생성되고 몇 분 안에 사용할 수 있습니다.

## MySQL 데이터베이스에 연결하기

데이터베이스 인스턴스가 생성되면 MySQL Workbench와 같은 MySQL 호환 클라이언트를 사용하여 연결할 수 있습니다. 데이터베이스 인스턴스에 연결하려면 다음 정보를 제공해야 합니다.

- **엔드포인트**: 데이터베이스 인스턴스의 URL입니다. RDS 콘솔의 "연결 및 보안" 섹션에서 이 정보를 찾을 수 있습니다.

- **포트**: MySQL의 기본 포트는 3306입니다.

- **사용자 이름**: 데이터베이스 인스턴스를 시작할 때 지정한 사용자 이름입니다.

- **암호**: 데이터베이스 인스턴스를 시작할 때 지정한 암호입니다.

![데이터베이스 인스턴스 연결](https://i.imgur.com/CnjNJTV.png)

이제 데이터베이스에 연결하고 SQL 쿼리를 실행할 수 있습니다.

## MySQL 데이터베이스 보안

무단 액세스를 방지하려면 MySQL 데이터베이스를 보호하는 것이 중요합니다. AWS RDS를 사용하면 데이터베이스 인스턴스에 대한 액세스를 제어하는 데 사용할 수 있는 방화벽을 제공하여 데이터베이스를 쉽게 보호할 수 있습니다.

방화벽에 새 규칙을 추가하려면 RDS 콘솔의 "보안 그룹" 섹션으로 이동하고 "인바운드 규칙 편집" 버튼을 클릭합니다.

![데이터베이스 인스턴스 보안 그룹](https://i.imgur.com/Jz4U3vN.png)

다음 페이지에서 규칙 유형과 규칙의 소스 및 대상을 지정해야 합니다. 이 예에서는 모든 소스(0.0.0.0/0)에서 데이터베이스 인스턴스에 대한 액세스를 허용합니다.

![데이터베이스 인스턴스 보안 그룹 규칙](https://i.imgur.com/taY0TGi.png)

이제 "규칙 저장" 버튼을 클릭하여 변경 사항을 저장할 수 있습니다.

## MySQL 데이터베이스 문제 해결

AWS RDS에서 MySQL 데이터베이스를 설정하거나 사용할 때 발생할 수 있는 몇 가지 일반적인 문제가 있습니다.

- **연결 문제**: 데이터베이스에 연결하는 데 문제가 있는 경우 올바른 끝점, 포트 및 자격 증명을 사용하고 있는지 확인하십시오. 방화벽을 일시적으로 비활성화하여 이것이 문제의 원인인지 확인할 수도 있습니다.

- **느린 성능**: 성능이 저하되는 경우 워크로드에 올바른 인스턴스 유형을 사용하고 있는지 확인하십시오. 데이터베이스 인스턴스의 크기를 늘려야 할 수도 있습니다.

- **1040 오류**: "1040 - 너무 많은 연결" 오류를 수신하는 경우 데이터베이스 인스턴스의 크기를 늘려야 합니다.