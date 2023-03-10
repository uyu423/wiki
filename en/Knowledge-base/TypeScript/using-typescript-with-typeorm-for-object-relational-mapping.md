---
title: Using TypeScript with TypeORM for Object-Relational Mapping
description: 
published: true
date: 2023-03-10T12:32:58.205Z
tags: 
editor: markdown
dateCreated: 2023-03-10T12:32:58.205Z
---

- [개체 관계형 매핑을 위해 TypeORM과 함께 TypeScript 사용***Korean** document is available*](/ko/Knowledge-base/TypeScript/using-typescript-with-typeorm-for-object-relational-mapping)
{.links-list}



Using TypeScript with TypeORM for Object-Relational Mapping

Object-relational mapping (ORM) is a technique that allows developers to map an object-oriented model to a relational database. TypeORM is a popular ORM library for TypeScript and JavaScript that uses decorators and is compatible with various databases such as MySQL, PostgreSQL, etc. In this article, we will explore how to use TypeScript with TypeORM for ORM.

## Prerequisites

Before diving into the details, there are some prerequisites that we need to install:

- Node.js and npm
- TypeScript
- TypeORM

## Installing TypeORM

To use TypeORM, we need to install it first. We can install it globally using the following command:

```npm install -g typeorm```

## Setting up a project with TypeScript and TypeORM

To set up a project with TypeScript and TypeORM, we need to create a new directory and initialize it with npm using the following command:

```npm init -y```

Then, we need to install the required dependencies. We can install the following dependencies using npm:

```npm install --save-dev typescript ts-node @types/node @types/express typeorm mysql2```

- `typescript` is required to compile TypeScript code to JavaScript.
- `ts-node` is required to run TypeScript code directly without compiling it.
- `@types/node` and `@types/express` are TypeScript definitions for Node.js and Express.
- `typeorm` is the TypeORM library.
- `mysql2` is a MySQL driver for TypeORM.

Next, we need to create a TypeScript configuration file, `tsconfig.json`, in the root directory of the project with the following content:

```json
{
    "compilerOptions": {
        "module": "commonjs",
        "esModuleInterop": true,
        "target": "es6",
        "moduleResolution": "node",
        "sourceMap": true,
        "outDir": "dist"
    },
    "include": ["src/**/*"],
    "exclude": ["node_modules"]
}
```

In this configuration, we have specified that we want to compile the TypeScript code to ES6 JavaScript, with source maps enabled and output in the `dist` directory. We have also specified that we want to include all the `.ts` files in the `src` directory and exclude the `node_modules` directory.

## Creating an Entity

In TypeORM, an entity is a TypeScript class that represents a database table. To create an entity, we need to define a class with properties that correspond to the columns in the table. We can also use decorators to specify the table name, column types, primary keys, etc.

Let's create an entity for a `User` table with the following properties:

- `id`: a unique identifier for the user.
- `username`: the username of the user.
- `password`: the password of the user.

Create a new file `User.ts` in the `src/entity` directory with the following content:

```typescript
import { Entity, PrimaryGeneratedColumn, Column } from 'typeorm';

@Entity()
export class User {
    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    username: string;

    @Column()
    password: string;
}
```

In this code, we have used the `@Entity()` decorator to specify that this class is an entity. We have also used the `@PrimaryGeneratedColumn()` decorator to specify that the `id` property is the primary key for the table, and it will be generated automatically. Similarly, we have used the `@Column()` decorator to specify that the `username` and `password` properties are columns in the table.

## Creating a Connection

To use TypeORM, we need to create a connection to the database. We can create a connection using the `createConnection()` method from the `typeorm` module.

Create a new file `index.ts` in the `src` directory with the following content:

```typescript
import "reflect-metadata";
import { createConnection } from "typeorm";
import { User } from "./entity/User";

createConnection().then(async connection => {

    console.log("Inserting a new user into the database...");
    const user = new User();
    user.username = "john_doe";
    user.password = "my_password";
    await connection.manager.save(user);
    console.log("Saved a new user with id: " + user.id);

    console.log("Loading users from the database...");
    const users = await connection.manager.find(User);
    console.log("Loaded users: ", users);

}).catch(error => console.log(error));
```

In this code, we have imported the `reflect-metadata` module, which is required to use decorators. Then, we have imported the `createConnection()` function from the `typeorm` module and the `User` class from the `entity/User.ts` module.

We have used the `createConnection()` function to create a connection to the default database. Then, we have inserted a new user into the database using the `save()` method of the connection manager. Finally, we have loaded all the users from the database using the `find()` method of the connection manager.

## Running the Application

To run the application, we need to compile the TypeScript code to JavaScript and then run the JavaScript code using `ts-node`. We can do this using the following command:

```npx ts-node src/index.ts```

This will compile the TypeScript code and run the `index.ts` file, which will insert a new user into the database and load all the users from the database.

## Conclusion

TypeScript with TypeORM is a powerful combination for ORM. With the help of decorators, we can easily create entities that map to database tables. We can also create relationships between entities, query the database using the connection manager, and perform transactions. TypeORM supports various databases and provides a simple and intuitive API.

## External resources

- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [TypeORM Documentation](https://typeorm.io/)
- [TypeORM Examples](https://github.com/typeorm/typeorm/tree/master/sample)