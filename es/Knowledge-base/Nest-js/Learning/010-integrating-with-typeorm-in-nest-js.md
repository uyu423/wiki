---
title: 010: Integración con TypeORM en Nest.js
description: 
published: true
date: 2023-02-09T02:55:48.263Z
tags: 
editor: markdown
dateCreated: 2023-02-09T02:55:42.273Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [010: Integrating with TypeORM in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/010-integrating-with-typeorm-in-nest-js)
{.links-list}


# Integración con TypeORM en Nest.js

Nest.js es un marco para crear aplicaciones Node.js. Está basado en Express y usa TypeScript.

TypeORM es un mapeador relacional de objetos (ORM) para TypeScript. Permite a los desarrolladores trabajar con bases de datos utilizando objetos y TypeScript.

En esta publicación, aprenderemos cómo integrar TypeORM con Nest.js.

## Requisitos previos

- Nodo.js
- Mecanografiado
- Expresar
- TipoORM

## Instalación

Instale Nest.js y TypeORM usando npm.

```
npm install --save @nestjs/typeorm typeorm
```

## Crear un proyecto Nest.js

Cree un nuevo proyecto Nest.js.

```
nest new project-name
```

## Crear una entidad TypeORM

Cree una entidad TypeORM.

```
typeorm entity:create -n User
```

## Configurar TipoORM

Cree un archivo llamado ormconfig.json en la raíz del proyecto.

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

Reemplace los valores en el archivo con su propia configuración de base de datos.

## Crear una migración

Crear una migración.

```
typeorm migration:create -n migration-name
```

## Actualice el archivo de migración

Actualice el archivo de migración generado con el siguiente código.

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

## Ejecutar la migración

Ejecute la migración.

```
typeorm migration:run
```

## Crear un servicio TypeORM

Cree un servicio TypeORM.

```
typeorm service:create -n user
```

## Actualice el archivo de servicio

Actualice el archivo de servicio generado con el siguiente código.

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

## Crear un controlador

Crea un controlador.

```
typeorm controller:create -n user
```

## Actualice el archivo del controlador

Actualice el archivo de controlador generado con el siguiente código.

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

## Registrar el controlador

Registre el controlador en el módulo Nest.js.

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

## Inicie la aplicación Nest.js

Inicie la aplicación Nest.js.

```
nest start
```

## Conclusión

En esta publicación, hemos aprendido cómo integrar TypeORM con Nest.js.