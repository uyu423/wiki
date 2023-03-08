---
title: MySQL 분석: 데이터 집계 및 보고 기술 마스터하기
description: 
published: true
date: 2023-02-06T22:33:38.471Z
tags: 
editor: markdown
dateCreated: 2023-02-06T22:33:36.677Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [MySQL Analytics: Mastering Data Aggregation and Reporting Techniques***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-analytics-mastering-data-aggregation-and-reporting-techniques)
{.links-list}


# MySQL 분석: 데이터 집계 및 보고 기술 마스터하기

데이터 분석은 정확한 최신 정보를 기반으로 정보에 입각한 의사 결정을 내리려는 모든 비즈니스에 매우 중요합니다. MySQL은 데이터 분석을 위한 많은 기능과 도구를 제공하는 강력한 데이터베이스 플랫폼입니다.

이 게시물에서는 MySQL의 데이터 집계 및 보고의 기본 사항을 다룹니다. SQL 쿼리를 사용하여 데이터를 집계하고 보고서를 생성하는 방법을 배웁니다. 또한 내장된 일부 MySQL 분석 기능 및 도구를 사용하는 방법도 배웁니다.

## 데이터 집계란?

데이터 집계는 여러 소스의 데이터를 단일 데이터 세트로 결합하는 프로세스입니다. 이것은 수동으로 또는 자동화된 도구를 사용하여 수행할 수 있습니다. 데이터 집계는 데이터 정리 및 구성, 분석용 데이터 준비 또는 보고서 생성에 자주 사용됩니다.

SQL 쿼리를 사용하여 데이터 집계를 수행할 수 있습니다. SQL(Structured Query Language)은 데이터베이스 액세스 및 조작을 위한 표준 언어입니다. SQL 쿼리를 사용하여 데이터를 선택, 삽입, 업데이트 또는 삭제할 수 있습니다. SQL 쿼리를 사용하여 데이터 집계를 수행할 수도 있습니다.

SQL 쿼리를 사용한 데이터 집계는 종종 "SQL 기반 데이터 집계"라고 합니다. SQL 기반 데이터 집계를 사용하여 여러 테이블의 데이터를 단일 데이터 세트로 결합할 수 있습니다. 또한 평균, 개수 및 합계와 같은 요약 통계를 계산하는 데 사용할 수 있습니다.

## SQL 기초

데이터 집계에 대해 알아보기 전에 몇 가지 기본 SQL 개념을 검토해 보겠습니다.

### 테이블

MySQL 데이터베이스는 테이블로 구성됩니다. 테이블은 행과 열로 구성된 데이터 모음입니다. 테이블은 각 테이블이 정보 모음을 저장하는 파일 시스템의 폴더와 유사합니다.

예를 들어 테이블은 고객 이름, 주소, 전화 번호와 같은 고객에 대한 정보를 저장할 수 있습니다. 다른 테이블은 주문 날짜, 주문 합계 및 주문 상태와 같은 주문에 대한 정보를 저장할 수 있습니다.

### 열

열은 테이블의 필드입니다. 각 열에는 이름과 데이터 유형이 있습니다. 데이터 유형은 열에 저장할 수 있는 데이터 유형을 정의합니다. 예를 들어 열 이름이 "customer_name"이고 데이터 유형이 "varchar"일 수 있습니다. 이는 열이 문자열(즉, 텍스트)을 저장할 수 있음을 의미합니다.

다른 일반적인 데이터 유형에는 "int"(정수), "decimal"(십진수) 및 "date"(날짜)가 있습니다.

### 행

행은 테이블의 레코드입니다. 행에는 고객 또는 주문과 같은 단일 엔터티에 해당하는 데이터가 포함됩니다.

예를 들어 "customers" 테이블의 행에는 "John Smith, 123 Main Street, 555-1212"라는 데이터가 포함될 수 있습니다. 이 행은 단일 고객인 John Smith를 나타냅니다. "고객" 테이블의 다른 행에는 "Jane Doe, 456 Elm Street, 555-1234" 데이터가 포함될 수 있습니다. 이 행은 다른 고객인 Jane Doe를 나타냅니다.

