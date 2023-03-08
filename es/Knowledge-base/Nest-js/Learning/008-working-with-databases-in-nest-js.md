---
title: 008: Trabajar con bases de datos en Nest.js
description: 
published: true
date: 2023-02-14T19:32:39.420Z
tags: 
editor: markdown
dateCreated: 2023-02-14T19:32:37.817Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [008: Working with databases in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/008-working-with-databases-in-nest-js)
{.links-list}


# Trabajar con bases de datos en Nest.js

Nest.js es un marco de Node.js para crear aplicaciones escalables del lado del servidor. Utiliza TypeScript, un superconjunto de JavaScript, y proporciona una plataforma poderosa para crear servicios web RESTful.

En esta publicación, veremos cómo trabajar con bases de datos en Nest.js. Cubriremos los siguientes temas:

- Conexión a una base de datos
- Usando el ORM de Nest.js
- Uso de Nest.js QueryBuilder

## Conexión a una base de datos

El primer paso para trabajar con bases de datos en Nest.js es establecer una conexión con la base de datos. Nest.js es compatible con una variedad de bases de datos, incluidas MySQL, PostgreSQL, MongoDB y SQLite.

Para establecer una conexión a una base de datos, deberá crear una fuente de datos. Nest.js proporciona un paquete @nestjs/typeorm que facilita la creación de fuentes de datos.

Para crear una fuente de datos, deberá instalar el paquete @nestjs/typeorm y el controlador para su base de datos. Por ejemplo, si usa MySQL, deberá instalar el paquete mysql2.

Una vez que tenga instalados los paquetes de controlador de base de datos y @nestjs/typeorm, puede crear una fuente de datos importando la función createConnection() del paquete @nestjs/typeorm y pasando las opciones para su conexión de base de datos.

El siguiente ejemplo crea una fuente de datos para una base de datos MySQL:

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

## Usando el ORM de Nest.js

Una vez que haya establecido una fuente de datos, puede comenzar a usar el ORM de Nest.js para trabajar con su base de datos. El ORM de Nest.js se basa en el patrón Active Record y proporciona una manera conveniente de trabajar con su base de datos.

Para usar el ORM de Nest.js, deberá crear un repositorio. Un repositorio es una clase que contiene métodos para realizar operaciones CRUD en una entidad de base de datos.

Para crear un repositorio, deberá importar el Repositorio desde el paquete @nestjs/typeorm y ampliar la clase Repositorio.

El siguiente ejemplo crea un repositorio para una entidad Usuario:

```typescript
import { Repository } from '@nestjs/typeorm';

@EntityRepository(User)
export class UserRepository extends Repository<User> {}
```

Una vez que tenga un repositorio, puede comenzar a realizar operaciones CRUD en las entidades de su base de datos. El siguiente ejemplo muestra cómo encontrar un usuario por su id:

```typescript
import { UserRepository } from './user.repository';

const user = await this.userRepository.findOne(1);
```

## Uso de Nest.js QueryBuilder

Además de los métodos proporcionados por la clase Repository, también puede usar Nest.js QueryBuilder para construir consultas más complejas.

Nest.js QueryBuilder se basa en Doctrine QueryBuilder y proporciona una manera conveniente de crear consultas encadenando métodos.

Para usar QueryBuilder, deberá importar la función getConnection() del paquete @nestjs/typeorm y llamar a la función createQueryBuilder() en la conexión.

El siguiente ejemplo muestra cómo usar QueryBuilder para encontrar un usuario por su ID:

```typescript
import { getConnection } from '@nestjs/typeorm';

const user = await getConnection()
  .createQueryBuilder()
  .select('user')
  .from(User, 'user')
  .where('user.id = :id', { id: 1 })
  .getOne();
```

## Conclusión

En esta publicación, echamos un vistazo a cómo trabajar con bases de datos en Nest.js. Hemos cubierto los siguientes temas:

- Conexión a una base de datos
- Usando el ORM de Nest.js
- Uso de Nest.js QueryBuilder

Si está interesado en obtener más información sobre Nest.js, asegúrese de consultar la documentación de Nest.js.