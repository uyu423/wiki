---
title: MongoDB 인덱싱: 더 빠른 쿼리를 위한 팁 및 모범 사례
description: 
published: true
date: 2023-03-11T09:32:41.361Z
tags: 
editor: markdown
dateCreated: 2023-03-11T09:32:41.361Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [MongoDB Indexing: Tips and Best Practices for Faster Queries***English** document is available*](/en/Knowledge-base/NoSQL/mongodb-indexing-tips-and-best-practices-for-faster-queries)
{.links-list}

MongoDB 인덱싱: 더 빠른 쿼리를 위한 팁 및 모범 사례

데이터가 증가함에 따라 더 빠른 성능을 위해 쿼리를 최적화하는 것이 점점 더 중요해지고 있습니다. 널리 사용되는 NoSQL 데이터베이스인 MongoDB는 쿼리 실행 시간을 개선하는 방법으로 인덱싱을 제공합니다. 인덱싱은 더 빠른 데이터 검색을 가능하게 하는 데이터 구조인 인덱스를 만드는 프로세스입니다. 이 기사에서는 쿼리 성능을 개선하고 응답 시간을 줄이는 데 도움이 되는 MongoDB 인덱싱에 대한 팁과 모범 사례를 살펴봅니다.

## MongoDB의 인덱싱 이해

MongoDB 인덱싱 팁과 모범 사례를 살펴보기 전에 잠시 MongoDB의 인덱싱을 이해해 보겠습니다. MongoDB는 B-tree 데이터 구조를 사용하여 인덱스를 저장하고 관리합니다. 이 트리 구조는 인덱스의 키 순서에 따라 데이터에 대한 빠른 액세스를 제공합니다. MongoDB는 다음과 같은 다양한 유형의 인덱스를 지원합니다.

- 단일 필드 인덱스: 이 인덱스는 컬렉션의 단일 필드에 생성됩니다.
- 복합 색인: 이 색인은 컬렉션의 여러 필드에서 생성됩니다.
- 다중 키 인덱스: 이 인덱스는 컬렉션의 필드에 값 배열이 포함될 때 생성됩니다.
- 텍스트 인덱스: 이 인덱스는 텍스트 검색을 가능하게 하기 위해 텍스트 필드에 생성됩니다.

## MongoDB 인덱싱 팁 및 모범 사례

다음은 MongoDB 인덱싱을 사용할 때 따라야 할 몇 가지 팁과 모범 사례입니다.

### 1. 쿼리한 내용만 인덱싱

자주 쿼리되지 않는 필드에 인덱스를 만들면 리소스가 낭비되고 쓰기 성능이 느려질 수 있습니다. 따라서 쿼리하는 항목만 인덱싱하는 것이 중요합니다. 쿼리를 분석하여 자주 쿼리되는 필드를 식별하고 해당 필드에 대한 인덱스를 만듭니다.

### 2. 많은 양의 데이터 인덱싱 방지

큰 필드 또는 컬렉션에 인덱스를 생성하면 쓰기 성능이 느려지고 스토리지 요구 사항이 증가할 수 있습니다. 따라서 많은 양의 데이터를 인덱싱하지 않는 것이 중요합니다. 데이터를 분석하여 자주 쿼리되는 필드를 식별하고 해당 필드에 대한 인덱스를 만듭니다.

### 3. 정렬 및 집계에 인덱스 사용

인덱스는 데이터 정렬 및 집계에도 사용할 수 있습니다. MongoDB에서 인덱스는 정렬 및 그룹화 작업 속도를 높이는 데 사용됩니다. 쿼리를 분석하여 정렬 및 그룹화에 자주 사용되는 필드를 식별하고 해당 필드에 대한 인덱스를 만듭니다.

### 4. 커버드 쿼리 사용

포함된 쿼리는 인덱스를 사용하여 완전히 충족될 수 있고 MongoDB가 컬렉션의 실제 문서에 액세스할 필요가 없는 쿼리입니다. 포함된 쿼리는 디스크에서 읽어야 하는 데이터의 양을 줄임으로써 쿼리 성능을 향상시키는 데 도움이 될 수 있습니다. 쿼리를 분석하여 자주 사용되는 필드를 식별하고 해당 필드에 적용되는 쿼리를 만듭니다.

### 5. 인덱스 사용 모니터링

인덱스 사용량을 모니터링하면 사용되지 않거나 충분히 활용되지 않는 인덱스를 식별하는 데 도움이 됩니다. 사용하지 않는 인덱스를 삭제하여 스토리지 공간을 확보하고 쓰기 성능을 향상시킬 수 있습니다. 쿼리를 분석하여 자주 사용되는 필드를 식별하고 해당 필드에 대한 인덱스를 만듭니다.

## 코드 예제

다음은 MongoDB 인덱싱 팁과 모범 사례를 보여주는 몇 가지 코드 예제입니다.

### 1. 쿼리한 내용만 인덱싱

```javascript
db.customers.createIndex({firstName:1, lastName:1});
```

### 2. 많은 양의 데이터 인덱싱 방지

```javascript
db.orders.createIndex({status:1});
```

### 3. 정렬 및 집계에 인덱스 사용

```javascript
db.customers.createIndex({orderDate:-1});
```

### 4. 커버드 쿼리 사용

```javascript
db.customers.find({firstName:"John"}, {orderDate:1, _id:0}).sort({orderDate:-1});
```

### 5. 인덱스 사용 모니터링

```javascript
db.customers.aggregate([{$indexStats:{}}]);
```

## 결론

결론적으로 MongoDB 인덱싱은 쿼리 성능을 향상시키고 응답 시간을 줄이는 데 도움이 되는 중요한 기능입니다. 이러한 팁과 모범 사례를 따르면 쿼리를 최적화하고 MongoDB 인덱싱을 최대한 활용할 수 있습니다. 쿼리하는 항목만 인덱싱하고, 많은 양의 데이터 인덱싱을 피하고, 정렬 및 집계에 인덱스를 사용하고, 적용 쿼리를 사용하고, 인덱스 사용을 모니터링해야 합니다. 이렇게 하면 MongoDB 데이터베이스가 최적의 성능을 발휘하는지 확인할 수 있습니다.

## 외부 리소스

- MongoDB의 [MongoDB 인덱싱 전략](https://www.mongodb.com/blog/post/6-rules-of-thumb-for-mongodb-schema-design-part-3)
- MongoDB 설명서의 [인덱싱 및 쿼리 최적화](https://docs.mongodb.com/manual/indexes/)
- Arpit Bhayani의 [성능을 위한 인덱싱](https://www.codementor.io/@arpitbhayani/indexing-for-performance-in-mongodb-g06x0m6j5)