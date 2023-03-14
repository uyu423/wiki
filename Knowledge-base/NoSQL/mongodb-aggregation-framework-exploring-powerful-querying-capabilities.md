---
title: MongoDB 집계 프레임워크: 강력한 쿼리 기능 탐색
description: 
published: true
date: 2023-03-14T04:33:35.157Z
tags: 
editor: markdown
dateCreated: 2023-03-14T04:33:35.157Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [MongoDB Aggregation Framework: Exploring Powerful Querying Capabilities***English** document is available*](/en/Knowledge-base/NoSQL/mongodb-aggregation-framework-exploring-powerful-querying-capabilities)
{.links-list}



## 소개

MongoDB는 최신 웹 애플리케이션 개발에 사용되는 가장 인기 있는 NoSQL 데이터베이스 중 하나입니다. 유연한 데이터 모델과 확장 가능한 용량을 갖춘 MongoDB는 높은 성능과 안정성이 필요한 개발자가 선호하는 선택이 되었습니다.

이 기사에서는 MongoDB Aggregation Framework에 중점을 둘 것입니다. 집계 프레임워크는 MongoDB에서 데이터를 쿼리하고 분석하기 위한 강력한 도구로, 개발자가 대규모 데이터 세트에서 복잡한 작업을 쉽게 수행할 수 있도록 합니다.

## MongoDB 집계 프레임워크가 무엇인가요?

집계 프레임워크는 개발자가 컬렉션의 문서에 대해 복잡한 집계 작업을 수행할 수 있도록 하는 MongoDB의 파이프라인 기반 데이터 처리 방법입니다. 프레임워크는 데이터를 변환하고 조작하는 데 사용할 수 있는 일련의 연산자를 제공하여 강력하고 유연한 쿼리 기능을 제공합니다.

집계 프레임워크는 여러 컬렉션의 데이터 필터링, 그룹화, 정렬 및 조인을 포함하여 광범위한 데이터 분석 작업을 수행하는 데 사용됩니다. 또한 수학적 연산, 통계 분석 및 텍스트 검색 기능을 지원합니다.

## 집계 파이프라인 분석

집계 프레임워크는 단계 파이프라인을 통해 컬렉션의 문서 집합에서 작동하며 각 단계는 하나 이상의 연산자로 구성됩니다. 각 단계의 출력은 다음 단계의 입력이 됩니다.

파이프라인은 입력 문서에서 다양한 작업을 수행하는 여러 단계로 구성됩니다. 단계는 순서대로 적용되며 각 단계의 결과는 다음 단계로 전달됩니다.

파이프라인 단계에는 다음이 포함됩니다.

- **$match**: 지정된 조건에 따라 입력 문서를 필터링합니다.
- **$project**: 입력 문서를 수정하고 출력에 포함하거나 제외할 필드를 지정합니다.
- **$group**: 지정된 키를 기준으로 입력 문서를 그룹화하고 집계 작업을 수행합니다.
- **$sort**: 지정된 정렬 순서에 따라 입력 문서를 정렬합니다.
- **$limit**: 다음 단계로 넘어가는 문서의 수를 제한합니다.
- **$skip**: 입력에서 지정된 수의 문서를 건너뛰고 나머지는 다음 단계로 넘깁니다.
- **$lookup**: 컬렉션 간에 왼쪽 외부 조인을 수행합니다.
- **$unwind**: 입력 문서에서 배열 필드를 분해하고 배열의 각 요소에 대해 하나의 문서를 출력합니다.

## 집계 작업

### $match로 데이터 필터링하기

`$match` 단계는 지정된 조건에 따라 입력 문서를 필터링합니다. 조건은 `$eq`, `$gt`, `$lt`, `$in`, `$ne`, `$and`, `$or` 등과 같은 쿼리 연산자를 사용하는 유효한 쿼리 식일 수 있습니다. .

다음 예는 `status` 필드가 "active"인 문서를 검색하기 위해 `$match` 단계를 사용하는 방법을 보여줍니다.

```javascript
db.inventory.aggregate([
   { $match : { status : "active" } }
])
```

### $project로 데이터 프로젝션

`$project` 단계는 입력 문서를 수정하고 출력에 포함하거나 제외할 필드를 지정합니다. 또한 `$addFields`, `$project` 및 `$rename` 연산자를 사용하여 새 필드를 만들거나 기존 필드의 이름을 바꿀 수 있습니다.

