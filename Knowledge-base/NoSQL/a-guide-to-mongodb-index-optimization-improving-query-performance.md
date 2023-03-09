---
title: MongoDB 인덱스 최적화 가이드: 쿼리 성능 개선
description: 
published: true
date: 2023-03-09T05:32:45.903Z
tags: 
editor: markdown
dateCreated: 2023-03-09T05:32:45.903Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [A Guide to MongoDB Index Optimization: Improving Query Performance***English** document is available*](/en/Knowledge-base/NoSQL/a-guide-to-mongodb-index-optimization-improving-query-performance)
{.links-list}

MongoDB는 최신 웹 애플리케이션에서 널리 사용되는 대중적인 NoSQL 데이터베이스입니다. 데이터베이스 성능에서 가장 중요한 요소 중 하나는 인덱싱입니다. MongoDB에서 인덱스는 쿼리 성능을 크게 향상시킬 수 있지만 올바르게 최적화되지 않으면 성능 문제를 일으킬 수도 있습니다. 이 가이드는 MongoDB 인덱스의 작동 방식을 이해하는 데 도움이 되며 인덱스를 최적화하여 쿼리 성능을 개선하기 위한 실용적인 팁을 제공합니다.

## MongoDB 인덱스 이해하기

인덱스는 데이터베이스 테이블에서 데이터 검색 작업의 속도를 향상시키는 데이터 구조입니다. MongoDB는 관계형 데이터베이스에서 사용되는 인덱스와 유사한 B-트리 인덱스를 사용합니다. 각 인덱스는 특정 컬렉션에 생성되며 하나 이상의 필드로 구성됩니다. MongoDB는 기본 키(_id 필드)와 보조 필드 모두에 대한 인덱스를 생성할 수 있습니다.

MongoDB의 인덱스는 'system.indexes'라는 특수 컬렉션에 저장됩니다. 인덱스를 만들 때 MongoDB는 이 컬렉션에 인덱스 정의를 저장합니다. system.indexes 컬렉션은 MongoDB에서 자동으로 관리하며 사용자가 액세스할 수 없습니다.

## MongoDB의 인덱스 유형

MongoDB는 다음을 포함하여 여러 유형의 인덱스를 지원합니다.

### 단일 필드 인덱스

단일 필드 인덱스는 문서의 단일 필드에 생성됩니다. MongoDB에서 가장 일반적인 인덱스 유형이며 단일 필드를 필터링하거나 정렬하는 쿼리를 최적화하는 데 사용됩니다.

MongoDB에서 단일 필드 인덱스를 생성하려면 `createIndex()` 메서드를 사용할 수 있습니다.

```javascript
db.collection.createIndex({field:1})
```

### 복합 인덱스

복합 인덱스는 문서의 여러 필드에 생성됩니다. 여러 필드를 필터링하거나 정렬하는 쿼리를 최적화하는 데 사용됩니다.

MongoDB에서 복합 인덱스를 생성하려면 `createIndex()` 메서드를 사용할 수 있습니다.

```javascript
db.collection.createIndex({field1:1, field2:1})
```

### 멀티키 인덱스

다중 키 인덱스는 배열이 포함된 필드에 생성됩니다. 배열이 포함된 필드를 필터링하거나 정렬하는 쿼리를 최적화하는 데 사용됩니다.

MongoDB에서 다중 키 인덱스를 생성하려면 `createIndex()` 메서드를 사용할 수 있습니다.

```javascript
db.collection.createIndex({field:1})
```

### 지리공간 인덱스

지리 공간 인덱스는 지리 공간 데이터가 포함된 필드에 생성됩니다. 지리 공간 데이터를 필터링하거나 정렬하는 쿼리를 최적화하는 데 사용됩니다.

MongoDB에서 지리공간 인덱스를 생성하려면 `createIndex()` 메서드를 사용할 수 있습니다.

```javascript
db.collection.createIndex({location:"2d"})
```

### 텍스트 인덱스

텍스트 인덱스는 텍스트 데이터가 포함된 필드에 생성됩니다. 텍스트 데이터를 검색하는 쿼리를 최적화하는 데 사용됩니다.

MongoDB에서 텍스트 인덱스를 생성하려면 `createIndex()` 메서드를 사용할 수 있습니다.

