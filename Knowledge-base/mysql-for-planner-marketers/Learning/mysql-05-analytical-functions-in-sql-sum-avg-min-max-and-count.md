---
title: MySQL 05: SQL의 분석 함수: SUM, AVG, MIN, MAX 및 COUNT
description: 
published: true
date: 2023-02-06T11:32:24.904Z
tags: 
editor: markdown
dateCreated: 2023-02-06T11:32:23.276Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [MySQL 05: Analytical functions in SQL: SUM, AVG, MIN, MAX, and COUNT***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-05-analytical-functions-in-sql-sum-avg-min-max-and-count)
{.links-list}


# MySQL 05: SQL의 분석 함수: SUM, AVG, MIN, MAX 및 COUNT

분석 함수는 데이터 작업을 위한 SQL의 강력한 도구입니다. 이 게시물에서는 SUM, AVG, MIN, MAX 및 COUNT 함수를 사용하여 MySQL에서 데이터 작업을 수행하는 방법을 살펴보겠습니다.

## 합계

SUM 함수는 데이터 열의 합계를 반환하는 데 사용됩니다. 예를 들어 숫자 열이 있는 데이터 테이블이 있는 경우 SUM 함수를 사용하여 해당 열에 있는 모든 숫자의 합계를 얻을 수 있습니다.

```mysql
SELECT SUM(number_column)
FROM table_name;
```

## 평균

AVG 함수는 데이터 열의 평균을 반환하는 데 사용됩니다. 예를 들어 숫자 열이 있는 데이터 테이블이 있는 경우 AVG 함수를 사용하여 해당 열에 있는 모든 숫자의 평균을 구할 수 있습니다.

```mysql
SELECT AVG(number_column)
FROM table_name;
```

## 분

MIN 함수는 데이터 열의 최소값을 반환하는 데 사용됩니다. 예를 들어 숫자 열이 있는 데이터 테이블이 있는 경우 MIN 함수를 사용하여 해당 열의 최소 수를 얻을 수 있습니다.

```mysql
SELECT MIN(number_column)
FROM table_name;
```

## 맥스

MAX 함수는 데이터 열의 최대값을 반환하는 데 사용됩니다. 예를 들어 숫자 열이 있는 데이터 테이블이 있는 경우 MAX 함수를 사용하여 해당 열의 최대 수를 얻을 수 있습니다.

```mysql
SELECT MAX(number_column)
FROM table_name;
```

## 세다

COUNT 함수는 테이블의 행 수를 반환하는 데 사용됩니다. 예를 들어 데이터 테이블이 있는 경우 COUNT 함수를 사용하여 해당 테이블의 행 수를 가져올 수 있습니다.

```mysql
SELECT COUNT(*)
FROM table_name;
```

다음은 SQL에서 분석 함수를 사용하여 데이터 작업을 수행할 수 있는 몇 가지 방법입니다. 자세한 내용은 아래 리소스를 확인하세요.

## 자원

- [MySQL 문서: 분석 함수](https://dev.mysql.com/doc/refman/8.0/en/group-by-functions.html)
- [스택 오버플로: count(*), count(1) 및 count(columnName)의 차이점은 무엇입니까](https://stackoverflow.com/questions/3696867/what-is-the-difference-between-count- 1-and-count-columnname)
- [W3Schools: SQL COUNT](https://www.w3schools.com/sql/sql_count.asp)