다음 예에서는 `$project` 단계를 사용하여 출력에 `item` 및 `qty` 필드만 포함하는 방법을 보여줍니다.

```javascript
db.inventory.aggregate([
   { $project : { item: 1, qty: 1 } }
])
```

### $group으로 데이터 그룹화

`$group` 단계는 지정된 키를 기준으로 입력 문서를 그룹화하고 그룹화된 데이터에 대한 집계 작업을 수행합니다. 집계 작업에는 `$sum`, `$avg`, `$min`, `$max`, `$first`, `$last`, `$push` 및 `$addToSet`이 포함됩니다.

다음 예는 `$group` 단계를 사용하여 `status` 필드로 문서를 그룹화하고 각 상태에 대한 총 수량을 계산하는 방법을 보여줍니다.

```javascript
db.inventory.aggregate([
   { $group : { _id : "$status", total_qty: { $sum: "$qty" } } }
])
```

### $sort로 데이터 정렬하기

`$sort` 단계는 지정된 정렬 순서에 따라 입력 문서를 정렬합니다. 정렬 순서는 오름차순(`1`) 또는 내림차순(`-1`)일 수 있습니다.

다음 예는 `$sort` 스테이지를 사용하여 `qty` 필드를 기준으로 내림차순으로 문서를 정렬하는 방법을 보여줍니다.

```javascript
db.inventory.aggregate([
   { $sort : { qty : -1 } }
])
```

### $limit로 데이터 제한

`$limit` 단계는 다음 단계로 전달되는 문서의 수를 제한합니다. 대량의 데이터를 검색하는 쿼리를 최적화하는 데 사용할 수 있습니다.

다음 예는 `$limit` 단계를 사용하여 출력을 처음 5개 문서로 제한하는 방법을 보여줍니다.

```javascript
db.inventory.aggregate([
   { $limit : 5 }
])
```

### $skip으로 데이터 건너뛰기

`$skip` 단계는 입력에서 지정된 수의 문서를 건너뛰고 나머지는 다음 단계로 전달합니다. 이미 처리된 문서를 건너뛰는 데 사용할 수 있습니다.

다음 예는 `$skip` 단계를 사용하여 입력의 처음 5개 문서를 건너뛰는 방법을 보여줍니다.

```javascript
db.inventory.aggregate([
   { $skip : 5 }
])
```

### $lookup으로 데이터 조인

`$lookup` 단계는 컬렉션 간에 왼쪽 외부 조인을 수행합니다. 공통 필드를 기반으로 여러 컬렉션의 데이터를 결합하는 데 사용할 수 있습니다.

다음 예는 `$lookup` 단계를 사용하여 `product_id` 필드를 기반으로 `products` 컬렉션과 `orders` 컬렉션을 조인하는 방법을 보여줍니다.

```javascript
db.orders.aggregate([
   {
      $lookup:
         {
           from: "products",
           localField: "product_id",
           foreignField: "_id",
           as: "product"
         }
   }
])
```

### $unwind로 데이터 풀기

`$unwind` 단계는 입력 문서의 배열 필드를 분해하고 배열의 각 요소에 대해 하나의 문서를 출력합니다. 중첩 배열을 평면화하고 배열 요소에 대한 집계 작업을 수행하는 데 사용할 수 있습니다.

다음 예제는 `$unwind` 단계를 사용하여 입력 문서에서 `sizes` 배열을 평면화하는 방법을 보여줍니다.

```javascript
db.products.aggregate([
   { $unwind : "$sizes" }
])
```

## 결론

MongoDB 집계 프레임워크는 MongoDB에서 데이터를 쿼리하고 분석하기 위한 강력한 도구입니다. 대규모 데이터 세트에서 복잡한 집계 작업을 수행하는 유연하고 효율적인 방법을 제공하여 개발자가 데이터에서 귀중한 통찰력을 얻을 수 있도록 합니다. 집계 프레임워크를 마스터함으로써 개발자는 MongoDB의 잠재력을 최대한 활용하고 강력하고 확장 가능한 애플리케이션을 구축할 수 있습니다.

## 외부 리소스

- [MongoDB 집계 파이프라인](https://docs.mongodb.com/manual/core/aggregation-pipeline/)
- [집계 참조](https://docs.mongodb.com/manual/reference/operator/aggregation/)
- [MongoDB Aggregation 소개](https://www.mongodb.com/blog/post/an-introduction-to-mongodb-aggregation-part-1-of-2)