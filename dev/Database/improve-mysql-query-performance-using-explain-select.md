---
title: MySQL의 EXPLAIN SELECT를 활용한 쿼리 성능 향상
description: 
published: true
date: 2023-03-08T19:19:33.299Z
tags: database, mysql
editor: markdown
dateCreated: 2023-03-08T19:19:33.299Z
---

## EXPLAIN SELECT란?

EXPLAIN SELECT는 MySQL에서 쿼리의 실행 계획을 확인할 수 있는 명령어입니다. 이 명령어를 사용하면 쿼리가 어떻게 실행되는지, 어떤 인덱스가 사용되는지 등의 정보를 확인할 수 있습니다.

## EXPLAIN SELECT의 반환 컬럼과 의미
EXPLAIN SELECT 결과는 다음과 같은 반환 컬럼을 가집니다. 이를 예제를 통해 설명하겠습니다.

```sql
EXPLAIN SELECT *
FROM users
WHERE age > 30
ORDER BY id DESC
LIMIT 10;
```

```
id   select_type   table   partitions   type    possible_keys   key    key_len   ref   rows    filtered   Extra
1    SIMPLE        users   (NULL)       range   age_index       age    4         NULL  10000   10.00      Using where; Using index; Backward index scan

```

### id

SELECT 문에서 사용되는 SELECT 쿼리 블록의 고유 ID입니다. 여러 개의 쿼리 블록이 사용되는 경우 각각의 블록마다 ID가 할당됩니다.
  
### select_type

SELECT 쿼리의 유형을 나타냅니다. 예제에서는 "SIMPLE"으로 표시됩니다. 이는 UNION이나 서브쿼리가 없는 간단한 SELECT 문임을 나타냅니다.

### table

쿼리에서 사용되는 테이블 이름입니다. 예제에서는 "users"로 표시됩니다.

### partitions

쿼리에서 사용되는 파티션의 이름입니다. 이 예제에서는 파티션이 사용되지 않았기 때문에 "NULL"로 표시됩니다.

### type

쿼리에서 사용되는 테이블 접근 방법을 나타냅니다. 이 예제에서는 "range"으로 표시됩니다. "range"은 인덱스를 사용하여 특정 범위 내의 row를 찾는 방법입니다. 이는 WHERE 절에서 사용된 age > 30 조건에 해당하는 인덱스를 사용하고 있음을 나타냅니다.

- "ALL": 전체 테이블 스캔을 수행합니다. 가장 느린 타입으로, 가능한한 회피해야 합니다.
- "index": 인덱스를 사용합니다. 인덱스 탐색을 통해 해당 row를 찾습니다.
- "range": 인덱스의 범위를 사용합니다. 특정 범위 내의 row를 찾습니다.
- "ref": 인덱스를 참조합니다. 조인 등에서 사용됩니다.
- "eq_ref": 유일 인덱스를 참조합니다. 쿼리에서 단 하나의 row를 반환합니다.
- "const", "system": 모두 매우 빠른 타입으로, 상수 값을 사용하여 해당 row를 찾습니다.

### possible_keys	

쿼리에서 사용할 수 있는 인덱스의 목록을 나타냅니다. 이 예제에서는 "age_index"가 가능한 인덱스로 표시됩니다.

### key

쿼리에서 실제로 사용된 인덱스의 이름을 나타냅니다. 이 예제에서는 "age_index"가 사용된 인덱스로 표시됩니다. 

- "NULL": 인덱스를 사용하지 않았음을 나타냅니다.
- "PRIMARY": PRIMARY KEY 인덱스를 사용했습니다.
- "index_name": index_name에 해당하는 인덱스를 사용했습니다.

### key_len

사용된 인덱스의 길이를 나타냅니다. 이 예제에서는 "4"로 표시됩니다. 이는 age 컬럼이 INT(11) 데이터 타입이므로 4바이트임을 나타냅니다.

### ref

인덱스와 비교하는 열의 이름을 나타냅니다. 이 예제에서는 "const"로 표시됩니다. 이는 age > 30 조건이 상수 값임을 나타냅니다. 

### rows

쿼리에서 반환되는 row의 수를 나타냅니다. 이 예제에서는 "10"으로 표시됩니다. LIMIT 10으로 설정되어 있기 때문입니다.

### filtered

쿼리에서 필터링된 데이터의 비율을 나타냅니다. 이 예제에서는 "100.00"으로 표시됩니다. WHERE 절에서 age > 30 조건을 사용하고 있으므로, 전체 row 수에 대한 필터링된 row 수의 비율이 100%이기 때문입니다.

### Extra

