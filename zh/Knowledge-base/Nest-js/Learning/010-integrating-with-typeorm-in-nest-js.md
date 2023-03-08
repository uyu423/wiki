---
title: 010: 在 Nest.js 中与 TypeORM 集成
description: 
published: true
date: 2023-02-09T02:55:48.263Z
tags: 
editor: markdown
dateCreated: 2023-02-09T02:55:42.270Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [010: Integrating with TypeORM in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/010-integrating-with-typeorm-in-nest-js)
{.links-list}


# 在 Nest.js 中与 TypeORM 集成

Nest.js 是用于构建 Node.js 应用程序的框架。它基于 Express 并使用 TypeScript。

TypeORM 是 TypeScript 的对象关系映射器 (ORM)。它使开发人员能够使用对象和 TypeScript 处理数据库。

在这篇文章中，我们将学习如何将 TypeORM 与 Nest.js 集成。

## 先决条件

- 节点.js
- 打字稿
- 表达
- 类型ORM

## 安装

使用 npm 安装 Nest.js 和 TypeORM。

```
npm install --save @nestjs/typeorm typeorm
```

## 创建一个 Nest.js 项目

创建一个新的 Nest.js 项目。

```
nest new project-name
```

## 创建一个 TypeORM 实体

创建一个 TypeORM 实体。

```
typeorm entity:create -n User
```

## 配置 TypeORM

在项目根目录中创建一个名为 ormconfig.json 的文件。

```json
{
  "type": "postgres",
  "host": "localhost",
  "port": 5432,
  "username": "postgres",
  "password": "postgres",
  "database": "test",
  "entities": ["src/**/*.entity{.links-list}"],
  "migrations": ["src/migration/*.{ts,js}"],
  "cli": {
    "migrationsDir": "src/migration"
  }
}
```

用您自己的数据库配置替换文件中的值。

## 创建迁移

创建迁移。

```
typeorm migration:create -n migration-name
```

## 更新迁移文件

使用以下代码更新生成的迁移文件。

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

## 运行迁移

运行迁移。

```
typeorm migration:run
```

## 创建一个 TypeORM 服务

创建 TypeORM 服务。

```
typeorm service:create -n user
```

## 更新服务文件

使用以下代码更新生成的服务文件。

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

## 创建控制器

创建一个控制器。

```
typeorm controller:create -n user
```

## 更新控制器文件

使用以下代码更新生成的控制器文件。

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

## 注册控制器

在 Nest.js 模块中注册控制器。

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

## 启动 Nest.js 应用程序

启动 Nest.js 应用程序。

```
nest start
```

## 结论

在这篇文章中，我们学习了如何将 TypeORM 与 Nest.js 集成。