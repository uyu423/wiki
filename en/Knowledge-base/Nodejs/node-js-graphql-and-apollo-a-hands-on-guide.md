---
title: Node.js, GraphQL and Apollo: A Hands-On Guide
description: 
published: true
date: 2023-02-06T09:57:19.331Z
tags: 
editor: markdown
dateCreated: 2023-02-06T09:57:13.689Z
---

- [Node.js, GraphQL y Apollo: una guía práctica***Spanish** document is available*](/es/Knowledge-base/Nodejs/node-js-graphql-and-apollo-a-hands-on-guide)
{.links-list}
- [Node.js、GraphQL 和 Apollo：动手指南***Chinese Simplified** document is available*](/zh/Knowledge-base/Nodejs/node-js-graphql-and-apollo-a-hands-on-guide)
{.links-list}
- [Node.js, GraphQL 및 Apollo: 실습 가이드***Korean** document is available*](/ko/Knowledge-base/Nodejs/node-js-graphql-and-apollo-a-hands-on-guide)
{.links-list}


# Node.js, GraphQL and Apollo: A Hands-On Guide

## Introduction

In this article, we'll be looking at how to use Node.js, GraphQL and Apollo to build a simple, yet powerful API for our application. We'll be building a simple to-do application and the API will power the front-end interface.

We'll be using the following technologies:

- [Node.js](https://nodejs.org/)
- [GraphQL](https://graphql.org/)
- [Apollo](https://www.apollographql.com/)

## What is Node.js?

Node.js is a JavaScript runtime built on Chrome's V8 JavaScript engine. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient.

Node.js is an ideal platform for building highly scalable network applications.

## What is GraphQL?

GraphQL is a query language for your API, and a server-side runtime for executing queries by using a type system you define for your data. GraphQL isn't tied to any specific database or storage engine and is instead backed by your existing code and data.

GraphQL provides a complete and understandable description of the data in your API, gives clients the power to ask for exactly what they need and nothing more, makes it easier to evolve APIs over time, and enables powerful developer tools.

## What is Apollo?

Apollo is a set of tools to make it easier to build GraphQL applications. It includes a client and server, and has bindings for popular frameworks like React, Angular, Vue.js and more.

## Setting up our project

Let's start by setting up our project. We'll be using the [Express](https://expressjs.com/) framework to build our server.

First, we need to install the dependencies for our project. We'll be using [npm](https://www.npmjs.com/) to install our dependencies.

```
npm install express graphql apollo-server-express
```

Next, we need to create a file for our server. We'll call it `server.js`.

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

In the code above, we've imported the dependencies we need, created an Express server and defined our GraphQL schema. We've also defined a resolver for our `hello` query.

Finally, we've started our server on port `4000`.

You can start the server by running the following command:

```
node server.js
```

If you navigate to [http://localhost:4000/graphql](http://localhost:4000/graphql), you should see the GraphQL Playground where you can run queries against your API.

Try running the following query:

```graphql
query {
  hello
}
```

You should see the following result:

```json
{
  "data": {
    "hello": "Hello World!"
  }
}
```

## Adding data

Now that we have our server up and running, let's add some data to our API. We'll use the [lowdb](https://github.com/typicode/lowdb) library to store our data.

First, we need to install the lowdb dependency:

```
npm install lowdb
```

Next, we need to create a file for our database. We'll call it `db.js`.

```javascript
const low = require('lowdb');
const FileSync = require('lowdb/adapters/FileSync');

const adapter = new FileSync('db.json');
const db = low(adapter);

// Set some defaults
db.defaults({ todos: [] }).write();

module.exports = db;
```

In the code above, we've imported the dependencies we need and created a file called `db.json` to store our data. We've also created a `todos` array to store our to-dos.

Next, we need to update our server code to use our database.

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

In the code above, we've updated our schema to include a `Todo` type, and we've defined three queries: `todos`, `addTodo` and `toggleTodo`. We've also defined three corresponding resolvers.

The `todos` query will fetch all of the to-dos from our database. The `addTodo` mutation will add a to-do to our database. The `toggleTodo` mutation will toggle the `done` flag for a to-do.

## Adding the front-end

Now that we have our API up and running, let's add a front-end to our application. We'll be using [React](https://reactjs.org/).

First, we need to install the dependencies for our project. We'll be using [Create React App](https://github.com/facebook/create-react-app) to set up our React project.

```
npm install -g create-react-app
create-react-app todo-app
cd todo-app
npm install apollo-boost graphql react-apollo
```

Next, we need to update our `App.js` file.

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

In the code above, we've imported the dependencies we need and created a new Apollo client. We've also defined a query called `GET_TODOS` which will fetch all of the to-dos from our API.

Finally, we've wrapped our `App` component in an `ApolloProvider` and rendered the `GET_TODOS` query using the `Query` component.

If you start the React server by running the following command:

```
npm start
```

and navigate to [http://localhost:3000](http://localhost:3000), you should see the to-dos from our API rendered on the page.

## Adding mutations

Now that we can query our API, let's add the ability to perform mutations. We'll start by adding a form to our `App` component.

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

In the code above, we've imported the `useState` hook from React and we've defined three new mutations: `ADD_TODO`, `TOGGLE_TODO` and `DELETE_TODO`.

We've also updated our `App` component to include a form for adding to-dos, and we've added buttons for toggling and deleting to-dos.

If you navigate to [http://localhost:3000](http://localhost:3000), you should now see a form for adding to-dos, and you should be able to toggle and delete to-dos.

## Conclusion

In this article, we've looked at how to use Node.js, GraphQL and Apollo to build a simple, yet powerful API for our application. We've set up a server, added a database, created a GraphQL schema and resolvers, and added a front-end using React.

Finally, we've added the ability to perform mutations on our data.