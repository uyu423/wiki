---
title: NoSQL 데이터베이스 설계: MongoDB 및 Redis에서 데이터를 모델링하는 방법
description: 
published: true
date: 2023-03-08T18:33:05.997Z
tags: 
editor: markdown
dateCreated: 2023-03-08T18:33:05.997Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [NoSQL Database Design: How to Model Data in MongoDB and Redis***English** document is available*](/en/Knowledge-base/NoSQL/nosql-database-design-how-to-model-data-in-mongodb-and-redis)
{.links-list}

NoSQL 데이터베이스 설계: MongoDB 및 Redis에서 데이터를 모델링하는 방법

NoSQL 데이터베이스는 유연성, 확장성 및 성능으로 인해 최근 몇 년 동안 인기를 얻고 있습니다. MySQL 및 PostgreSQL과 같은 기존 관계형 데이터베이스는 정형 데이터를 처리하는 데 적합하지만 NoSQL 데이터베이스는 비정형 또는 반정형 데이터를 처리하는 데 더 적합합니다. 이 기사에서는 널리 사용되는 두 가지 NoSQL 데이터베이스인 MongoDB와 Redis에 초점을 맞추고 데이터를 모델링하는 방법에 대해 설명합니다.

## 몽고디비

### 소개

MongoDB는 JSON과 유사한 문서에 데이터를 저장하는 문서 지향 NoSQL 데이터베이스입니다. 각 문서는 단일 레코드를 나타내며 다른 구조를 가질 수 있습니다. 즉, MongoDB에는 스키마가 없습니다. MongoDB는 높은 쓰기 및 읽기 처리량이 필요하고 수평 확장이 필요한 애플리케이션에 탁월한 선택입니다.

### 데이터 모델링

MongoDB에서 데이터를 모델링할 때 다음 사항을 고려해야 합니다.

- 데이터 관계: 관계형 데이터베이스와 달리 MongoDB는 테이블 조인을 지원하지 않습니다. 대신 문서 내에 관련 데이터를 포함하거나 참조를 사용할 수 있습니다. 데이터 포함은 관련 데이터가 작고 자주 함께 액세스되는 경우 훌륭한 옵션입니다. 그러나 관련 데이터가 크거나 독립적으로 액세스하는 경우 참조를 사용하는 것이 좋습니다.

- 쿼리 패턴: MongoDB에서 실행할 쿼리를 기반으로 데이터 모델을 설계해야 합니다. 이는 성능을 향상시키기 위해 가장 일반적인 쿼리에 대해 데이터 모델을 최적화해야 함을 의미합니다. 인덱스를 사용하여 쿼리 속도를 높일 수 있습니다.

- 데이터 증가: MongoDB는 빠르게 증가하는 데이터를 처리하는 데 적합합니다. 전체 스키마를 수정하지 않고도 새 필드나 하위 문서를 문서에 추가할 수 있습니다.

### 예

MongoDB에서 블로그 플랫폼을 구축한다고 가정해 보겠습니다. 우리의 데이터 모델은 `users`와 `posts`라는 두 개의 컬렉션으로 구성됩니다. 각 게시물에는 여러 댓글과 좋아요가 있을 수 있으며 각 사용자는 여러 게시물을 가질 수 있습니다.

데이터를 모델링하는 방법은 다음과 같습니다.

```javascript
// users collection
{
  _id: ObjectId("615e9bca3c0a2d0ff29a8d1a"),
  username: "john_doe",
  email: "john.doe@example.com",
  password: "$2a$10$qE8jC/1NzGTf6DhUJ0f8sO4/E4j4WOzvYmHfYJzjSgS1gKj56FSWS",
  created_at: ISODate("2021-10-07T09:00:00.000Z")
}

// posts collection
{
  _id: ObjectId("615e9c003c0a2d0ff29a8d1b"),
  title: "My First Blog Post",
  body: "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
  author_id: ObjectId("615e9bca3c0a2d0ff29a8d1a"),
  comments: [
    {
      _id: ObjectId("615e9c5d3c0a2d0ff29a8d1f"),
      text: "Great post!",
      author_id: ObjectId("615e9d8e3c0a2d0ff29a8d1c"),
      created_at: ISODate("2021-10-07T09:10:00.000Z")
    },
    {
      _id: ObjectId("615e9c6c3c0a2d0ff29a8d20"),
      text: "Thanks!",
      author_id: ObjectId("615e9bca3c0a2d0ff29a8d1a"),
      created_at: ISODate("2021-10-07T09:11:00.000Z")
    }
  ],
  likes: [
    ObjectId("615e9d8e3c0a2d0ff29a8d1c"), // user_id
    ObjectId("615e9bca3c0a2d0ff29a8d1a") // user_id
  ],
  created_at: ISODate("2021-10-07T09:05:00.000Z")
}
```