### 키

키는 테이블의 행을 고유하게 식별하는 열 또는 열 집합입니다. 기본 키는 테이블의 행을 고유하게 식별하는 열 또는 열 집합이며 NULL일 수 없습니다. 외래 키는 다른 테이블의 행을 식별하는 데 사용되는 한 테이블의 열 또는 열 집합입니다.

### SQL 구문

SQL 쿼리는 "SELECT", "INSERT", "UPDATE" 및 "DELETE"와 같은 명령으로 구성됩니다. 명령 다음에는 "FROM", "WHERE" 및 "ORDER BY"와 같은 하나 이상의 절이 옵니다. 절은 키워드와 값으로 구성됩니다.

예를 들어 다음 SQL 쿼리는 "customers" 테이블에서 모든 행을 선택합니다.

```sql
SELECT * FROM customers;
```

"SELECT" 명령 다음에는 데이터를 선택할 테이블을 지정하는 "FROM" 절이 옵니다. "*" 값은 모든 열을 선택하도록 지정합니다.

오류를 방지하려면 SQL 쿼리를 신중하게 구성해야 합니다. 예를 들어 다음 SQL 쿼리는 오류를 생성합니다.

```sql
SELECT * FROM table_does_not_exist;
```

데이터베이스에 "table_does_not_exist" 테이블이 없기 때문입니다.

## MySQL의 데이터 집계

MySQL의 데이터 집계는 SQL 쿼리를 사용하여 수행할 수 있습니다. 이 섹션에서는 가장 일반적인 데이터 집계 기술 중 일부를 다룹니다.

### 선택하다

"SELECT" 명령은 데이터베이스에서 데이터를 선택하는 데 사용됩니다. "SELECT" 명령 다음에는 데이터를 선택할 테이블을 지정하는 "FROM" 절이 옵니다. "*" 값은 모든 열을 선택하도록 지정합니다.

예를 들어 다음 SQL 쿼리는 "customers" 테이블에서 모든 행을 선택합니다.

```sql
SELECT * FROM customers;
```

"SELECT" 명령을 사용하여 특정 열을 선택할 수도 있습니다. 예를 들어 다음 SQL 쿼리는 "customers" 테이블에서 "customer_name" 및 "customer_address" 열을 선택합니다.

```sql
SELECT customer_name, customer_address FROM customers;
```

"SELECT" 명령을 사용하여 여러 테이블에서 데이터를 선택할 수도 있습니다. 예를 들어 다음 SQL 쿼리는 "customers" 및 "orders" 테이블에서 데이터를 선택합니다.

```sql
SELECT * FROM customers, orders;
```

"SELECT" 명령을 사용하여 조건에 따라 데이터를 선택할 수도 있습니다. 예를 들어 다음 SQL 쿼리는 "customer_name" 열이 "John Smith"인 "customers" 테이블에서 모든 행을 선택합니다.

```sql
SELECT * FROM customers WHERE customer_name = 'John Smith';
```

"WHERE" 절은 데이터 선택 조건을 지정하는 데 사용됩니다. 위의 예에서 조건은 "customer_name" 열이 "John Smith"와 같아야 한다는 것입니다.

"SELECT" 명령을 사용하여 데이터를 정렬할 수도 있습니다. 예를 들어 다음 SQL 쿼리는 "customers" 테이블에서 모든 행을 선택하고 "customer_name" 열을 기준으로 데이터를 정렬합니다.

```sql
SELECT * FROM customers ORDER BY customer_name;
```

"ORDER BY" 절은 데이터를 정렬할 열을 지정하는 데 사용됩니다. 위의 예에서 데이터는 "customer_name" 열을 기준으로 정렬됩니다.

### 삽입

"INSERT" 명령은 데이터베이스에 데이터를 삽입하는 데 사용됩니다. "INSERT" 명령 다음에는 데이터를 삽입할 테이블을 지정하는 "INTO" 절이 옵니다. "VALUES" 절은 삽입할 값을 지정하는 데 사용됩니다.

