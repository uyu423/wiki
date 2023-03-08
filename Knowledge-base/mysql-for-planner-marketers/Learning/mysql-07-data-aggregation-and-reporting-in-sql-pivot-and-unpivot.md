---
title: MySQL 07: SQL의 데이터 집계 및 보고: PIVOT 및 UNPIVOT
description: 
published: true
date: 2023-02-06T13:32:37.460Z
tags: 
editor: markdown
dateCreated: 2023-02-06T13:32:35.882Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [MySQL 07: Data aggregation and reporting in SQL: PIVOT and UNPIVOT***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-07-data-aggregation-and-reporting-in-sql-pivot-and-unpivot)
{.links-list}


MySQL 07: SQL의 데이터 집계 및 보고: PIVOT 및 UNPIVOT

비즈니스에서 의사 결정을 내리기 위해 데이터를 집계하고 보고하는 경우가 많습니다. 예를 들어 회사는 리소스를 어디에 할당해야 하는지 더 잘 이해하기 위해 각 지역에서 얼마나 많은 제품이 판매되었는지 알고자 할 수 있습니다.

이 게시물에서는 SQL PIVOT 및 UNPIVOT 연산자를 사용하여 MySQL에서 데이터를 집계하고 보고하는 방법을 알아봅니다.

피벗

PIVOT 연산자는 행을 열로 변환하는 데 사용됩니다. 행에 데이터가 있는 테이블을 입력으로 사용하고 열에 데이터가 있는 테이블을 출력합니다.

PIVOT을 사용하려면 먼저 행으로 변환할 열을 지정해야 합니다. FOR 절을 사용하여 이를 수행할 수 있습니다. 예를 들어 다음 쿼리는 Region 및 Product 열을 행으로 변환합니다.

```sql
SELECT *
FROM mytable
PIVOT (
  SUM(Sales)
  FOR Region IN ('East', 'West', 'North', 'South')
) AS pvt;
```

위의 쿼리에서는 SUM 함수를 사용하여 Sales 열을 집계합니다. 또한 IN 절을 사용하여 열로 변환하려는 값을 지정합니다.

쿼리 출력은 다음과 같습니다.

| | 동쪽 | 웨스트 | 북쪽 | 남쪽 |
| --- | --- | --- | --- | --- |
| 제품 A | 10 | 20 | 30 | 40 |
| 제품 B | 50 | 60 | 70 | 80 |

원하는 경우 AS 절을 사용하여 출력 열의 이름을 지정할 수도 있습니다. 위의 예에서는 출력 테이블에 별칭 pvt를 사용했습니다.

UNPIVOT

UNPIVOT 연산자는 열을 행으로 변환하는 데 사용됩니다. 열에 데이터가 있는 테이블을 입력으로 사용하고 행에 데이터가 있는 테이블을 출력합니다.

UNPIVOT을 사용하려면 먼저 행으로 변환하려는 열을 지정해야 합니다. FOR 절을 사용하여 이를 수행할 수 있습니다. 예를 들어 다음 쿼리는 East, West, North 및 South 열을 행으로 변환합니다.

```sql
SELECT *
FROM mytable
UNPIVOT (
  Sales
  FOR Region IN ('East', 'West', 'North', 'South')
) AS upvt;
```

위의 쿼리에서 UNPIVOT에 대한 입력으로 Sales 열을 사용하고 있습니다. 또한 IN 절을 사용하여 행으로 변환하려는 값을 지정합니다.

쿼리 출력은 다음과 같습니다.

| 지역 | 영업 |
| --- | --- |
| 동쪽 | 10 |
| 웨스트 | 20 |
| 북쪽 | 30 |
| 남쪽 | 40 |

원하는 경우 AS 절을 사용하여 출력 열의 이름을 지정할 수도 있습니다. 위의 예에서는 출력 테이블에 대해 별칭 upvt를 사용했습니다.

추가 정보

PIVOT 및 UNPIVOT 연산자는 매우 강력하며 다양한 집계 및 보고 작업을 수행하는 데 사용할 수 있습니다.

PIVOT 및 UNPIVOT에 대해 자세히 알아보려면 다음 리소스를 확인하는 것이 좋습니다.

- PIVOT 및 UNPIVOT에 대한 MySQL 문서
- PIVOT 및 UNPIVOT에 대한 이 우수한 블로그 게시물
- PIVOT 및 UNPIVOT에 대한 이 스택 오버플로 답변