---
title: 008: Working with databases in Nest.js
description: 
published: true
date: 2023-02-14T19:32:45.431Z
tags: 
editor: markdown
dateCreated: 2023-02-14T19:32:37.818Z
---

- [008: Trabajar con bases de datos en Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/008-working-with-databases-in-nest-js)
{.links-list}
- [008：在 Nest.js 中使用数据库***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/008-working-with-databases-in-nest-js)
{.links-list}
- [008: Nest.js에서 데이터베이스 작업***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/008-working-with-databases-in-nest-js)
{.links-list}


# Working with databases in Nest.js

Nest.js is a Node.js framework for building scalable server-side applications. It uses TypeScript, a superset of JavaScript, and provides a powerful platform for building RESTful web services.

In this post, we'll take a look at how to work with databases in Nest.js. We'll cover the following topics:

- Connecting to a database
- Using the Nest.js ORM
- Using the Nest.js QueryBuilder

## Connecting to a database

The first step in working with databases in Nest.js is to establish a connection to the database. Nest.js supports a variety of databases, including MySQL, PostgreSQL, MongoDB, and SQLite.

To establish a connection to a database, you'll need to create a datasource. Nest.js provides a @nestjs/typeorm package that makes it easy to create datasources.

To create a datasource, you'll need to install the @nestjs/typeorm package and the driver for your database. For example, if you're using MySQL, you'll need to install the mysql2 package.

Once you have the @nestjs/typeorm and database driver packages installed, you can create a datasource by importing the createConnection() function from the @nestjs/typeorm package and passing in the options for your database connection.

The following example creates a datasource for a MySQL database:

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

## Using the Nest.js ORM

Once you have a datasource established, you can start using the Nest.js ORM to work with your database. The Nest.js ORM is based on the Active Record pattern and provides a convenient way to work with your database.

To use the Nest.js ORM, you'll need to create a repository. A repository is a class that contains methods for performing CRUD operations on a database entity.

To create a repository, you'll need to import the Repository from the @nestjs/typeorm package and extend the Repository class.

The following example creates a repository for a User entity:

```typescript
import { Repository } from '@nestjs/typeorm';

@EntityRepository(User)
export class UserRepository extends Repository<User> {}
```

Once you have a repository, you can start performing CRUD operations on your database entities. The following example shows how to find a user by their id:

```typescript
import { UserRepository } from './user.repository';

const user = await this.userRepository.findOne(1);
```

## Using the Nest.js QueryBuilder

In addition to the methods provided by the Repository class, you can also use the Nest.js QueryBuilder to construct more complex queries.

The Nest.js QueryBuilder is based on the Doctrine QueryBuilder and provides a convenient way to build queries by chaining together methods.

To use the QueryBuilder, you'll need to import the getConnection() function from the @nestjs/typeorm package and call the createQueryBuilder() function on the connection.

The following example shows how to use the QueryBuilder to find a user by their id:

```typescript
import { getConnection } from '@nestjs/typeorm';

const user = await getConnection()
  .createQueryBuilder()
  .select('user')
  .from(User, 'user')
  .where('user.id = :id', { id: 1 })
  .getOne();
```

## Conclusion

In this post, we've taken a look at how to work with databases in Nest.js. We've covered the following topics:

- Connecting to a database
- Using the Nest.js ORM
- Using the Nest.js QueryBuilder

If you're interested in learning more about Nest.js, be sure to check out the Nest.js documentation.