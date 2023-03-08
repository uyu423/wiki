---
title: MySQL 04: 고급 SQL 기술: JOIN, UNION 및 하위 쿼리
description: 
published: true
date: 2023-02-06T10:32:15.588Z
tags: 
editor: markdown
dateCreated: 2023-02-06T10:32:14.002Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [MySQL 04: Advanced SQL techniques: JOIN, UNION, and subqueries***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-04-advanced-sql-techniques-join-union-and-subqueries)
{.links-list}


MySQL은 수백만 개의 웹사이트와 애플리케이션에서 사용되는 강력한 데이터베이스 관리 시스템입니다. 데이터 작업을 쉽고 효율적으로 수행할 수 있는 다양한 기능과 옵션을 제공합니다.

이 게시물에서는 MySQL에서 데이터 작업에 사용할 수 있는 몇 가지 고급 SQL 기술을 살펴보겠습니다. 조인, 통합 및 하위 쿼리와 같은 주제를 다룰 것입니다. 이 게시물을 마치면 이러한 기술을 사용하여 MySQL에서 데이터 작업을 수행하는 방법을 잘 이해하게 될 것입니다.

## 조인

조인은 둘 이상의 테이블에서 단일 결과 집합으로 데이터를 결합하는 방법입니다. 조인은 여러 테이블에서 데이터를 검색하는 데 사용됩니다.

다양한 유형의 조인이 있지만 가장 일반적인 유형은 내부 조인입니다. 내부 조인은 조인 조건과 일치하는 두 테이블의 모든 행을 반환합니다.

다음은 내부 조인의 예입니다.

```sql
SELECT *
FROM table1
INNER JOIN table2
ON table1.id = table2.id
```

이 예에서는 id 열에서 table1과 table2라는 두 테이블을 조인합니다. 이 쿼리의 결과는 동일한 ID를 가진 두 테이블의 모든 행입니다.

## 노조

통합은 둘 이상의 테이블에서 단일 결과 집합으로 데이터를 결합하는 방법입니다. 조인과 달리 공용체에는 조인 조건이 필요하지 않습니다.

다음은 노동 조합의 예입니다.

```sql
SELECT *
FROM table1
UNION
SELECT *
FROM table2
```

이 예에서는 table1과 table2라는 두 테이블을 유니온합니다. 이 쿼리의 결과는 두 테이블의 모든 행입니다.

## 서브쿼리

하위 쿼리는 다른 쿼리 안에 중첩된 쿼리입니다. 하위 쿼리는 외부 쿼리에서 사용하는 데이터를 반환하는 데 사용됩니다.

다음은 하위 쿼리의 예입니다.

```sql
SELECT *
FROM table1
WHERE id IN (SELECT id
            FROM table2)
```

이 예제에서는 하위 쿼리를 사용하여 table2에도 있는 id를 가진 table1의 모든 행을 반환합니다.