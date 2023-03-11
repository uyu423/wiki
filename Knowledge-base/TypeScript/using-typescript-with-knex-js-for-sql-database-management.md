---
title: SQL 데이터베이스 관리를 위해 Knex.js와 함께 TypeScript 사용
description: 
published: true
date: 2023-03-11T11:32:57.749Z
tags: 
editor: markdown
dateCreated: 2023-03-11T11:32:57.749Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Using TypeScript with Knex.js for SQL Database Management***English** document is available*](/en/Knowledge-base/TypeScript/using-typescript-with-knex-js-for-sql-database-management)
{.links-list}

## 소개

TypeScript는 JavaScript의 상위 집합인 오픈 소스 프로그래밍 언어입니다. 선택적 정적 타이핑 및 클래스 기반 객체 지향 프로그래밍을 언어에 추가하여 대규모 애플리케이션을 더 쉽게 작성하고 유지 관리할 수 있습니다. Knex.js는 SQL 쿼리 작성을 위한 유창한 인터페이스를 제공하는 Node.js용 인기 SQL 쿼리 빌더입니다. 이 기사에서는 SQL 데이터베이스 관리를 위해 Knex.js와 함께 TypeScript를 사용하는 방법을 살펴봅니다.

## Knex.js로 TypeScript 프로젝트 설정

시작하려면 새 TypeScript 프로젝트를 설정하고 TypeScript, Knex.js 및 적절한 데이터베이스 드라이버(예: PostgreSQL의 경우 `pg`)와 같은 필수 종속 항목을 설치해야 합니다.

```bash
$ mkdir my-project
$ cd my-project
$ npm init -y
$ npm install typescript knex pg
$ npx tsc --init
```

다음으로 ES6 모듈 구문을 사용하도록 TypeScript를 구성하고 TypeScript 유형을 사용하도록 Knex.js에 지시해야 합니다.

```json
// tsconfig.json
{
  "compilerOptions": {
    "module": "es6",
    "outDir": "./dist",
    "target": "es6"
  }
}
```

```typescript
// knexfile.ts
import { Config } from "knex";
import { development, production } from "./config";

const knexConfig: Record<string, Config> = {
  development: {
    client: "pg",
    connection: development.url,
    migrations: {
      directory: "./src/migrations",
    },
    seeds: {
      directory: "./src/seeds",
    },
  },
  production: {
    client: "pg",
    connection: production.url,
    migrations: {
      directory: "./dist/migrations",
    },
    seeds: {
      directory: "./dist/seeds",
    },
  },
};

export default knexConfig;
```

## TypeScript로 데이터베이스 모델 정의하기

이제 프로젝트를 설정했으므로 TypeScript를 사용하여 데이터베이스 모델을 정의할 수 있습니다. Knex.js에서 제공하는 `Knex` 인터페이스를 사용하여 데이터베이스 테이블의 모양을 정의합니다.

```typescript
// src/models/User.ts
import { Knex } from "knex";

interface User {
  id: number;
  username: string;
  email: string;
  created_at: Date;
  updated_at: Date;
}

const createTable = (knex: Knex) =>
  knex.schema.createTable("users", (table) => {
    table.increments("id").primary();
    table.string("username").notNullable();
    table.string("email").notNullable().unique();
    table.timestamps(true, true);
  });

export { User, createTable };
```

이 예에서는 `users` 테이블의 구조를 나타내는 `User` 인터페이스를 정의합니다. 또한 `Knex` 인스턴스를 사용하고 존재하지 않는 경우 `users` 테이블을 생성하는 `createTable` 함수를 정의합니다. 이 함수는 마이그레이션 스크립트에서 테이블을 생성하는 데 사용할 수 있습니다.

```typescript
// src/migrations/20220101000000_create_users.ts
import { Knex } from "knex";
import { createTable } from "../models/User";

export const up = async (knex: Knex): Promise<void> => {
  await createTable(knex);
};

export const down = async (knex: Knex): Promise<void> => {
  await knex.schema.dropTableIfExists("users");
};
```

## TypeScript 및 Knex.js로 데이터베이스 쿼리

이제 데이터베이스 모델을 정의했으므로 Knex.js를 사용하여 데이터베이스 쿼리를 시작할 수 있습니다. 유형이 안전한 방식으로 SQL 쿼리를 구성하기 위해 `Knex` 인터페이스를 사용할 수 있습니다.

```typescript
// src/repository/UserRepository.ts
import { Knex } from "knex";
import { User } from "../models/User";

class UserRepository {
  constructor(private readonly knex: Knex) {}

  async create(user: User): Promise<User> {
    const [createdUser] = await this.knex("users")
      .insert(user)
      .returning("*");
    return createdUser as User;
  }

  async findById(id: number): Promise<User | undefined> {
    const [user] = await this.knex("users").where({ id });
    return user as User | undefined;
  }

  async findByEmail(email: string): Promise<User | undefined> {
    const [user] = await this.knex("users").where({ email });
    return user as User | undefined;
  }

  async update(user: User): Promise<User> {
    const [updatedUser] = await this.knex("users")
      .where({ id: user.id })
      .update(user)
      .returning("*");
    return updatedUser as User;
  }

  async delete(id: number): Promise<void> {
    await this.knex("users").where({ id }).delete();
  }
}

export { UserRepository };
```

이 예제에서는 `User` 개체를 만들고, 찾고, 업데이트하고, 삭제하는 메서드를 제공하는 `UserRepository` 클래스를 정의합니다. `this.knex` 인스턴스를 사용하여 `users` 테이블과 상호 작용하는 SQL 쿼리를 구성합니다.

## 결론

이 기사에서는 SQL 데이터베이스 관리를 위해 Knex.js와 함께 TypeScript를 사용하는 방법을 살펴보았습니다. TypeScript 인터페이스를 사용하여 데이터베이스 모델을 정의하는 방법과 'Knex' 인터페이스를 사용하여 유형이 안전한 SQL 쿼리를 구성하는 방법을 살펴보았습니다. 또한 데이터베이스 작업을 캡슐화하기 위해 리포지토리 클래스를 만드는 방법도 살펴보았습니다. Knex.js와 함께 TypeScript를 사용하면 보다 유지 관리 및 확장 가능한 데이터베이스 코드를 작성할 수 있습니다.

## 외부 리소스

- [TypeScript 설명서](https://www.typescriptlang.org/docs/)
- [Knex.js 문서](https://knexjs.org/)
- [TypeORM](https://typeorm.io/) - TypeScript를 지원하는 ORM(Object-Relational Mapper)
- [Sequelize](https://sequelize.org/) - TypeScript를 지원하는 Node.js용 ORM