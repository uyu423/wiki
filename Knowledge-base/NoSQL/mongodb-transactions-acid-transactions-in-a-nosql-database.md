---
title: MongoDB 트랜잭션: NoSQL 데이터베이스의 ACID 트랜잭션
description: 
published: true
date: 2023-03-10T20:32:34.589Z
tags: 
editor: markdown
dateCreated: 2023-03-10T20:32:34.589Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [MongoDB Transactions: ACID Transactions in a NoSQL Database***English** document is available*](/en/Knowledge-base/NoSQL/mongodb-transactions-acid-transactions-in-a-nosql-database)
{.links-list}

MongoDB 트랜잭션: NoSQL 데이터베이스의 ACID 트랜잭션

MongoDB는 높은 확장성과 유연성을 제공하는 널리 사용되는 NoSQL 데이터베이스입니다. 그러나 NoSQL 데이터베이스의 중요한 단점 중 하나는 ACID(Atomicity, Consistency, Isolation, Durability) 트랜잭션에 대한 지원이 부족하다는 것입니다. 버전 4.0에 도입된 MongoDB 트랜잭션은 이 문제에 대한 솔루션을 제공합니다. 이 기사에서는 MongoDB 트랜잭션, 해당 속성 및 사용 방법에 대해 설명합니다.

### ACID 거래란 무엇인가요?

ACID 트랜잭션은 데이터베이스 안정성과 일관성을 보장하는 속성 집합입니다. 원자성은 트랜잭션이 완전히 완료되거나 완전히 롤백되도록 보장하고, 일관성은 데이터베이스가 트랜잭션 전후에 일관성을 유지하도록 보장하고, 격리는 여러 트랜잭션이 서로 영향을 주지 않고 동시에 실행할 수 있도록 보장하며, 내구성은 트랜잭션이 커밋되면 시스템 오류가 발생한 경우에도 커밋된 상태로 유지됩니다.

### MongoDB 트랜잭션이란 무엇입니까?

MongoDB 트랜잭션은 NoSQL 데이터베이스에서 ACID 속성을 제공합니다. 여러 쓰기 작업을 트랜잭션으로 그룹화하고 단일 단위로 완전히 커밋하거나 완전히 롤백할 수 있습니다. MongoDB 트랜잭션은 복제 세트 및 샤드 클러스터와 함께 사용할 수 있으며 분산 환경에서도 사용할 수 있습니다.

### MongoDB 트랜잭션의 속성

MongoDB 트랜잭션에는 다음 속성이 있습니다.

- 원자성: 트랜잭션 내의 모든 쓰기 작업은 그룹화되어 단일 단위로 실행됩니다. 트랜잭션 내의 작업이 실패하면 전체 트랜잭션이 롤백되고 데이터베이스가 이전 상태로 돌아갑니다.
- 일관성: MongoDB 트랜잭션은 스냅샷 격리를 제공합니다. 즉, 각 트랜잭션은 특정 시점에서 데이터베이스의 일관된 보기를 볼 수 있습니다. 이렇게 하면 데이터베이스가 트랜잭션 전후에 일관성을 유지할 수 있습니다.
- 격리: MongoDB 트랜잭션은 다중 버전 동시성 제어(MVCC)를 사용하여 여러 트랜잭션이 서로 영향을 주지 않고 동시에 실행될 수 있도록 합니다. 각 트랜잭션은 특정 시점에서 데이터베이스의 일관된 스냅샷을 봅니다.
- 지속성: 트랜잭션이 커밋되면 시스템 장애가 발생하더라도 커밋된 상태를 유지합니다.

### MongoDB 트랜잭션 사용 방법

MongoDB 트랜잭션은 MongoDB 서버와의 연결을 시작하고 유지하는 데 사용되는 세션과 함께 사용할 수 있습니다. 세션은 여러 작업을 트랜잭션으로 그룹화하는 데 사용됩니다.

트랜잭션을 시작하려면 세션을 생성한 다음 해당 세션에서 트랜잭션을 시작해야 합니다. 다음은 MongoDB Node.js 드라이버를 사용하여 트랜잭션을 시작하는 방법의 예입니다.

```
const session = client.startSession();
try {
  session.startTransaction();
  // Perform write operations here
  await session.commitTransaction();
} catch (error) {
  await session.abortTransaction();
} finally {
  session.endSession();
}
```

이 예제에서는 MongoDB Node.js 드라이버의 `startSession` 메소드를 사용하여 세션을 생성합니다. 그런 다음 `startTransaction` 메서드를 사용하여 세션에서 트랜잭션을 시작합니다. 트랜잭션 내에서 데이터베이스에 대한 모든 쓰기 작업을 수행할 수 있습니다. 쓰기 작업 중 하나라도 실패하면 오류를 포착하고 `abortTransaction` 메서드를 사용하여 트랜잭션을 중단합니다. 모든 쓰기 작업이 성공하면 `commitTransaction` 메서드를 사용하여 트랜잭션을 커밋합니다. 마지막으로 `endSession` 메서드를 사용하여 세션을 종료합니다.

### 결론

MongoDB 트랜잭션은 NoSQL 데이터베이스에서 ACID 속성을 제공하므로 보다 복잡하고 안정적인 애플리케이션을 만들 수 있습니다. MongoDB 트랜잭션에는 원자성, 일관성, 격리 및 내구성 속성이 있으며 세션과 함께 사용하여 여러 쓰기 작업을 트랜잭션으로 그룹화할 수 있습니다. MongoDB 트랜잭션을 사용하면 분산 환경에서도 데이터를 안정적이고 일관되게 유지할 수 있습니다.

### 추가 정보

- MongoDB 트랜잭션 문서: https://docs.mongodb.com/manual/core/transactions/
- MongoDB Node.js 드라이버 설명서: https://mongodb.github.io/node-mongodb-native/
- MongoDB 트랜잭션: 알아야 할 모든 것: https://www.mongodb.com/blog/post/mongodb-transactions-everything-you-need-to-know