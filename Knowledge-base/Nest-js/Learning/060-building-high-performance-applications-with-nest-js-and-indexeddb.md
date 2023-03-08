---
title: 060: Nest.js 및 IndexedDB로 고성능 애플리케이션 구축
description: 
published: true
date: 2023-02-08T23:55:36.099Z
tags: 
editor: markdown
dateCreated: 2023-02-08T23:55:30.106Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [060: Building high-performance applications with Nest.js and IndexedDB***English** document is available*](/en/Knowledge-base/Nest-js/Learning/060-building-high-performance-applications-with-nest-js-and-indexeddb)
{.links-list}


# 소개

이 게시물에서는 Nest.js 및 IndexedDB를 사용하여 고성능 애플리케이션을 구축하는 방법을 살펴보겠습니다.

다음 주제를 다룹니다.

- Nest.js가 무엇인가요?
- IndexedDB란?
- Nest.js와 IndexedDB를 함께 사용하는 이유는 무엇입니까?
- Nest.js 및 IndexedDB를 사용하여 고성능 애플리케이션을 구축하는 방법.

# Nest.js가 무엇인가요?

Nest.js는 확장 가능한 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. Angular에서 크게 영감을 받았으며 TypeScript를 사용합니다.

Nest.js는 고성능 애플리케이션을 구축하기 위한 탁월한 선택입니다. 사용하기 쉽고 다양한 기능이 있습니다.

# IndexedDB란?

IndexedDB는 JavaScript 기반의 객체 지향 데이터베이스입니다. 이는 데이터가 개체에 저장되고 트랜잭션이 데이터를 조작하는 데 사용됨을 의미하는 트랜잭션 데이터베이스입니다.

IndexedDB는 사용하기 쉽고 다양한 기능을 갖추고 있기 때문에 고성능 애플리케이션을 구축하는 데 탁월한 선택입니다.

# 왜 Nest.js와 IndexedDB를 함께 사용하나요?

Nest.js와 IndexedDB는 모두 고성능 애플리케이션을 구축하기 위한 훌륭한 선택입니다. Nest.js는 확장 가능한 서버측 애플리케이션 구축에 탁월한 선택이며 IndexedDB는 트랜잭션 데이터베이스 구축에 탁월한 선택입니다.

Nest.js와 IndexedDB는 모두 사용하기 쉽고 다양한 기능을 제공합니다. Nest.js는 Angular에서 크게 영감을 받았으며 TypeScript를 사용합니다. IndexedDB는 JavaScript 기반의 객체 지향 데이터베이스입니다.

Nest.js와 IndexedDB는 모두 고성능 애플리케이션을 구축하기 위한 훌륭한 선택입니다.

# Nest.js 및 IndexedDB를 사용하여 고성능 애플리케이션을 구축하는 방법.

이 섹션에서는 Nest.js 및 IndexedDB를 사용하여 고성능 애플리케이션을 구축하는 방법을 살펴보겠습니다.

다음 주제를 다룹니다.

- Nest.js 애플리케이션을 만드는 방법.
- IndexedDB 데이터베이스에 연결하는 방법.
- 트랜잭션 데이터베이스를 만드는 방법.
- IndexedDB 데이터베이스에서 데이터를 조작하는 방법.

## Nest.js 애플리케이션을 만드는 방법.

Nest.js 애플리케이션을 만들려면 Nest.js CLI를 설치해야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
npm install -g @nestjs/cli
```

Nest.js CLI가 설치되면 다음 명령을 실행하여 새 Nest.js 애플리케이션을 만들 수 있습니다.

```
nest new my-nestjs-app
```

이렇게 하면 my-nestjs-app이라는 디렉토리에 새로운 Nest.js 애플리케이션이 생성됩니다.

## IndexedDB 데이터베이스에 연결하는 방법.

IndexedDB 데이터베이스에 연결하려면 IndexedDB 드라이버를 설치해야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
npm install indexeddb-js
```

IndexedDB 드라이버가 설치되면 다음 명령을 실행하여 IndexedDB 데이터베이스에 연결할 수 있습니다.

```
nest connect my-nestjs-app my-indexeddb-database
```

그러면 my-indexeddb-database라는 IndexedDB 데이터베이스에 연결됩니다.

## 트랜잭션 데이터베이스를 만드는 방법.

트랜잭션 데이터베이스를 생성하려면 IndexedDB 드라이버를 설치해야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
npm install indexeddb-js
```

IndexedDB 드라이버가 설치되면 다음 명령을 실행하여 트랜잭션 데이터베이스를 생성할 수 있습니다.

```
nest create-database my-nestjs-app my-indexeddb-database
```

이렇게 하면 my-indexeddb-database라는 트랜잭션 데이터베이스가 생성됩니다.

## IndexedDB 데이터베이스에서 데이터를 조작하는 방법.

IndexedDB 데이터베이스의 데이터를 조작하려면 IndexedDB 드라이버를 설치해야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
npm install indexeddb-js
```

IndexedDB 드라이버가 설치되면 다음 명령을 실행하여 IndexedDB 데이터베이스의 데이터를 조작할 수 있습니다.

```
nest manipulate-data my-nestjs-app my-indexeddb-database
```

이것은 my-indexeddb-database라는 IndexedDB 데이터베이스의 데이터를 조작합니다.