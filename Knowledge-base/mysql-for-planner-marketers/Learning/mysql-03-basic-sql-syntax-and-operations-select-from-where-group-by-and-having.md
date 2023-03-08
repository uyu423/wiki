---
title: MySQL 03: 기본 SQL 구문 및 작업: SELECT, FROM, WHERE, GROUP BY 및 HAVING
description: 
published: true
date: 2023-02-06T09:32:26.350Z
tags: 
editor: markdown
dateCreated: 2023-02-06T09:32:20.855Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [MySQL 03: Basic SQL syntax and operations: SELECT, FROM, WHERE, GROUP BY, and HAVING***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-03-basic-sql-syntax-and-operations-select-from-where-group-by-and-having)
{.links-list}


# MySQL 03: 기본 SQL 구문 및 작업: SELECT, FROM, WHERE, GROUP BY 및 HAVING

## 소개

이 게시물에서는 MySQL에서 데이터 작업을 위한 기본 SQL 구문 및 작업을 다룰 것입니다. `SELECT`, `FROM`, `WHERE`, `GROUP BY` 및 `HAVING` 절을 사용하여 MySQL 데이터베이스에서 데이터를 쿼리하는 방법을 배웁니다.

## 선택하다

`SELECT` 절은 데이터베이스 테이블에서 검색하려는 열을 지정하는 데 사용됩니다. 예를 들어 다음 `SELECT` 문은 `employees` 테이블에서 `first_name` 및 `last_name` 열을 검색합니다.

```sql
SELECT first_name, last_name
FROM employees
```

테이블에서 모든 열을 검색하려면 열 목록 대신 `*` 문자를 사용할 수 있습니다.

```sql
SELECT *
FROM employees
```

## 에서

'FROM' 절은 데이터를 검색하려는 테이블을 지정하는 데 사용됩니다. 예를 들어 다음 `SELECT` 문은 `employees` 테이블에서 데이터를 검색합니다.

```sql
SELECT first_name, last_name
FROM employees
```

쉼표로 구분하여 `FROM` 절에 여러 테이블을 지정할 수 있습니다.

```sql
SELECT first_name, last_name
FROM employees, departments
```

## 어디

'WHERE' 절은 데이터베이스 테이블에서 데이터를 검색하기 위한 조건을 지정하는 데 사용됩니다. 예를 들어 다음 `SELECT` 문은 `employee_id`가 `1`인 `employees` 테이블에서 데이터를 검색합니다.

```sql
SELECT first_name, last_name
FROM employees
WHERE employee_id = 1
```

`AND` 및 `OR` 연산자를 사용하여 `WHERE` 절에 여러 조건을 지정할 수 있습니다.

```sql
SELECT first_name, last_name
FROM employees
WHERE employee_id = 1 OR employee_id = 2
```

## 그룹화 기준

'GROUP BY' 절은 데이터베이스 테이블에서 데이터를 그룹화하는 데 사용됩니다. 예를 들어 다음 `SELECT` 문은 `employees` 테이블에서 데이터를 검색하고 `department_id`별로 그룹화합니다.

```sql
SELECT department_id, count(*)
FROM employees
GROUP BY department_id
```

## 갖는

'HAVING' 절은 데이터베이스 테이블에서 데이터를 검색하기 위한 조건을 지정하는 데 사용됩니다. 예를 들어 다음 `SELECT` 문은 `department_id`가 `1`인 `employees` 테이블에서 데이터를 검색합니다.

```sql
SELECT department_id, count(*)
FROM employees
GROUP BY department_id
HAVING department_id = 1
```

## 결론

이 게시물에서는 MySQL에서 데이터 작업을 위한 기본 SQL 구문 및 작업을 다루었습니다. `SELECT`, `FROM`, `WHERE`, `GROUP BY` 및 `HAVING` 절을 사용하여 MySQL 데이터베이스에서 데이터를 쿼리하는 방법을 배웠습니다.