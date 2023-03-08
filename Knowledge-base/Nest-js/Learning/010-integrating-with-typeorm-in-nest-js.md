---
title: 010: Nest.js에서 TypeORM과 통합
description: 
published: true
date: 2023-02-09T02:55:48.263Z
tags: 
editor: markdown
dateCreated: 2023-02-09T02:55:42.272Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [010: Integrating with TypeORM in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/010-integrating-with-typeorm-in-nest-js)
{.links-list}


# Nest.js에서 TypeORM과 통합

Nest.js는 Node.js 애플리케이션을 구축하기 위한 프레임워크입니다. Express를 기반으로 하며 TypeScript를 사용합니다.

TypeORM은 TypeScript용 ORM(Object Relational Mapper)입니다. 이를 통해 개발자는 개체 및 TypeScript를 사용하여 데이터베이스 작업을 할 수 있습니다.

이 게시물에서는 TypeORM을 Nest.js와 통합하는 방법을 배웁니다.

## 전제 조건

- Node.js
- 타입스크립트
- 표현하다
- 유형ORM

## 설치

npm을 사용하여 Nest.js 및 TypeORM을 설치합니다.

```
npm install --save @nestjs/typeorm typeorm
```

## Nest.js 프로젝트 생성

새 Nest.js 프로젝트를 만듭니다.

```
nest new project-name
```

## TypeORM 엔티티 생성

TypeORM 엔터티를 만듭니다.

```
typeorm entity:create -n User
```

## TypeORM 구성

프로젝트 루트에 ormconfig.json이라는 파일을 만듭니다.

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

파일의 값을 고유한 데이터베이스 구성으로 바꿉니다.

## 마이그레이션 만들기

마이그레이션을 생성합니다.

```
typeorm migration:create -n migration-name
```

## 마이그레이션 파일 업데이트

다음 코드를 사용하여 생성된 마이그레이션 파일을 업데이트합니다.

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

## 마이그레이션 실행

마이그레이션을 실행합니다.

```
typeorm migration:run
```

## TypeORM 서비스 생성

TypeORM 서비스를 만듭니다.

```
typeorm service:create -n user
```

## 서비스 파일 업데이트

생성된 서비스 파일을 다음 코드로 업데이트합니다.

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

## 컨트롤러 만들기

컨트롤러를 만듭니다.

```
typeorm controller:create -n user
```

## 컨트롤러 파일 업데이트

생성된 컨트롤러 파일을 다음 코드로 업데이트합니다.

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

## 컨트롤러 등록

Nest.js 모듈에 컨트롤러를 등록합니다.

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

## Nest.js 애플리케이션 시작

Nest.js 애플리케이션을 시작합니다.

```
nest start
```

## 결론

이 게시물에서는 TypeORM을 Nest.js와 통합하는 방법을 배웠습니다.