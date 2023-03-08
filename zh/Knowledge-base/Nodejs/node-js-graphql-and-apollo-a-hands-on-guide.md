---
title: Node.js、GraphQL 和 Apollo：动手指南
description: 
published: true
date: 2023-02-06T09:57:15.337Z
tags: 
editor: markdown
dateCreated: 2023-02-06T09:57:13.682Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Node.js, GraphQL and Apollo: A Hands-On Guide***English** document is available*](/en/Knowledge-base/Nodejs/node-js-graphql-and-apollo-a-hands-on-guide)
{.links-list}


# Node.js、GraphQL 和 Apollo：动手指南

## 介绍

在本文中，我们将研究如何使用 Node.js、GraphQL 和 Apollo 为我们的应用程序构建一个简单但功能强大的 API。我们将构建一个简单的待办事项应用程序，API 将为前端界面提供支持。

我们将使用以下技术：

- [Node.js](https://nodejs.org/)
- [GraphQL](https://graphql.org/)
- [阿波罗](https://www.apollographql.com/)

## 什么是 Node.js？

Node.js 是一个基于 Chrome 的 V8 JavaScript 引擎构建的 JavaScript 运行时。 Node.js 使用事件驱动、非阻塞 I/O 模型，使其轻量级且高效。

Node.js 是构建高度可扩展的网络应用程序的理想平台。

## 什么是 GraphQL？

GraphQL 是一种用于 API 的查询语言，也是一种服务器端运行时，用于使用您为数据定义的类型系统来执行查询。 GraphQL 不依赖于任何特定的数据库或存储引擎，而是由您现有的代码和数据支持。

GraphQL 为您的 API 中的数据提供了完整且易于理解的描述，使客户能够准确地询问他们需要什么，仅此而已，随着时间的推移更容易发展 API，并启用强大的开发人员工具。

## 什么是阿波罗？

Apollo 是一组工具，可以更轻松地构建 GraphQL 应用程序。它包括客户端和服务器，并绑定了 React、Angular、Vue.js 等流行框架。

## 设置我们的项目

让我们从设置我们的项目开始。我们将使用 [Express](https://expressjs.com/) 框架来构建我们的服务器。

首先，我们需要为我们的项目安装依赖项。我们将使用 [npm](https://www.npmjs.com/) 来安装我们的依赖项。

```
npm install express graphql apollo-server-express
```

接下来，我们需要为我们的服务器创建一个文件。我们将其称为“server.js”。

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

在上面的代码中，我们导入了所需的依赖项，创建了一个 Express 服务器并定义了我们的 GraphQL 模式。我们还为我们的“hello”查询定义了一个解析器。

最后，我们在端口 4000 上启动了我们的服务器。

您可以通过运行以下命令来启动服务器：

```
node server.js
```

如果您导航到 [http://localhost:4000/graphql](http://localhost:4000/graphql)，您应该会看到 GraphQL Playground，您可以在其中对您的 API 运行查询。

尝试运行以下查询：

```graphql
query {
  hello
}
```

您应该会看到以下结果：

```json
{
  "data": {
    "hello": "Hello World!"
  }
}
```

## 添加数据

现在我们已经启动并运行了服务器，让我们向 API 添加一些数据。我们将使用 [lowdb](https://github.com/typicode/lowdb) 库来存储我们的数据。

首先，我们需要安装 lowdb 依赖项：

```
npm install lowdb
```

接下来，我们需要为我们的数据库创建一个文件。我们称它为 `db.js`。

```javascript
const low = require('lowdb');
const FileSync = require('lowdb/adapters/FileSync');

const adapter = new FileSync('db.json');
const db = low(adapter);

// Set some defaults
db.defaults({ todos: [] }).write();

module.exports = db;
```

在上面的代码中，我们导入了所需的依赖项并创建了一个名为“db.json”的文件来存储我们的数据。我们还创建了一个 `todos` 数组来存储我们的待办事项。

接下来，我们需要更新服务器代码以使用我们的数据库。

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

在上面的代码中，我们更新了我们的架构以包含一个“Todo”类型，并且我们定义了三个查询：“todos”、“addTodo”和“toggleTodo”。我们还定义了三个相应的解析器。

`todos` 查询将从我们的数据库中获取所有待办事项。 `addTodo` 突变将向我们的数据库添加待办事项。 `toggleTodo` 突变将切换待办事项的 `done` 标志。

## 添加前端

现在我们已经启动并运行了我们的 API，让我们向我们的应用程序添加一个前端。我们将使用 [React](https://reactjs.org/)。

首先，我们需要为我们的项目安装依赖项。我们将使用 [Create React App](https://github.com/facebook/create-react-app) 来设置我们的 React 项目。

```
npm install -g create-react-app
create-react-app todo-app
cd todo-app
npm install apollo-boost graphql react-apollo
```

接下来，我们需要更新我们的 App.js 文件。

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

在上面的代码中，我们导入了所需的依赖项并创建了一个新的 Apollo 客户端。我们还定义了一个名为“GET_TODOS”的查询，它将从我们的 API 中获取所有待办事项。

最后，我们将 `App` 组件包装在 `ApolloProvider` 中，并使用 `Query` 组件呈现 `GET_TODOS` 查询。

如果通过运行以下命令启动 React 服务器：

```
npm start
```

并导航至 [http://localhost:3000](http://localhost:3000)，您应该会在页面上看到 API 中的待办事项。

## 添加突变

现在我们可以查询我们的 API，让我们添加执行突变的能力。我们将从向我们的 App 组件添加一个表单开始。

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

在上面的代码中，我们从 React 导入了 useState 钩子，并定义了三个新的突变：ADD_TODO、TOGGLE_TODO 和 DELETE_TODO。

我们还更新了“App”组件以包含用于添加待办事项的表单，并且添加了用于切换和删除待办事项的按钮。

如果您导航到 [http://localhost:3000](http://localhost:3000)，您现在应该会看到一个用于添加待办事项的表单，并且您应该能够切换和删除待办事项。

## 结论

在本文中，我们了解了如何使用 Node.js、GraphQL 和 Apollo 为我们的应用程序构建一个简单但功能强大的 API。我们设置了一个服务器，添加了一个数据库，创建了一个 GraphQL 模式和解析器，并添加了一个使用 React 的前端。

最后，我们添加了对数据执行突变的功能。