예를 들어 다음 SQL 쿼리는 "customers" 테이블에 행을 삽입합니다.

```sql
INSERT INTO customers (customer_name, customer_address, customer_phone)
VALUES ('John Smith', '123 Main Street', '555-1212');
```

"INSERT" 명령 다음에는 "customers" 테이블을 지정하는 "INTO" 절이 옵니다. "VALUES" 절은 테이블에 삽입할 값을 지정합니다. 위의 예에서 값은 "John Smith", "123 Main Street" 및 "555-1212"입니다.

### 업데이트

"UPDATE" 명령은 데이터베이스의 데이터를 업데이트하는 데 사용됩니다. "UPDATE" 명령 다음에는 업데이트할 열을 지정하는 "SET" 절이 옵니다. "WHERE" 절은 데이터 업데이트 조건을 지정하는 데 사용됩니다.

예를 들어 다음 SQL 쿼리는 "customers" 테이블의 "customer_name" 열을 업데이트합니다.

```sql
UPDATE customers SET customer_name = 'Jane Doe' WHERE customer_id = 1;
```

"UPDATE" 명령 다음에는 "customer_name" 열을 지정하는 "SET" 절이 옵니다. "WHERE" 절은 데이터 업데이트 조건을 지정합니다. 위의 예에서 조건은 "customer_id" 열이 "1"과 같아야 한다는 것입니다.

### 삭제

"DELETE" 명령은 데이터베이스에서 데이터를 삭제하는 데 사용됩니다. "DELETE" 명령 다음에는 데이터를 삭제할 테이블을 지정하는 "FROM" 절이 옵니다. "WHERE" 절은 데이터 삭제 조건을 지정하는 데 사용됩니다.

예를 들어 다음 SQL 쿼리는 "customers" 테이블에서 모든 행을 삭제합니다.

```sql
DELETE FROM customers;
```

"DELETE" 명령 다음에는 "customers" 테이블을 지정하는 "FROM" 절이 옵니다. 이 예에서는 "WHERE" 절이 사용되지 않으므로 "customers" 테이블의 모든 행이 삭제됩니다.

## MySQL 분석 기능 및 도구

MySQL은 데이터 분석을 위한 많은 기능과 도구를 제공합니다. 이 섹션에서는 가장 일반적인 MySQL 분석 기능 및 도구 중 일부를 다룹니다.

### MySQL 워크벤치

MySQL Workbench는 MySQL 데이터베이스 작업을 위한 시각적 도구입니다. MySQL Workbench를 사용하여 테이블을 생성 및 편집하고, SQL 쿼리를 실행하고, 보고서를 생성할 수 있습니다.

MySQL Workbench는 [MySQL Workbench](https://www.mysql.com/products/workbench/)에서 다운로드할 수 있습니다.

### MySQL 보고 도구

MySQL은 보고서 생성을 위한 여러 도구를 제공합니다. 이러한 도구에는 MySQL 보고서 작성기 및 MySQL 보고 서비스가 포함됩니다.

MySQL Report Builder는 보고서 작성을 위한 그래픽 도구입니다. MySQL Report Builder는 [MySQL Report Builder](https://www.mysql.com/products/workbench/reporting-tools/)에서 다운로드할 수 있습니다.

MySQL 보고 서비스는 보고서를 만들고 공유하기 위한 웹 기반 도구입니다. MySQL 보고 서비스는 [MySQL 보고 서비스](https://reporting.mysql.com/)에서 사용할 수 있습니다.

### MySQL 차트

MySQL Charts는 차트와 그래프를 생성하기 위한 웹 기반 도구입니다. MySQL 차트는 [MySQL 차트](https://charts.mysql.com/)에서 사용할 수 있습니다.

## 결론

이 게시물에서는 MySQL의 데이터 집계 및 보고의 기본 사항을 다뤘습니다. SQL 쿼리를 사용하여 데이터를 집계하고 보고서를 생성하는 방법을 배웠습니다. 또한 내장된 일부 MySQL 분석 기능 및 도구를 사용하는 방법도 배웠습니다.