쿼리의 실행 계획에서 추가 정보를 제공합니다. 이 예제에서는 "Using where; Using index; Backward index scan"으로 표시됩니다. "Using where"는 WHERE 절을 사용했음을 나타냅니다. "Using index"는 인덱스를 사용했음을 나타냅니다. "Backward index scan"은 역방향 인덱스 스캔을 사용했음을 나타냅니다. 이는 ORDER BY 절에서 id DESC를 사용하고 있기 때문입니다.

- "Using index": 인덱스를 사용했음을 나타냅니다. 이 값이 표시되면 쿼리의 성능이 향상될 가능성이 높습니다.
- "Using where": WHERE 절을 사용했음을 나타냅니다. 이 값이 표시되면 쿼리의 성능이 향상될 가능성이 있습니다.
- "Using temporary": 임시 테이블을 사용했음을 나타냅니다. 이 값이 표시되면 쿼리의 성능이 저하될 가능성이 있습니다.
- "Using filesort": 파일 정렬을 사용했음을 나타냅니다. 이 값이 표시되면 쿼리의 성능이 저하될 가능성이 있습니다.
- "Using join buffer": 조인 버퍼를 사용했음을 나타냅니다. 이 값이 표시되면 쿼리의 성능이 향상될 가능성이 있습니다.
- "Impossible where": WHERE 절에 지원되지 않는 조건이 사용되었음을 나타냅니다. 이 값이 표시되면 쿼리의 성능이 저하될 가능성이 높습니다.
- "Select tables optimized away": 쿼리의 결과를 얻기 위해 테이블이 선택되지 않았음을 나타냅니다. 이 값이 표시되면 쿼리의 성능이 향상될 가능성이 있습니다.

## 쿼리 성능을 향상시키기 위한 방법

EXPLAIN SELECT 결과를 바탕으로 쿼리 성능을 향상시키기 위해 다음과 같은 방법을 고려할 수 있습니다.

### 1. 인덱스를 추가하거나 변경하기

EXPLAIN SELECT에서 type 값이 "ALL"인 경우, 전체 테이블 스캔을 수행하고 있습니다. 이 경우 인덱스를 추가하거나 변경하여 인덱스 스캔을 통해 데이터를 더 빠르게 가져올 수 있습니다.

예를 들어, 위 예제에서는 age 컬럼에 대한 인덱스가 이미 생성되어 있습니다. 하지만, 다른 필드를 사용하는 쿼리에서는 인덱스를 추가해야 할 수도 있습니다.

### 2. WHERE 절을 최적화하기
 
WHERE 절에서 사용되는 조건을 최적화하여 반환되는 row의 수를 줄일 수 있습니다. 이를 통해 쿼리 실행 시간을 단축할 수 있습니다.

예를 들어, 위 예제에서는 age > 30 조건을 사용하고 있습니다. 이 조건은 인덱스를 사용하여 row를 찾고 있기 때문에, WHERE 절에서 사용되는 조건을 최적화하여 인덱스를 효과적으로 활용할 수 있도록 할 수 있습니다.

### 3. ORDER BY 절을 최적화하기
ORDER BY 절에서는 인덱스를 최대한 활용하도록 인덱스 스캔 방향을 변경할 수 있습니다. 이를 통해 쿼리 실행 시간을 단축할 수 있습니다.

예를 들어, 위 예제에서는 id DESC를 사용하고 있습니다. 이 경우, 인덱스의 역방향 스캔을 사용하여 데이터를 가져올 수 있습니다.

### 4. LIMIT 절을 추가하기
반환되는 row의 수를 제한하는 LIMIT 절을 추가하여 쿼리 실행 시간을 단축할 수 있습니다.

위 예제에서는 LIMIT 10으로 설정되어 있기 때문에, 최대 10개의 row만 반환됩니다. LIMIT 절을 사용하지 않은 경우, 전체 row를 가져와야 하기 때문에 쿼리 실행 시간이 더 오래 걸릴 수 있습니다.

> EXPLAIN SELECT 결과는 쿼리 실행 계획을 분석하는 데 유용하지만, 항상 정확하지는 않습니다.
> 예를 들어, MySQL Optimizer는 실제 쿼리 실행 전에 EXPLAIN SELECT 결과를 생성하며, 이 결과는 인덱스 통계, 쿼리 캐시, 시스템 부하 등의 요인에 따라 달라질 수 있습니다.
> 따라서, EXPLAIN SELECT 결과를 완벽하게 이해하고 분석하기 위해서는 쿼리 실행 계획을 다양한 상황에서 확인해보는 것이 좋습니다.
{.is-warning}

![mysql-logo.png](/mysql-logo.png){.align-center}
