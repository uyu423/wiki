---
title: Uso de TypeScript con NeDB para base de datos NoSQL ligera
description: 
published: true
date: 2023-02-09T18:56:28.232Z
tags: 
editor: markdown
dateCreated: 2023-02-09T18:56:26.568Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Using TypeScript with NeDB for Lightweight NoSQL Database***English** document is available*](/en/Knowledge-base/TypeScript/using-typescript-with-nedb-for-lightweight-nosql-database)
{.links-list}


# Uso de TypeScript con NeDB para base de datos NoSQL ligera

## Introducción

TypeScript es un superconjunto escrito de JavaScript que se compila en JavaScript simple. Ofrece clases, módulos e interfaces para ayudarlo a crear componentes sólidos. TypeScript es uno de los muchos lenguajes que se pueden usar con el entorno de tiempo de ejecución de Node.js.

NeDB es una base de datos NoSQL liviana que se puede usar tanto en Node.js como en el navegador. Es compatible con la API de MongoDB, lo que facilita su uso con las bibliotecas y herramientas existentes de MongoDB.

En este artículo, le mostraremos cómo usar TypeScript con NeDB. Crearemos una sencilla aplicación de tareas pendientes que almacene datos en una base de datos NeDB.

## Configuración de un proyecto TypeScript

Primero, necesitamos crear un proyecto de TypeScript. Usaremos la plantilla de proyecto [TypeScript Node Starter](https://github.com/Microsoft/TypeScript-Node-Starter).

```
$ git clone https://github.com/Microsoft/TypeScript-Node-Starter.git todo-app
$ cd todo-app
$ npm install
```

A continuación, necesitamos instalar los tipos NeDB.

```
$ npm install --save-dev @types/nedb
```

## Creación de un modelo de tareas pendientes

Comenzaremos creando un modelo de tareas pendientes. Cree un nuevo archivo llamado `todo.ts` en el directorio `src` con el siguiente código:

```typescript
export class ToDo {
  _id: string;
  title: string;
  completed: boolean;
  date: Date;

  constructor(title: string) {
    this.title = title;
    this.completed = false;
    this.date = new Date();
  }
}
```

Este modelo tiene cuatro campos: `_id`, `título`, `completado` y `fecha`. El campo `_id` es la clave principal y es generado por NeDB. El campo `título` es el título del elemento pendiente. El campo `completed` es un valor booleano que indica si la tarea pendiente está completa. El campo `fecha` es la fecha en que se creó la tarea pendiente.

## Creación de un servicio de tareas pendientes

A continuación, crearemos un servicio de tareas pendientes. Este servicio será responsable de las operaciones CRUD en elementos pendientes. Cree un nuevo archivo llamado `todoService.ts` en el directorio `src` con el siguiente código:

```typescript
import { Datastore } from 'nedb';
import { ToDo } from './todo';

export class ToDoService {
  private db: Datastore;

  constructor(db: Datastore) {
    this.db = db;
  }

  public async getAll(): Promise<ToDo[]> {
    return new Promise<ToDo[]>((resolve, reject) => {
      this.db.find({}, (err, docs: ToDo[]) => {
        if (err) {
          return reject(err);
        }
        resolve(docs);
      });
    });
  }

  public async getById(id: string): Promise<ToDo | null> {
    return new Promise<ToDo | null>((resolve, reject) => {
      this.db.findOne({ _id: id }, (err, doc: ToDo) => {
        if (err) {
          return reject(err);
        }
        resolve(doc);
      });
    });
  }

  public async create(todo: ToDo): Promise<string> {
    return new Promise<string>((resolve, reject) => {
      this.db.insert(todo, (err, doc: ToDo) => {
        if (err) {
          return reject(err);
        }
        resolve(doc._id);
      });
    });
  }

  public async update(todo: ToDo): Promise<number> {
    return new Promise<number>((resolve, reject) => {
      this.db.update({ _id: todo._id }, todo, {}, (err, numUpdated: number) => {
        if (err) {
          return reject(err);
        }
        resolve(numUpdated);
      });
    });
  }

  public async delete(id: string): Promise<number> {
    return new Promise<number>((resolve, reject) => {
      this.db.remove({ _id: id }, {}, (err, numRemoved: number) => {
        if (err) {
          return reject(err);
        }
        resolve(numRemoved);
      });
    });
  }
}
```

Este servicio tiene cinco métodos: `getAll`, `getById`, `create`, `update` y `delete`. Estos métodos se asignan a las operaciones CRUD en elementos pendientes.

Los métodos `getAll` y `getById` devuelven una `Promesa` que se resuelve en una matriz de tareas pendientes o en una única tarea pendiente, respectivamente.

Los métodos `create`, `update` y `delete` devuelven una `promesa` que se resuelve en el `_id` del elemento pendiente creado, la cantidad de elementos pendientes actualizados o la cantidad de tareas pendientes. elementos eliminados, respectivamente.

## Creación de un controlador de tareas pendientes

A continuación, crearemos un controlador de tareas pendientes. Este controlador será responsable de manejar las solicitudes HTTP. Cree un nuevo archivo llamado `todoController.ts` en el directorio `src` con el siguiente código:

```typescript
import { Request, Response } from 'express';
import { ToDoService } from './todoService';
import { ToDo } from './todo';

export class ToDoController {
  private todoService: ToDoService;

  constructor(todoService: ToDoService) {
    this.todoService = todoService;
  }

  public async getAll(req: Request, res: Response) {
    try {
      const todos = await this.todoService.getAll();
      res.json(todos);
    } catch (err) {
      res.status(500).send(err);
    }
  }

  public async getById(req: Request, res: Response) {
    const id = req.params.id;
    try {
      const todo = await this.todoService.getById(id);
      if (todo) {
        res.json(todo);
      } else {
        res.sendStatus(404);
      }
    } catch (err) {
      res.status(500).send(err);
    }
  }

  public async create(req: Request, res: Response) {
    const todo = req.body as ToDo;
    try {
      const id = await this.todoService.create(todo);
      res.json({ id: id });
    } catch (err) {
      res.status(500).send(err);
    }
  }

  public async update(req: Request, res: Response) {
    const todo = req.body as ToDo;
    if (!todo._id) {
      return res.status(400).send('To-Do item must have an _id');
    }
    try {
      const numUpdated = await this.todoService.update(todo);
      res.json({ numUpdated: numUpdated });
    } catch (err) {
      res.status(500).send(err);
    }
  }

  public async delete(req: Request, res: Response) {
    const id = req.params.id;
    try {
      const numDeleted = await this.todoService.delete(id);
      res.json({ numDeleted: numDeleted });
    } catch (err) {
      res.status(500).send(err);
    }
  }
}
```

Este controlador tiene cinco métodos: `getAll`, `getById`, `create`, `update` y `delete`. Estos métodos se asignan a los métodos HTTP `GET`, `GET`/`:id`, `POST`, `PUT` y `DELETE`, respectivamente.

Los métodos `getAll` y `getById` devuelven una matriz de elementos pendientes o un único elemento pendiente, respectivamente.

Los métodos `create`, `update` y `delete` devuelven el `_id` del elemento pendiente creado, el número de elementos pendientes actualizados o el número de elementos pendientes eliminados, respectivamente.

## Creando un servidor Express

A continuación, crearemos un servidor [Express](https://expressjs.com/). Express es un marco de aplicación web para Node.js.

Cree un nuevo archivo llamado `server.ts` en el directorio `src` con el siguiente código:

```typescript
import * as express from 'express';
import * as bodyParser from 'body-parser';
import { ToDoController } from './todoController';
import { Datastore } from 'nedb';

const app = express();
const PORT = 3000;

const db = new Datastore('todo.db');
db.loadDatabase();

const todoService = new ToDoService(db);
const todoController = new ToDoController(todoService);

app.use(bodyParser.json());

app.get('/todos', todoController.getAll);
app.get('/todos/:id', todoController.getById);
app.post('/todos', todoController.create);
app.put('/todos', todoController.update);
app.delete('/todos/:id', todoController.delete);

app.listen(PORT, () => {
  console.log(`Server listening on port ${PORT}`);
});
```

Este servidor crea una base de datos NeDB llamada `todo.db` y la carga. A continuación, crea un servicio de tareas pendientes y un controlador de tareas pendientes.

El servidor configura Express para usar el middleware [body-parser](https://www.npmjs.com/package/body-parser) para analizar cuerpos JSON.

El servidor define rutas para los métodos del controlador To-Do. La ruta `app.get` se asigna al método `GET`. La ruta `app.get`/`:id` se asigna al método `GET` con un parámetro de ruta. La ruta `app.post` se asigna al método `POST`. La ruta `app.put` se asigna al método `PUT`. La ruta `app.delete` se asigna al método `DELETE`.

Finalmente, el servidor comienza a escuchar en el puerto 3000.

## Prueba de la API de tareas pendientes

Podemos probar nuestra API To-Do usando [cURL](https://curl.haxx.se/).

Primero, iniciaremos el servidor:

```
$ npm start

> todo-app@1.0.0 start /Users/username/projects/todo-app
> ts-node src/server.ts

Server listening on port 3000
```

A continuación, usaremos cURL para crear una tarea pendiente:

```
$ curl -X POST -H "Content-Type: application/json" -d '{"title": "Buy milk"}' http://localhost:3000/todos
```

Este comando cURL envía una solicitud `POST` al extremo `/todos` con un cuerpo JSON. El cuerpo JSON contiene una tarea pendiente con el título "Comprar leche".

Deberíamos obtener una respuesta como esta:

```json
{"id": "5e1d280b04a7a22a68e0e7cd"}
```

Este es el `_id` de la tarea pendiente que creamos. Podemos usar este `_id` para recuperar el elemento To-Do:

```
$ curl http://localhost:3000/todos/5e1d280b04a7a22a68e0e7cd
```

Deberíamos obtener una respuesta como esta:

```json
{"_id":"5e1d280b04a7a22a68e0e7cd","title":"Buy milk","completed":false,"date":"2020-01-08T05:34:51.596Z"}
```

Este es el elemento de tareas pendientes que creamos. Podemos ver que el campo `completado` es `falso` y el campo `fecha` es la fecha en que creamos el elemento.

A continuación, actualizaremos el elemento Tareas pendientes:

```
$ curl -X PUT -H "Content-Type: application/json" -d '{"_id": "5e1d280b04a7a22a68e0e7cd", "title": "Buy eggs", "completed": true}' http://localhost:3000/todos
```

Este comando cURL envía una solicitud `PUT` al extremo `/todos` con un cuerpo JSON. El cuerpo JSON contiene el elemento pendiente actualizado. Cambiamos el título a `Comprar huevos` y configuramos el campo `completado` en `verdadero`.

Deberíamos obtener una respuesta como esta:

```json
{"numUpdated": 1}
```

Este es el número de tareas pendientes que se actualizaron. Podemos recuperar el elemento pendiente actualizado para verificar que se actualizó:

```
$ curl http://localhost:3000/todos/5e1d280b04a7a22a68e0e7cd
```

Deberíamos obtener una respuesta como esta:

```json
{"_id":"5e1d280b04a7a22a68e0e7cd","title":"Buy eggs","completed":true,"date":"2020-01-08T05:34:51.596Z"}
```

Finalmente, eliminaremos el elemento To-Do:

```
$ curl -X DELETE http://localhost:3000/todos/5e1d280b04a7a22a68e0e7cd
```

Este comando cURL envía una solicitud `DELETE` al extremo `/todos/:id`. Estamos pasando el `_id` del elemento To-Do para eliminar como un parámetro de ruta.

Deberíamos obtener una respuesta como esta:

```json
{"numDeleted": 1}
```

Este es el número de tareas pendientes que se eliminaron. Podemos verificar que el elemento se eliminó recuperándolo:

```
$ curl http://localhost:3000/todos/5e1d280b04a7a22a68e0e7cd
```

Deberíamos obtener un error `404 No encontrado` porque el elemento Tarea pendiente ya no existe.

## Conclusión

En este artículo, le mostramos cómo usar TypeScript con NeDB. Hemos creado una API To-Do simple que almacena datos en una base de datos NeDB. También le mostramos cómo probar la API usando cURL.