이 예에는 `users`와 `posts`라는 두 개의 컬렉션이 있습니다. 우리는 `게시물`을 `사용자`와 연결하기 위해 참조를 사용했습니다. 주석은 작고 게시물과 함께 액세스되므로 게시물 문서 내에 포함된 주석도 있습니다. 좋아요는 사용자 ID의 배열로 저장됩니다.

## 레디스

### 소개

Redis는 데이터를 메모리에 저장하는 키-값 NoSQL 데이터베이스입니다. Redis는 고속 데이터 액세스와 짧은 대기 시간이 필요한 애플리케이션에 탁월한 선택입니다. Redis는 데이터를 디스크에 저장할 수도 있습니다. 즉, 데이터를 캐시나 데이터베이스로 사용할 수 있습니다.

### 데이터 모델링

Redis에서 데이터를 모델링할 때 다음 사항을 고려해야 합니다.

- 데이터 관계: 관계형 데이터베이스와 달리 Redis는 테이블 조인을 지원하지 않습니다. 여러 키를 사용하여 데이터 간의 관계를 나타낼 수 있습니다. 집합, 목록 및 해시와 같은 데이터 구조를 사용하여 관련 데이터를 저장할 수도 있습니다.

- 쿼리 패턴: Redis에서 실행할 쿼리를 기반으로 데이터 모델을 설계해야 합니다. 이는 성능을 향상시키기 위해 가장 일반적인 쿼리에 대해 데이터 모델을 최적화해야 함을 의미합니다. 인덱스를 사용하여 쿼리 속도를 높일 수 있습니다.

- 메모리 사용량: Redis는 데이터를 메모리에 저장하므로 데이터 모델을 설계할 때 메모리 사용량을 고려해야 합니다. 데이터 샤딩 및 만료와 같은 기술을 사용하여 메모리 사용을 관리할 수 있습니다.

### 예

Redis에서 실시간 채팅 애플리케이션을 구축한다고 가정해 보겠습니다. 우리의 데이터 모델은 `users`와 `rooms`라는 두 개의 키로 구성됩니다. 각 방에는 여러 사용자와 메시지가 있을 수 있으며 각 사용자는 여러 방에 있을 수 있습니다.

데이터를 모델링하는 방법은 다음과 같습니다.

```javascript
// users key
{
  "user:1": {
    "name": "John Doe",
    "email": "john.doe@example.com"
  },
  "user:2": {
    "name": "Jane Doe",
    "email": "jane.doe@example.com"
  }
}

// rooms key
{
  "room:1": {
    "name": "Room 1",
    "users": ["user:1", "user:2"],
    "messages": [
      {
        "text": "Hello, World!",
        "user_id": "user:1",
        "created_at": "2021-10-07T09:20:00.000Z"
      },
      {
        "text": "Hi, John!",
        "user_id": "user:2",
        "created_at": "2021-10-07T09:21:00.000Z"
      }
    ]
  },
  "room:2": {
    "name": "Room 2",
    "users": ["user:1"],
    "messages": [
      {
        "text": "Hey, everyone!",
        "user_id": "user:1",
        "created_at": "2021-10-07T09:22:00.000Z"
      }
    ]
  }
}
```

이 예에서는 데이터 간의 관계를 나타내기 위해 여러 키를 사용했습니다. 방에 있는 사용자 목록을 저장하는 세트와 방에 메시지를 저장하는 목록을 사용했습니다. 또한 해시를 사용하여 사용자 데이터를 저장했습니다.

## 결론

이 기사에서는 MongoDB 및 Redis에서 데이터를 모델링하는 방법을 살펴보았습니다. 우리는 NoSQL 데이터베이스의 데이터 모델링이 기존의 관계형 데이터베이스와 다르며 데이터 관계, 쿼리 패턴, 데이터 증가 또는 메모리 사용량을 고려해야 한다는 것을 배웠습니다. 이러한 모범 사례를 따르면 실제 애플리케이션을 처리할 수 있는 효율적이고 확장 가능한 데이터 모델을 설계할 수 있습니다.

## 외부 리소스

- [MongoDB 데이터 모델링 가이드](https://docs.mongodb.com/manual/core/data-modeling-introduction/)
- [레디스 데이터 모델링](https://redis.io/topics/data-modeling)