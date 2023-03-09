---
title: MongoDB 집계 성능: 속도를 위한 복잡한 쿼리 최적화
description: 
published: true
date: 2023-03-09T10:32:51.490Z
tags: 
editor: markdown
dateCreated: 2023-03-09T10:32:51.490Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [MongoDB Aggregation Performance: Optimizing Complex Queries for Speed***English** document is available*](/en/Knowledge-base/NoSQL/mongodb-aggregation-performance-optimizing-complex-queries-for-speed)
{.links-list}

MongoDB 집계 성능: 속도를 위한 복잡한 쿼리 최적화

MongoDB의 집계는 의미 있는 통찰력을 추출하기 위해 데이터를 변환하고 그룹화하는 프로세스입니다. 개발자가 대규모 데이터 세트에서 복잡한 쿼리를 수행할 수 있도록 하는 강력한 기능입니다. 그러나 집계 쿼리의 복잡성이 증가함에 따라 이를 실행하는 데 걸리는 시간도 늘어납니다. 이 기사에서는 MongoDB에서 복잡한 집계 쿼리의 성능을 최적화하는 방법에 중점을 둘 것입니다.

집계의 기초 이해

최적화 기술에 대해 알아보기 전에 MongoDB에서 집계의 기본 사항을 이해하는 것이 중요합니다. 집계는 단계 배열을 입력으로 사용하는 MongoDB의 `aggregate()` 메서드를 사용하여 수행됩니다. 스테이지는 집계 프로세스의 한 단계를 나타내며 필터링, 그룹화, 정렬 및 프로젝션과 같은 다양한 작업을 수행할 수 있습니다.

집계 파이프라인의 각 단계에는 이와 관련된 성능 비용이 있습니다. 예를 들어 정렬 및 그룹화 작업은 특히 대규모 데이터 세트에서 비용이 많이 들 수 있습니다. 따라서 집계 쿼리의 전반적인 성능을 개선하려면 파이프라인의 단계 수와 각 단계의 복잡성을 최소화하는 것이 중요합니다.

집계 성능 최적화

1. 인덱스 사용

인덱스는 집계 성능을 최적화하는 데 중요한 구성 요소입니다. 이를 통해 MongoDB는 집계 쿼리에 필요한 데이터를 빠르게 찾고 검색할 수 있습니다. 인덱스가 없으면 MongoDB는 전체 컬렉션 스캔을 수행해야 하며 이는 대규모 데이터 세트에서 매우 느릴 수 있습니다.

집계 쿼리를 디자인할 때 쿼리에 필요한 인덱스를 고려하는 것이 중요합니다. MongoDB는 단일 필드, 복합 및 텍스트 인덱스와 같은 다양한 인덱스 유형을 지원합니다. 쿼리에 적합한 인덱스 유형을 선택하면 쿼리 성능이 크게 향상될 수 있습니다.

예를 들어 `상태`라는 필드로 문서를 그룹화하는 다음 집계 쿼리를 고려하십시오.

```javascript
db.collection.aggregate([
   { $group: { _id: "$status", count: { $sum: 1 } } }
])
```

이 쿼리를 최적화하기 위해 `status` 필드에 인덱스를 만들 수 있습니다.

```javascript
db.collection.createIndex( { status: 1 } )
```

이 인덱스를 사용하면 MongoDB가 '상태' 필드별로 문서를 빠르게 그룹화하여 상당한 성능 향상을 가져올 수 있습니다.

2. 프로젝션 사용

프로젝션은 컬렉션의 문서에서 필드 하위 집합을 선택하는 프로세스입니다. 처리해야 하는 데이터의 양을 줄이기 때문에 집계 성능을 최적화하는 데 필수적인 부분입니다.

집계 쿼리를 수행할 때 쿼리에 필요한 필드만 프로젝션하는 것이 중요합니다. 이는 집계 파이프라인의 `$project` 단계를 사용하여 달성할 수 있습니다.

예를 들어 `status` 필드로 문서를 그룹화하고 `value`라는 필드의 평균 값을 계산하는 다음 집계 쿼리를 고려하십시오.

```javascript
db.collection.aggregate([
   { $group: { _id: "$status", avgValue: { $avg: "$value" } } }
])
```

이 쿼리를 최적화하기 위해 `status` 및 `value` 필드만 프로젝션할 수 있습니다.

```javascript
db.collection.aggregate([
   { $project: { status: 1, value: 1 } },
   { $group: { _id: "$status", avgValue: { $avg: "$value" } } }
])
```

이렇게 하면 처리해야 하는 데이터 양이 줄어들어 쿼리 실행 속도가 빨라집니다.

3. 쿼리 필터 사용

쿼리 필터는 집계 쿼리 중에 처리해야 하는 데이터 양을 줄이는 또 다른 방법입니다. 이를 통해 개발자는 관련 없는 문서를 집계 파이프라인에서 처리하기 전에 필터링할 수 있습니다.

쿼리 성능을 더욱 최적화하기 위해 쿼리 필터를 인덱스와 함께 사용할 수 있습니다. 예를 들어 `상태` 필드로 문서를 그룹화하고 `값`이라는 필드의 평균 값을 계산하는 다음 집계 쿼리를 생각해 보십시오. `status` 필드가 `active`인 문서만 포함하려고 합니다.

```javascript
db.collection.aggregate([
   { $match: { status: "active" } },
   { $group: { _id: "$status", avgValue: { $avg: "$value" } } }
])
```

집계 파이프라인에 `$match` 단계를 포함하면 기준과 일치하지 않는 모든 문서를 필터링하여 쿼리 실행 속도를 높일 수 있습니다.

4. 집계 연산자를 현명하게 사용

집계 연산자는 MongoDB에서 집계 파이프라인의 빌딩 블록입니다. 이를 통해 개발자는 필터링, 그룹화, 정렬 및 프로젝션과 같은 다양한 작업을 수행할 수 있습니다.

집계 연산자를 사용할 때는 집계 쿼리의 성능을 최적화하기 위해 현명하게 사용하는 것이 중요합니다. 예를 들어 정렬 및 그룹화 작업은 특히 대규모 데이터 세트에서 비용이 많이 들 수 있습니다. 따라서 필요할 때만 사용하는 것이 중요합니다.

또한 일부 집계 연산자는 다른 것보다 비쌀 수 있습니다. 예를 들어 컬렉션 간에 왼쪽 외부 조인을 수행하는 `$lookup` 연산자는 대규모 데이터 세트에서 비용이 많이 들 수 있습니다. 따라서 필요한 경우에만 이 연산자를 사용하고 조인 조건을 신중하게 설계하여 처리해야 하는 문서 수를 최소화하는 것이 중요합니다.

결론

집계는 개발자가 대규모 데이터 세트에서 복잡한 쿼리를 수행할 수 있도록 하는 MongoDB의 강력한 기능입니다. 그러나 집계 쿼리의 복잡성이 증가함에 따라 이를 실행하는 데 걸리는 시간도 늘어납니다. 이 문서에 설명된 최적화 기술을 따르면 개발자는 집계 쿼리의 성능을 크게 향상시킬 수 있습니다.

외부 자원

- MongoDB 집계 파이프라인 최적화 모범 사례: https://www.mongodb.com/blog/post/optimizing-mongodb-aggregation-pipelines-best-practices-part-1
- MongoDB 집계 성능 최적화: https://scalegrid.io/blog/mongodb-aggregation-performance-optimization/
- MongoDB 집계 프레임워크: https://docs.mongodb.com/manual/aggregation/