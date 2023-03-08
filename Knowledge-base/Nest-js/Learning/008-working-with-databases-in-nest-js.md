---
title: 008: Nest.js에서 데이터베이스 작업
description: 
published: true
date: 2023-02-14T19:32:39.660Z
tags: 
editor: markdown
dateCreated: 2023-02-14T19:32:37.814Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [008: Working with databases in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/008-working-with-databases-in-nest-js)
{.links-list}


# Nest.js에서 데이터베이스 작업하기

Nest.js는 확장 가능한 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. JavaScript의 상위 집합인 TypeScript를 사용하며 RESTful 웹 서비스를 구축하기 위한 강력한 플랫폼을 제공합니다.

이 게시물에서는 Nest.js에서 데이터베이스로 작업하는 방법을 살펴보겠습니다. 다음 주제를 다룹니다.

- 데이터베이스에 연결
- Nest.js ORM 사용
- Nest.js QueryBuilder 사용

## 데이터베이스에 연결

Nest.js에서 데이터베이스 작업의 첫 번째 단계는 데이터베이스에 대한 연결을 설정하는 것입니다. Nest.js는 MySQL, PostgreSQL, MongoDB 및 SQLite를 포함한 다양한 데이터베이스를 지원합니다.

데이터베이스에 대한 연결을 설정하려면 데이터 소스를 생성해야 합니다. Nest.js는 데이터 소스를 쉽게 생성할 수 있는 @nestjs/typeorm 패키지를 제공합니다.

데이터 소스를 생성하려면 @nestjs/typeorm 패키지와 데이터베이스용 드라이버를 설치해야 합니다. 예를 들어 MySQL을 사용하는 경우 mysql2 패키지를 설치해야 합니다.

@nestjs/typeorm 및 데이터베이스 드라이버 패키지가 설치되면 @nestjs/typeorm 패키지에서 createConnection() 함수를 가져오고 데이터베이스 연결 옵션을 전달하여 데이터 소스를 생성할 수 있습니다.

다음 예제에서는 MySQL 데이터베이스에 대한 데이터 소스를 생성합니다.

```typescript
import { createConnection } from '@nestjs/typeorm';

createConnection({
  type: 'mysql',
  host: 'localhost',
  port: 3306,
  username: 'root',
  password: 'password',
  database: 'database',
  entities: [],
  synchronize: true,
});
```

## Nest.js ORM 사용

데이터 소스가 설정되면 Nest.js ORM을 사용하여 데이터베이스 작업을 시작할 수 있습니다. Nest.js ORM은 활성 레코드 패턴을 기반으로 하며 데이터베이스 작업을 위한 편리한 방법을 제공합니다.

Nest.js ORM을 사용하려면 저장소를 만들어야 합니다. 리포지토리는 데이터베이스 엔터티에서 CRUD 작업을 수행하기 위한 메서드를 포함하는 클래스입니다.

리포지토리를 생성하려면 @nestjs/typeorm 패키지에서 리포지토리를 가져와 리포지토리 클래스를 확장해야 합니다.

다음 예제에서는 사용자 엔터티에 대한 리포지토리를 만듭니다.

```typescript
import { Repository } from '@nestjs/typeorm';

@EntityRepository(User)
export class UserRepository extends Repository<User> {}
```

리포지토리가 있으면 데이터베이스 엔터티에서 CRUD 작업을 시작할 수 있습니다. 다음 예에서는 ID로 사용자를 찾는 방법을 보여줍니다.

```typescript
import { UserRepository } from './user.repository';

const user = await this.userRepository.findOne(1);
```

## Nest.js QueryBuilder 사용

Repository 클래스에서 제공하는 메서드 외에도 Nest.js QueryBuilder를 사용하여 더 복잡한 쿼리를 구성할 수 있습니다.

Nest.js QueryBuilder는 Doctrine QueryBuilder를 기반으로 하며 메서드를 함께 연결하여 쿼리를 작성하는 편리한 방법을 제공합니다.

QueryBuilder를 사용하려면 @nestjs/typeorm 패키지에서 getConnection() 함수를 가져와 연결에서 createQueryBuilder() 함수를 호출해야 합니다.

다음 예는 QueryBuilder를 사용하여 ID로 사용자를 찾는 방법을 보여줍니다.

```typescript
import { getConnection } from '@nestjs/typeorm';

const user = await getConnection()
  .createQueryBuilder()
  .select('user')
  .from(User, 'user')
  .where('user.id = :id', { id: 1 })
  .getOne();
```

## 결론

이 게시물에서는 Nest.js에서 데이터베이스로 작업하는 방법을 살펴보았습니다. 우리는 다음 주제를 다루었습니다.

- 데이터베이스에 연결
- Nest.js ORM 사용
- Nest.js QueryBuilder 사용

Nest.js에 대해 자세히 알아보려면 Nest.js 문서를 확인하세요.