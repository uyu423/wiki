---
title: GraphQL
description: 
published: true
date: 2023-02-11T18:17:51.052Z
tags: 
editor: markdown
dateCreated: 2023-02-11T18:17:43.547Z
---

- [GraphQL***Japanese** document is available*](/ja/Knowledge-base/Dictionary/graphql)
{.links-list}
- [GraphQL***Spanish** document is available*](/es/Knowledge-base/Dictionary/graphql)
{.links-list}
- [GraphQL***Chinese Simplified** document is available*](/zh/Knowledge-base/Dictionary/graphql)
{.links-list}
- [GraphQL***Korean** document is available*](/ko/Knowledge-base/Dictionary/graphql)
{.links-list}


# Overview
GraphQL is a query language for APIs and a runtime for fulfilling those queries with existing data. It provides an efficient, powerful, and flexible approach to developing web APIs.

# Description
GraphQL is a query language created by Facebook in 2012 that provides an alternative to REST and ad-hoc web service architectures. It allows clients to define the structure of the data they require, and exactly the same structure of the data is returned from the server. This eliminates the need for multiple API fetches and reduces over-fetching of data, resulting in faster and more efficient applications.

GraphQL is organized into a type system, which defines the relationships between different types of data, and a query language that allows clients to ask for specific fields of data. The GraphQL query language is used to define the data that should be returned from a server. A GraphQL query is sent to an endpoint and the server responds with the data in the requested format.

GraphQL is often used in web and mobile applications, as well as in microservices architectures. It is also used in data-driven applications, such as content management systems, to define the structure of the data that should be returned.

# History
GraphQL was created by Facebook in 2012 as an alternative to the traditional REST architecture. Initially, it was used internally at Facebook to power their mobile applications, but it was later released as open source in 2015. Since then, GraphQL has become increasingly popular and is now used by a wide variety of companies and organizations.

# Features
GraphQL has several features that make it an attractive alternative to traditional REST architectures. These include:

- Self-documenting: GraphQL is self-documenting, meaning that the structure of the data is defined in the query, so the server knows what data to return.
- Flexible: GraphQL is flexible and allows clients to ask for exactly the data they need, eliminating the need for multiple API fetches.
- Efficient: GraphQL queries are efficient, as they only return the data that is requested, reducing over-fetching of data.
- Type System: GraphQL has a type system that defines the relationships between different types of data.

# Example
Here is an example of a GraphQL query:

```
query {
  user(id: "123") {
    name
    age
    email
  }
}
```

This query requests the name, age, and email of the user with the ID "123". The server will then respond with the requested data in the same structure as the query:

```
{
  "user": {
    "name": "John Doe",
    "age": 30,
    "email": "john@example.com"
  }
}
```

# Pros and Cons
GraphQL has several advantages over traditional REST architectures, including flexibility, efficiency, and self-documenting queries. However, it also has some drawbacks, such as the lack of standardization and the need for additional tooling to implement.

# Controversy
GraphQL has been the subject of some controversy, as some developers argue that it is too complex and requires additional tooling to implement.

# Related Technology
GraphQL is often used in conjunction with other technologies, such as Apollo, a platform for building data-driven applications.

# Digression
GraphQL is an increasingly popular technology, and its use is growing rapidly.

# Others
GraphQL is an open source technology, and its source code is available on GitHub.