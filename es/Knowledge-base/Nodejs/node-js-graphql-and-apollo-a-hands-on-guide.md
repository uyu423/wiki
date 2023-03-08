---
title: Node.js, GraphQL y Apollo: una guía práctica
description: 
published: true
date: 2023-02-06T09:57:15.414Z
tags: 
editor: markdown
dateCreated: 2023-02-06T09:57:13.686Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Node.js, GraphQL and Apollo: A Hands-On Guide***English** document is available*](/en/Knowledge-base/Nodejs/node-js-graphql-and-apollo-a-hands-on-guide)
{.links-list}


# Node.js, GraphQL y Apollo: una guía práctica

## Introducción

En este artículo, veremos cómo usar Node.js, GraphQL y Apollo para crear una API simple pero poderosa para nuestra aplicación. Construiremos una aplicación simple de tareas pendientes y la API impulsará la interfaz de usuario.

Usaremos las siguientes tecnologías:

- [Node.js](https://nodejs.org/)
- [GraphQL](https://graphql.org/)
- [Apolo](https://www.apollographql.com/)

## ¿Qué es Node.js?

Node.js es un tiempo de ejecución de JavaScript basado en el motor de JavaScript V8 de Chrome. Node.js utiliza un modelo de E/S sin bloqueo y controlado por eventos que lo hace liviano y eficiente.

Node.js es una plataforma ideal para crear aplicaciones de red altamente escalables.

## ¿Qué es GraphQL?

GraphQL es un lenguaje de consulta para su API y un tiempo de ejecución del lado del servidor para ejecutar consultas mediante el uso de un sistema de tipos que defina para sus datos. GraphQL no está vinculado a ninguna base de datos o motor de almacenamiento específico y, en cambio, está respaldado por su código y datos existentes.

GraphQL proporciona una descripción completa y comprensible de los datos en su API, brinda a los clientes el poder de solicitar exactamente lo que necesitan y nada más, facilita la evolución de las API con el tiempo y habilita herramientas poderosas para desarrolladores.

## ¿Qué es Apolo?

Apollo es un conjunto de herramientas para facilitar la creación de aplicaciones GraphQL. Incluye un cliente y un servidor, y tiene enlaces para marcos populares como React, Angular, Vue.js y más.

## Configurando nuestro proyecto

Empecemos configurando nuestro proyecto. Usaremos el marco [Express](https://expressjs.com/) para construir nuestro servidor.

Primero, necesitamos instalar las dependencias para nuestro proyecto. Usaremos [npm](https://www.npmjs.com/) para instalar nuestras dependencias.

```
npm install express graphql apollo-server-express
```

A continuación, necesitamos crear un archivo para nuestro servidor. Lo llamaremos `server.js`.

```javascript
const express = require('express');
const { ApolloServer } = require('apollo-server-express');

const app = express();

const typeDefs = `
  type Query {
    hello: String
  }
`;

const resolvers = {
  Query: {
    hello: () => 'Hello World!',
  },
};

const server = new ApolloServer({
  typeDefs,
  resolvers,
});

server.applyMiddleware({ app });

app.listen({ port: 4000 }, () =>
  console.log(`Server ready at http://localhost:4000${server.graphqlPath}`),
);
```

En el código anterior, importamos las dependencias que necesitamos, creamos un servidor Express y definimos nuestro esquema GraphQL. También hemos definido un solucionador para nuestra consulta `hola`.

Finalmente, iniciamos nuestro servidor en el puerto `4000`.

Puede iniciar el servidor ejecutando el siguiente comando:

```
node server.js
```

Si navega a [http://localhost:4000/graphql](http://localhost:4000/graphql), debería ver GraphQL Playground donde puede ejecutar consultas en su API.

Intenta ejecutar la siguiente consulta:

```graphql
query {
  hello
}
```

Deberías ver el siguiente resultado:

```json
{
  "data": {
    "hello": "Hello World!"
  }
}
```

## Agregando datos

Ahora que tenemos nuestro servidor en funcionamiento, agreguemos algunos datos a nuestra API. Usaremos la biblioteca [lowdb](https://github.com/typicode/lowdb) para almacenar nuestros datos.

Primero, necesitamos instalar la dependencia lowdb:

```
npm install lowdb
```

A continuación, necesitamos crear un archivo para nuestra base de datos. Lo llamaremos `db.js`.

```javascript
const low = require('lowdb');
const FileSync = require('lowdb/adapters/FileSync');

const adapter = new FileSync('db.json');
const db = low(adapter);

// Set some defaults
db.defaults({ todos: [] }).write();

module.exports = db;
```

En el código anterior, importamos las dependencias que necesitamos y creamos un archivo llamado `db.json` para almacenar nuestros datos. También hemos creado una matriz `todos` para almacenar nuestras tareas pendientes.

Luego, necesitamos actualizar nuestro código de servidor para usar nuestra base de datos.

```javascript
const express = require('express');
const { ApolloServer } = require('apollo-server-express');
const low = require('lowdb');
const FileSync = require('lowdb/adapters/FileSync');

const adapter = new FileSync('db.json');
const db = low(adapter);

db.defaults({ todos: [] }).write();

const typeDefs = `
  type Todo {
    id: ID!
    text: String!
    done: Boolean!
  }

  type Query {
    todos: [Todo!]!
  }

  type Mutation {
    addTodo(text: String!): Todo
    toggleTodo(id: ID!): Todo
    deleteTodo(id: ID!): Boolean
  }
`;

const resolvers = {
  Query: {
    todos: () => db.get('todos').value(),
  },
  Mutation: {
    addTodo: (_, { text }) => {
      const todo = {
        id: Date.now(),
        text,
        done: false,
      };

      db.get('todos')
        .push(todo)
        .write();

      return todo;
    },
    toggleTodo: (_, { id }) => {
      const todo = db
        .get('todos')
        .find({ id })
        .value();

      todo.done = !todo.done;

      db.get('todos')
        .find({ id })
        .assign(todo)
        .write();

      return todo;
    },
    deleteTodo: (_, { id }) => {
      db.get('todos')
        .remove({ id })
        .write();

      return true;
    },
  },
};

const server = new ApolloServer({
  typeDefs,
  resolvers,
});

server.applyMiddleware({ app });

app.listen({ port: 4000 }, () =>
  console.log(`Server ready at http://localhost:4000${server.graphqlPath}`),
);
```

En el código anterior, hemos actualizado nuestro esquema para incluir un tipo `Todo` y hemos definido tres consultas: `todos`, `addTodo` y `toggleTodo`. También hemos definido tres resolutores correspondientes.

La consulta `todos` obtendrá todas las tareas pendientes de nuestra base de datos. La mutación `addTodo` agregará una tarea pendiente a nuestra base de datos. La mutación `toggleTodo` alternará el indicador `hecho` para una tarea pendiente.

## Agregando el front-end

Ahora que tenemos nuestra API en funcionamiento, agreguemos un front-end a nuestra aplicación. Usaremos [React](https://reactjs.org/).

Primero, necesitamos instalar las dependencias para nuestro proyecto. Usaremos [Crear aplicación React] (https://github.com/facebook/create-react-app) para configurar nuestro proyecto React.

```
npm install -g create-react-app
create-react-app todo-app
cd todo-app
npm install apollo-boost graphql react-apollo
```

A continuación, debemos actualizar nuestro archivo `App.js`.

```javascript
import React from 'react';
import { ApolloProvider } from 'react-apollo';
import { ApolloClient } from 'apollo-boost';
import { gql } from 'graphql-tag';
import { Query } from 'react-apollo';

const client = new ApolloClient({
  uri: 'http://localhost:4000/graphql',
});

const GET_TODOS = gql`
  query getTodos {
    todos {
      id
      text
      done
    }
  }
`;

function App() {
  return (
    <ApolloProvider client={client}>
      <div className="App">
        <Query query={GET_TODOS}>
          {({ loading, error, data }) => {
            if (loading) return <p>Loading...</p>;
            if (error) return <p>Error :(</p>;

            return data.todos.map(todo => (
              <div key={todo.id}>
                {todo.text}
              </div>
            ));
          }}
        </Query>
      </div>
    </ApolloProvider>
  );
}

export default App;
```

En el código anterior, importamos las dependencias que necesitamos y creamos un nuevo cliente Apollo. También hemos definido una consulta llamada `GET_TODOS` que obtendrá todas las tareas pendientes de nuestra API.

Finalmente, envolvimos nuestro componente `App` en un `ApolloProvider` y representamos la consulta `GET_TODOS` usando el componente `Query`.

Si inicia el servidor React ejecutando el siguiente comando:

```
npm start
```

y navegue a [http://localhost:3000](http://localhost:3000), debería ver las tareas pendientes de nuestra API representadas en la página.

## Agregando mutaciones

Ahora que podemos consultar nuestra API, agreguemos la capacidad de realizar mutaciones. Comenzaremos agregando un formulario a nuestro componente `App`.

```javascript
import React, { useState } from 'react';
import { ApolloProvider } from 'react-apollo';
import { ApolloClient } from 'apollo-boost';
import { gql } from 'graphql-tag';
import { Query, Mutation } from 'react-apollo';

const client = new ApolloClient({
  uri: 'http://localhost:4000/graphql',
});

const GET_TODOS = gql`
  query getTodos {
    todos {
      id
      text
      done
    }
  }
`;

const ADD_TODO = gql`
  mutation addTodo($text: String!) {
    addTodo(text: $text) {
      id
      text
      done
    }
  }
`;

const TOGGLE_TODO = gql`
  mutation toggleTodo($id: ID!) {
    toggleTodo(id: $id) {
      id
      text
      done
    }
  }
`;

const DELETE_TODO = gql`
  mutation deleteTodo($id: ID!) {
    deleteTodo(id: $id)
  }
`;

function App() {
  const [todoText, setTodoText] = useState('');

  return (
    <ApolloProvider client={client}>
      <div className="App">
        <Mutation mutation={ADD_TODO}>
          {(addTodo, { data }) => (
            <form
              onSubmit={e => {
                e.preventDefault();
                addTodo({ variables: { text: todoText } });
                setTodoText('');
              }}
            >
              <input
                type="text"
                value={todoText}
                onChange={e => setTodoText(e.target.value)}
              />
              <button type="submit">Add Todo</button>
            </form>
          )}
        </Mutation>
        <Query query={GET_TODOS}>
          {({ loading, error, data }) => {
            if (loading) return <p>Loading...</p>;
            if (error) return <p>Error :(</p>;

            return data.todos.map(todo => (
              <div key={todo.id}>
                <span style={{ textDecoration: todo.done ? 'line-through' : 'none' }}>
                  {todo.text}
                </span>
                <Mutation mutation={TOGGLE_TODO}>
                  {toggleTodo => (
                    <button
                      type="button"
                      onClick={() => toggleTodo({ variables: { id: todo.id } })}
                    >
                      Toggle
                    </button>
                  )}
                </Mutation>
                <Mutation mutation={DELETE_TODO}>
                  {deleteTodo => (
                    <button
                      type="button"
                      onClick={() => deleteTodo({ variables: { id: todo.id } })}
                    >
                      Delete
                    </button>
                  )}
                </Mutation>
              </div>
            ));
          }}
        </Query>
      </div>
    </ApolloProvider>
  );
}

export default App;
```

En el código anterior, importamos el enlace `useState` de React y definimos tres nuevas mutaciones: `ADD_TODO`, `TOGGLE_TODO` y `DELETE_TODO`.

También hemos actualizado nuestro componente `Aplicación` para incluir un formulario para agregar tareas y hemos agregado botones para alternar y eliminar tareas pendientes.

Si navega a [http://localhost:3000](http://localhost:3000), ahora debería ver un formulario para agregar tareas pendientes, y debería poder alternar y eliminar tareas pendientes.

## Conclusión

En este artículo, analizamos cómo usar Node.js, GraphQL y Apollo para crear una API simple pero poderosa para nuestra aplicación. Configuramos un servidor, agregamos una base de datos, creamos un esquema GraphQL y resoluciones, y agregamos un front-end usando React.

Finalmente, hemos agregado la capacidad de realizar mutaciones en nuestros datos.