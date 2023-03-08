---
title: 008：在 Nest.js 中使用数据库
description: 
published: true
date: 2023-02-14T19:32:39.640Z
tags: 
editor: markdown
dateCreated: 2023-02-14T19:32:37.813Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [008: Working with databases in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/008-working-with-databases-in-nest-js)
{.links-list}


# 在 Nest.js 中使用数据库

Nest.js 是一个用于构建可扩展的服务器端应用程序的 Node.js 框架。它使用 TypeScript（JavaScript 的超集），并为构建 RESTful Web 服务提供了一个强大的平台。

在这篇文章中，我们将看看如何在 Nest.js 中使用数据库。我们将涵盖以下主题：

- 连接到数据库
- 使用 Nest.js ORM
- 使用 Nest.js QueryBuilder

## 连接到数据库

在 Nest.js 中使用数据库的第一步是建立与数据库的连接。 Nest.js 支持多种数据库，包括 MySQL、PostgreSQL、MongoDB 和 SQLite。

要建立与数据库的连接，您需要创建一个数据源。 Nest.js 提供了一个 @nestjs/typeorm 包，可以轻松创建数据源。

要创建数据源，您需要安装 @nestjs/typeorm 包和数据库驱动程序。例如，如果您使用的是 MySQL，则需要安装 mysql2 包。

一旦安装了@nestjs/typeorm 和数据库驱动程序包，就可以通过从@nestjs/typeorm 包中导入 createConnection() 函数并传入数据库连接选项来创建数据源。

以下示例为 MySQL 数据库创建数据源：

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

## 使用 Nest.js ORM

一旦建立了数据源，就可以开始使用 Nest.js ORM 来处理数据库。 Nest.js ORM 基于 Active Record 模式，提供了一种使用数据库的便捷方式。

要使用 Nest.js ORM，您需要创建一个存储库。存储库是一个包含对数据库实体执行 CRUD 操作的方法的类。

要创建存储库，您需要从 @nestjs/typeorm 包中导入存储库并扩展存储库类。

以下示例为用户实体创建存储库：

```typescript
import { Repository } from '@nestjs/typeorm';

@EntityRepository(User)
export class UserRepository extends Repository<User> {}
```

拥有存储库后，您就可以开始对数据库实体执行 CRUD 操作。以下示例显示了如何通过 ID 查找用户：

```typescript
import { UserRepository } from './user.repository';

const user = await this.userRepository.findOne(1);
```

## 使用 Nest.js QueryBuilder

除了 Repository 类提供的方法外，您还可以使用 Nest.js QueryBuilder 来构造更复杂的查询。

Nest.js QueryBuilder 基于 Doctrine QueryBuilder 并提供了一种通过将方法链接在一起来构建查询的便捷方法。

要使用 QueryBuilder，您需要从 @nestjs/typeorm 包中导入 getConnection() 函数，并在连接上调用 createQueryBuilder() 函数。

以下示例显示如何使用 QueryBuilder 通过用户 ID 查找用户：

```typescript
import { getConnection } from '@nestjs/typeorm';

const user = await getConnection()
  .createQueryBuilder()
  .select('user')
  .from(User, 'user')
  .where('user.id = :id', { id: 1 })
  .getOne();
```

## 结论

在这篇文章中，我们了解了如何在 Nest.js 中使用数据库。我们涵盖了以下主题：

- 连接到数据库
- 使用 Nest.js ORM
- 使用 Nest.js QueryBuilder

如果您有兴趣了解有关 Nest.js 的更多信息，请务必查看 Nest.js 文档。