```javascript
db.collection.createIndex({field:"text"})
```

## MongoDB의 인덱스 최적화

MongoDB에서 인덱스를 생성하는 것은 쉽지만 최대 성능을 위해 인덱스를 최적화하는 것은 어려울 수 있습니다. 다음은 MongoDB에서 인덱스를 최적화하기 위한 몇 가지 실용적인 팁입니다.

### 많은 양의 데이터를 필터링하는 쿼리에 인덱스 사용

인덱스는 많은 양의 데이터를 필터링하거나 정렬하는 데 사용될 때 가장 효과적입니다. 쿼리가 컬렉션에서 소량의 데이터만 반환하는 경우 인덱스를 사용하는 것보다 전체 컬렉션을 스캔하는 것이 더 빠를 수 있습니다.

### 가장 일반적인 쿼리에 대한 인덱스 생성

애플리케이션에서 가장 자주 실행되는 쿼리에 대한 인덱스를 만들어야 합니다. 이렇게 하면 결과를 반환하기 위해 MongoDB가 스캔해야 하는 문서 수를 최소화할 수 있습니다.

### 적용 쿼리 사용

적용 쿼리는 컬렉션에 액세스하지 않고 인덱스에서 완전히 충족될 수 있는 쿼리입니다. 포함된 쿼리는 컬렉션에 액세스해야 하는 쿼리보다 훨씬 빠릅니다.

적용 쿼리를 만들려면 쿼리 프로젝션에 필요한 모든 필드를 포함해야 합니다.

```javascript
db.collection.find({field:value},{field1:1,field2:1})
```

### 인덱스 교차 사용

인덱스 교차는 MongoDB가 쿼리를 만족시키기 위해 여러 인덱스를 사용할 수 있도록 하는 기술입니다. 쿼리에 여러 필드를 필터링하거나 정렬해야 하는 경우 유용할 수 있습니다.

MongoDB에서 인덱스 교차를 사용하려면 여러 인덱스를 만들고 `hint()` 메서드를 사용하여 MongoDB에 사용할 인덱스를 알릴 수 있습니다.

```javascript
db.collection.find({field1:value1,field2:value2}).hint({field1:1,field2:1})
```

### 스파스 인덱스 사용

스파스 인덱스는 특정 필드가 없는 문서가 많은 대규모 컬렉션이 있을 때 유용합니다. 스파스 인덱스는 디스크 공간을 절약하고 쿼리 성능을 향상시킬 수 있는 특정 필드가 포함된 문서만 인덱싱합니다.

MongoDB에서 스파스 인덱스를 생성하려면 `sparse:true` 옵션을 사용할 수 있습니다.

```javascript
db.collection.createIndex({field:1},{sparse:true})
```

### 인덱스 사용 모니터링

인덱스가 효과적으로 사용되고 있는지 확인하려면 인덱스 사용량을 모니터링해야 합니다. MongoDB는 쿼리가 실행되는 방법과 사용되는 인덱스를 확인하는 데 사용할 수 있는 `explain()` 메서드를 제공합니다.

```javascript
db.collection.find({field:value}).explain()
```

### 사용하지 않는 색인 제거

사용되지 않은 인덱스는 쓰기 작업 속도를 늦추고 디스크 공간을 소비할 수 있습니다. 주기적으로 색인을 검토하고 사용하지 않는 항목을 제거해야 합니다.

```javascript
db.collection.dropIndex({field:1})
```

## 결론

MongoDB 인덱스를 최적화하면 애플리케이션의 쿼리 성능을 크게 향상시킬 수 있습니다. 이 가이드의 팁을 따르면 인덱스를 만들고 최적화하여 성능을 최대화하고 디스크 공간 사용을 최소화할 수 있습니다. 인덱스 사용을 정기적으로 모니터링하고 사용하지 않는 인덱스는 제거해야 합니다.

## 외부 리소스

1. [MongoDB 인덱싱 전략](https://docs.mongodb.com/manual/applications/indexes/)
2. [MongoDB 인덱싱 모범 사례](https://docs.mongodb.com/manual/core/index-best-practices/)
3. [MongoDB 성능 모범 사례](https://docs.mongodb.com/manual/administration/analyzing-mongodb-performance/)