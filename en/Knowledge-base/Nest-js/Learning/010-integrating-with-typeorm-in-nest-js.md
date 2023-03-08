---
title: 010: Integrating with TypeORM in Nest.js
description: 
published: true
date: 2023-02-09T02:55:43.965Z
tags: 
editor: markdown
dateCreated: 2023-02-09T02:55:42.275Z
---

- [010: Integración con TypeORM en Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/010-integrating-with-typeorm-in-nest-js)
{.links-list}
- [010: 在 Nest.js 中与 TypeORM 集成***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/010-integrating-with-typeorm-in-nest-js)
{.links-list}
- [010: Nest.js에서 TypeORM과 통합***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/010-integrating-with-typeorm-in-nest-js)
{.links-list}


# Integrating with TypeORM in Nest.js

Nest.js is a framework for building Node.js applications. It is based on Express and uses TypeScript.

TypeORM is an Object Relational Mapper (ORM) for TypeScript. It enables developers to work with databases using objects and TypeScript.

In this post, we will learn how to integrate TypeORM with Nest.js.

## Prerequisites

- Node.js
- TypeScript
- Express
- TypeORM

## Installation

Install Nest.js and TypeORM using npm.

```
npm install --save @nestjs/typeorm typeorm
```

## Create a Nest.js Project

Create a new Nest.js project.

```
nest new project-name
```

## Create a TypeORM Entity

Create a TypeORM entity.

```
typeorm entity:create -n User
```

## Configure TypeORM

Create a file named ormconfig.json in the project root.

```json
{
  "type": "postgres",
  "host": "localhost",
  "port": 5432,
  "username": "postgres",
  "password": "postgres",
  "database": "test",
  "entities": ["src/**/*.entity{.ts,.js}"],
  "migrations": ["src/migration/*.{ts,js}"],
  "cli": {
    "migrationsDir": "src/migration"
  }
}
```

Replace the values in the file with your own database configuration.

## Create a Migration

Create a migration.

```
typeorm migration:create -n migration-name
```

## Update the Migration File

Update the generated migration file with the following code.

```typescript
import {MigrationInterface, QueryRunner} from "typeorm";

export class migration-name1587404060444 implements MigrationInterface {
    name = 'migration-name1587404060444'

    public async up(queryRunner: QueryRunner): Promise<void> {
    }

    public async down(queryRunner: QueryRunner): Promise<void> {
    }

}
```

## Run the Migration

Run the migration.

```
typeorm migration:run
```

## Create a TypeORM Service

Create a TypeORM service.

```
typeorm service:create -n user
```

## Update the Service File

Update the generated service file with the following code.

```typescript
import {Injectable} from '@nestjs/common';
import {InjectRepository} from '@nestjs/typeorm';
import {Repository} from 'typeorm';
import {User} from './user.entity';

@Injectable()
export class UserService {
  constructor(
    @InjectRepository(User)
    private readonly userRepository: Repository<User>,
  ) {}

  async findAll(): Promise<User[]> {
    return await this.userRepository.find();
  }

  async findOne(id: number): Promise<User> {
    return await this.userRepository.findOne(id);
  }

  async create(user: User): Promise<User> {
    return await this.userRepository.save(user);
  }

  async update(id: number, user: User): Promise<User> {
    return await this.userRepository.update(id, user);
  }

  async delete(id: number): Promise<User> {
    return await this.userRepository.delete(id);
  }
}
```

## Create a Controller

Create a controller.

```
typeorm controller:create -n user
```

## Update the Controller File

Update the generated controller file with the following code.

```typescript
import {Controller, Get, Param, Post, Body, Put, Delete} from '@nestjs/common';
import {UserService} from './user.service';
import {User} from './user.entity';

@Controller('user')
export class UserController {
  constructor(private readonly userService: UserService) {}

  @Get()
  async findAll(): Promise<User[]> {
    return await this.userService.findAll();
  }

  @Get(':id')
  async findOne(@Param('id') id: number): Promise<User> {
    return await this.userService.findOne(id);
  }

  @Post()
  async create(@Body() user: User): Promise<User> {
    return await this.userService.create(user);
  }

  @Put(':id')
  async update(@Param('id') id: number, @Body() user: User): Promise<User> {
    return await this.userService.update(id, user);
  }

  @Delete(':id')
  async delete(@Param('id') id: number): Promise<User> {
    return await this.userService.delete(id);
  }
}
```

## Register the Controller

Register the controller in the Nest.js module.

```typescript
import {Module} from '@nestjs/common';
import {TypeOrmModule} from '@nestjs/typeorm';
import {UserController} from './user.controller';
import {UserService} from './user.service';
import {User} from './user.entity';

@Module({
  imports: [TypeOrmModule.forFeature([User])],
  controllers: [UserController],
  providers: [UserService],
})
export class UserModule {}
```

## Start the Nest.js Application

Start the Nest.js application.

```
nest start
```

## Conclusion

In this post, we have learned how to integrate TypeORM with Nest.js.