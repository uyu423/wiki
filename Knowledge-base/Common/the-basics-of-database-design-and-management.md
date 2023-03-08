---
title: 데이터베이스 설계 및 관리의 기초
description: 
published: true
date: 2023-02-16T10:55:38.988Z
tags: 
editor: markdown
dateCreated: 2023-02-16T10:55:30.986Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [The Basics of Database Design and Management***English** document is available*](/en/Knowledge-base/Common/the-basics-of-database-design-and-management)
{.links-list}


# 데이터베이스 설계 및 관리의 기초

모든 소프트웨어 응용 프로그램의 성공 여부는 기본 데이터베이스의 설계 및 구현에 크게 좌우됩니다. 이 문서에서는 염두에 두어야 할 몇 가지 모범 사례를 포함하여 데이터베이스 디자인 및 관리의 기본 사항을 살펴보겠습니다.

## 데이터베이스 설계

데이터베이스를 디자인할 때 애플리케이션의 요구 사항을 이해하는 것부터 시작하는 것이 중요합니다. 어떤 데이터를 저장해야 합니까? 어떻게 사용됩니까? 서로 다른 데이터 항목 간의 관계는 무엇입니까?

데이터와 데이터 사용 방법을 잘 이해하고 나면 데이터베이스 설계를 시작할 수 있습니다. 명심해야 할 몇 가지 중요한 고려 사항이 있습니다.

### 정규화

데이터베이스 설계의 한 가지 중요한 목표는 중복성을 최소화하는 것입니다. 이를 정규화라고 합니다. 예를 들어 직원 데이터베이스를 생각해 보십시오. 직원마다 이름, 주소, 급여가 있습니다. 여러 직원이 동일한 주소를 사용하는 경우 데이터베이스에 한 번만 저장됩니다.

### 키

데이터베이스 테이블의 각 레코드를 고유하게 식별하려면 키를 사용해야 합니다. 기본 키는 테이블의 행을 고유하게 식별하는 열(또는 열 집합)입니다. 기본 키는 NULL일 수 없으며 고유해야 합니다.

### 인덱스

인덱스는 데이터베이스 테이블에서 데이터 검색 속도를 높이는 데 도움이 되는 데이터 구조입니다. 인덱스는 기본 키 제약 조건을 구현하는 데 사용됩니다. 또한 고유성 및 외래 키와 같은 다른 유형의 제약 조건을 구현하는 데 사용할 수도 있습니다.

## 데이터베이스 관리

데이터베이스가 설계되면 이를 구현하고 관리해야 합니다. 여기에는 데이터베이스 생성, 데이터베이스에 데이터 로드, 데이터베이스에서 쿼리 실행과 같은 작업이 포함됩니다.

데이터베이스를 관리할 때 염두에 두어야 할 몇 가지 중요한 고려 사항이 있습니다.

### 백업 및 복구

데이터 손실에 대비하여 강력한 백업 및 복구 계획을 수립하는 것이 중요합니다. 여기에는 데이터베이스의 정기적인 백업과 데이터 손실로부터 복구하는 방법에 대한 계획이 포함되어야 합니다.

### 보안

무단 액세스로부터 데이터를 보호하려면 데이터베이스 보안이 중요합니다. 여기에는 인증, 권한 부여 및 암호화와 같은 작업이 포함됩니다.

### 성능

데이터베이스 성능은 데이터베이스가 애플리케이션의 로드를 처리할 수 있도록 하는 데 중요합니다. 여기에는 인덱싱, 쿼리 최적화 및 부하 분산과 같은 작업이 포함됩니다.

## 자원

다음은 데이터베이스 설계 및 관리에 대한 추가 정보를 제공하는 몇 가지 리소스입니다.

- [데이터베이스 디자인 기초](https://www.guru99.com/database-design.html)
- [데이터베이스 설계의 정규화](https://www.essentialsql.com/get-ready-to-learn-sql-database-normalization-explained-in-simple-english/)
- [데이터베이스 설계의 핵심](https://www.studytonight.com/dbms/database-key.php)
- [데이터베이스 설계에서의 인덱스](https://www.essentialsql.com/what-is-a-database-index-introduction-to-indexes-in-sql/)
- [데이터베이스 관리 기초](https://searchsqlserver.techtarget.com/definition/database-management-system-DBMS)
- [데이터베이스 관리의 백업 및 복구](https://www.guru99.com/backup-recovery-database-management.html)
- [데이터베이스 관리의 보안](https://searchsqlserver.techtarget.com/definition/database-security)
- [데이터베이스 관리 성능](https://searchsqlserver.techtarget.com/definition/database-performance)