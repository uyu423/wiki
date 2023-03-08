---
title: Node.js, GraphQL 및 Apollo: 실습 가이드
description: 
published: true
date: 2023-02-06T09:57:15.430Z
tags: 
editor: markdown
dateCreated: 2023-02-06T09:57:13.683Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Node.js, GraphQL and Apollo: A Hands-On Guide***English** document is available*](/en/Knowledge-base/Nodejs/node-js-graphql-and-apollo-a-hands-on-guide)
{.links-list}


# Node.js, GraphQL 및 Apollo: 실습 가이드

## 소개

이 기사에서는 Node.js, GraphQL 및 Apollo를 사용하여 애플리케이션을 위한 간단하면서도 강력한 API를 구축하는 방법을 살펴보겠습니다. 우리는 간단한 할 일 애플리케이션을 구축할 것이며 API는 프런트 엔드 인터페이스를 강화할 것입니다.

우리는 다음과 같은 기술을 사용할 것입니다.

- [Node.js](https://nodejs.org/)
- [GraphQL](https://graphql.org/)
- [아폴로](https://www.apollographql.com/)

## Node.js가 무엇인가요?

Node.js는 Chrome의 V8 JavaScript 엔진에 구축된 JavaScript 런타임입니다. Node.js는 가볍고 효율적인 이벤트 중심의 비차단 I/O 모델을 사용합니다.

Node.js는 확장성이 뛰어난 네트워크 애플리케이션을 구축하기 위한 이상적인 플랫폼입니다.

## GraphQL이란?

GraphQL은 API용 쿼리 언어이며 데이터에 대해 정의한 유형 시스템을 사용하여 쿼리를 실행하기 위한 서버 측 런타임입니다. GraphQL은 특정 데이터베이스 또는 스토리지 엔진에 연결되지 않으며 대신 기존 코드 및 데이터로 지원됩니다.

GraphQL은 API의 데이터에 대한 완전하고 이해하기 쉬운 설명을 제공하고 클라이언트에게 필요한 것을 정확히 요청할 수 있는 권한을 제공하며 시간이 지남에 따라 API를 더 쉽게 발전시키고 강력한 개발자 도구를 사용할 수 있도록 합니다.

## 아폴로란?

Apollo는 GraphQL 애플리케이션을 보다 쉽게 구축할 수 있는 도구 세트입니다. 여기에는 클라이언트와 서버가 포함되며 React, Angular, Vue.js 등과 같은 인기 있는 프레임워크에 대한 바인딩이 있습니다.

## 프로젝트 설정

프로젝트를 설정하여 시작하겠습니다. [Express](https://expressjs.com/) 프레임워크를 사용하여 서버를 구축할 것입니다.

먼저 프로젝트에 대한 종속성을 설치해야 합니다. [npm](https://www.npmjs.com/)을 사용하여 종속성을 설치합니다.

```
npm install express graphql apollo-server-express
```

다음으로 서버용 파일을 만들어야 합니다. 우리는 그것을 `server.js`라고 부를 것입니다.

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

위의 코드에서 필요한 종속 항목을 가져오고 Express 서버를 만들고 GraphQL 스키마를 정의했습니다. 또한 `hello` 쿼리에 대한 리졸버도 정의했습니다.

마지막으로 포트 `4000`에서 서버를 시작했습니다.

다음 명령을 실행하여 서버를 시작할 수 있습니다.

```
node server.js
```

[http://localhost:4000/graphql](http://localhost:4000/graphql)로 이동하면 API에 대해 쿼리를 실행할 수 있는 GraphQL Playground가 표시됩니다.

다음 쿼리를 실행해 보십시오.

```graphql
query {
  hello
}
```

다음 결과가 표시됩니다.

```json
{
  "data": {
    "hello": "Hello World!"
  }
}
```

## 데이터 추가

이제 서버를 가동하고 실행 중이므로 API에 일부 데이터를 추가해 보겠습니다. [lowdb](https://github.com/typicode/lowdb) 라이브러리를 사용하여 데이터를 저장합니다.

먼저 lowdb 종속성을 설치해야 합니다.

```
npm install lowdb
```

다음으로 데이터베이스용 파일을 만들어야 합니다. 우리는 이것을 `db.js`라고 부를 것입니다.

```javascript
const low = require('lowdb');
const FileSync = require('lowdb/adapters/FileSync');

const adapter = new FileSync('db.json');
const db = low(adapter);

// Set some defaults
db.defaults({ todos: [] }).write();

module.exports = db;
```

위의 코드에서 필요한 종속 항목을 가져오고 데이터를 저장하기 위해 `db.json`이라는 파일을 만들었습니다. 우리는 또한 할 일을 저장하기 위해 `todos` 배열을 만들었습니다.

다음으로 데이터베이스를 사용하도록 서버 코드를 업데이트해야 합니다.

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

위의 코드에서 `Todo` 유형을 포함하도록 스키마를 업데이트했으며 `todos`, `addTodo` 및 `toggleTodo`의 세 가지 쿼리를 정의했습니다. 우리는 또한 3개의 상응하는 리졸버를 정의했습니다.

`todos` 쿼리는 데이터베이스에서 모든 할 일을 가져옵니다. `addTodo` 변형은 데이터베이스에 할 일을 추가합니다. `toggleTodo` 변형은 할 일에 대한 `done` 플래그를 토글합니다.

## 프런트 엔드 추가

이제 API가 실행 중이므로 애플리케이션에 프런트 엔드를 추가해 보겠습니다. 우리는 [React](https://reactjs.org/)를 사용할 것입니다.

먼저 프로젝트에 대한 종속성을 설치해야 합니다. [Create React App](https://github.com/facebook/create-react-app)을 사용하여 React 프로젝트를 설정할 것입니다.

```
npm install -g create-react-app
create-react-app todo-app
cd todo-app
npm install apollo-boost graphql react-apollo
```

다음으로 `App.js` 파일을 업데이트해야 합니다.

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

위의 코드에서 필요한 종속 항목을 가져오고 새 Apollo 클라이언트를 만들었습니다. 또한 API에서 모든 할 일을 가져오는 `GET_TODOS`라는 쿼리를 정의했습니다.

마지막으로 `App` 구성 요소를 `ApolloProvider`에 래핑하고 `Query` 구성 요소를 사용하여 `GET_TODOS` 쿼리를 렌더링했습니다.

다음 명령을 실행하여 React 서버를 시작하는 경우:

```
npm start
```

[http://localhost:3000](http://localhost:3000)으로 이동하면 페이지에 렌더링된 API의 할 일이 표시됩니다.

## 돌연변이 추가

이제 API를 쿼리할 수 있으므로 변형을 수행하는 기능을 추가해 보겠습니다. `App` 구성 요소에 양식을 추가하여 시작하겠습니다.

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

위의 코드에서 우리는 React에서 `useState` 후크를 가져왔고 `ADD_TODO`, `TOGGLE_TODO` 및 `DELETE_TODO`의 세 가지 새로운 변이를 정의했습니다.

또한 할 일을 추가하기 위한 양식을 포함하도록 `App` 구성 요소를 업데이트했으며 할 일 전환 및 삭제를 위한 버튼을 추가했습니다.

[http://localhost:3000](http://localhost:3000)으로 이동하면 이제 할일 추가 양식이 표시되고 할일을 전환 및 삭제할 수 있습니다.

## 결론

이 기사에서는 Node.js, GraphQL 및 Apollo를 사용하여 애플리케이션을 위한 간단하면서도 강력한 API를 구축하는 방법을 살펴보았습니다. 우리는 서버를 설정하고, 데이터베이스를 추가하고, GraphQL 스키마와 리졸버를 생성하고, React를 사용하여 프런트 엔드를 추가했습니다.

마지막으로 데이터에 대한 변형을 수행하는 기능을 추가했습니다.