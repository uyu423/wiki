---
title: 059: Uso de Nest.js con IndexedDB
description: 
published: true
date: 2023-02-15T22:32:32.908Z
tags: 
editor: markdown
dateCreated: 2023-02-15T22:32:31.004Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [059: Using Nest.js with IndexedDB***English** document is available*](/en/Knowledge-base/Nest-js/Learning/059-using-nest-js-with-indexeddb)
{.links-list}


# Uso de Nest.js con IndexedDB

En esta publicación, veremos cómo usar [Nest.js](https://nestjs.com/) con [IndexedDB](https://developer.mozilla.org/en-US/docs/ Web/API/IndexedDB_API), una base de datos basada en JavaScript.

Comenzaremos creando una aplicación Nest.js simple que se conectará a una base de datos IndexedDB. Luego, agregaremos código para insertar datos en la base de datos y consultar los datos.

## Creación de una aplicación Nest.js

Primero, necesitamos crear una aplicación Nest.js. Podemos hacer esto usando [Nest CLI] (https://docs.nestjs.com/cli/overview).

```
$ nest new nest-indexeddb
```

Esto creará una nueva aplicación Nest.js en un directorio llamado `nest-indexeddb`.

## Conexión a la base de datos

A continuación, necesitamos conectarnos a la base de datos IndexedDB. Podemos hacer esto usando el paquete npm [`idb`](https://www.npmjs.com/package/idb).

Primero, necesitamos instalar el paquete `idb`:

```
$ npm install idb
```

Luego, podemos crear un nuevo archivo llamado `database.service.ts` en el directorio `src/` con los siguientes contenidos:

```typescript
import { Injectable } from '@nestjs/common';
import { openDB, DBSchema } from 'idb';

@Injectable()
export class DatabaseService {
  private dbPromise: Promise<IDBDatabase>;

  constructor() {
    this.dbPromise = openDB<DBSchema>('nest-indexeddb', 1, {
      upgrade(db) {
        db.createObjectStore('todos', {
          keyPath: 'id',
        });
      },
    });
  }

  getDb(): Promise<IDBDatabase> {
    return this.dbPromise;
  }
}
```

En este archivo, estamos creando un nuevo servicio llamado `DatabaseService` que se encargará de conectar con la base de datos. Estamos usando la función `openDB` del paquete `idb` para abrir la base de datos. También estamos pasando un objeto `esquema` que define la estructura de la base de datos. En este caso, estamos creando un nuevo almacén de objetos llamado `todos` que contendrá datos sobre todos.

## Inserción de datos en la base de datos

Ahora que tenemos un servicio para conectarnos a la base de datos, podemos usarlo para insertar datos en la base de datos.

Primero, necesitamos crear un nuevo archivo llamado `todo.model.ts` en el directorio `src/` con los siguientes contenidos:

```typescript
export class Todo {
  id: number;
  title: string;
  completed: boolean;
}
```

Este archivo contiene un modelo para una tarea pendiente. Tiene tres campos: 'id', 'título' y 'completado'.

A continuación, debemos crear un nuevo archivo llamado `todo.service.ts` en el directorio `src/` con los siguientes contenidos:

```typescript
import { Injectable } from '@nestjs/common';
import { DatabaseService } from './database.service';
import { Todo } from './todo.model';

@Injectable()
export class TodoService {
  constructor(private databaseService: DatabaseService) {}

  async createTodo(todo: Todo): Promise<void> {
    const db = await this.databaseService.getDb();
    const tx = db.transaction('todos', 'readwrite');
    const store = tx.objectStore('todos');
    store.put(todo);
    await tx.complete;
  }
}
```

En este archivo estamos creando un nuevo servicio llamado `TodoService` que será el encargado de insertar los datos en la base de datos. Estamos inyectando `DatabaseService` para que podamos usarlo para obtener una conexión a la base de datos.

El método `createTodo` toma un objeto `Todo` como parámetro y lo inserta en la base de datos. Primero, obtiene una conexión a la base de datos. Luego, inicia una nueva transacción. Las transacciones se utilizan para garantizar que los datos se inserten en la base de datos de forma atómica. En otras palabras, se insertan todos los datos o ninguno.

Después de iniciar la transacción, el código obtiene una referencia al almacén de objetos `todos`. Luego, llama al método `put` en la tienda, pasando el objeto `todo`. Esto insertará el objeto `todo` en la base de datos.

Finalmente, el código llama al método `completo` en la transacción. Esto confirmará la transacción y los datos se insertarán en la base de datos.

## Consulta de datos de la base de datos

Ahora que podemos insertar datos en la base de datos, echemos un vistazo a cómo consultar datos de la base de datos.

Podemos consultar datos de la base de datos utilizando el método `get` en un almacén de objetos. El método `get` toma una clave como parámetro y devuelve el valor asociado con esa clave.

Por ejemplo, digamos que tenemos una tarea pendiente con un `id` de `1`. Podemos consultar ese todo desde la base de datos de esta manera:

```typescript
const todo = await store.get(1);
```

También podemos usar el método `getAll` para obtener todos los valores de un almacén de objetos. Por ejemplo, podemos obtener todos los todos de la base de datos de esta manera:

```typescript
const todos = await store.getAll();
```

También podemos usar el método `getAllKeys` para obtener todas las claves de un almacén de objetos. Por ejemplo, podemos obtener todas las claves del almacén de objetos `todos` así:

```typescript
const keys = await store.getAllKeys();
```

## Eliminación de datos de la base de datos

Podemos eliminar datos de la base de datos utilizando el método `delete` en un almacén de objetos. El método `delete` toma una clave como parámetro y elimina el valor asociado con esa clave.

Por ejemplo, digamos que tenemos una tarea pendiente con un `id` de `1`. Podemos eliminar ese todo de la base de datos de esta manera:

```typescript
await store.delete(1);
```

## Conclusión

En esta publicación, hemos visto cómo usar Nest.js con IndexedDB. Hemos visto cómo conectarse a la base de datos, insertar datos en la base de datos, consultar datos de la base de datos y eliminar datos de la base de datos.