---
title: Express.js
description: 
published: true
date: 2023-03-12T20:33:00.265Z
tags: 
editor: markdown
dateCreated: 2023-03-12T20:33:00.265Z
---

- [Express.js***Korean** document is available*](/ko/Knowledge-base/Dictionary/express-js)
{.links-list}

# Overview

Express.js is a popular web application framework for Node.js. It provides a robust set of features for building web applications, including routing, middleware, and templating. Express.js is known for its simplicity and flexibility, making it a popular choice for developers of all skill levels.

# Description

Express.js is a minimalist web framework that sits on top of Node.js. It provides a set of tools and features that make it easy to build web applications. Express.js is designed to be simple and flexible, allowing developers to create custom solutions that fit their specific needs.

One of the key features of Express.js is its routing system. The routing system allows developers to define routes for their application, which determines how incoming requests are handled. Express.js also includes a powerful middleware system, which allows developers to add functionality to their application at various stages of the request/response cycle.

Another key feature of Express.js is its templating system. Express.js supports a variety of templating engines, including Pug, EJS, and Handlebars. This allows developers to choose the templating engine that best fits their needs.

Express.js is also known for its extensive library of third-party middleware and plugins. These plugins can add additional functionality to an application, such as authentication, logging, and error handling.

# History

Express.js was created in 2010 by TJ Holowaychuk. Holowaychuk was looking for a simple, lightweight framework for building web applications with Node.js. He created Express.js as a minimalist alternative to the more complex web frameworks that were available at the time.

Since its creation, Express.js has become one of the most popular web frameworks for Node.js. It has been used by companies such as IBM, Uber, and Accenture to build web applications.

# Features

- Routing system: Express.js provides a powerful routing system that allows developers to define routes for their application.
- Middleware system: Express.js includes a middleware system that allows developers to add functionality to their application at various stages of the request/response cycle.
- Templating system: Express.js supports a variety of templating engines, allowing developers to choose the engine that best fits their needs.
- Extensive library of third-party middleware and plugins: Express.js has a large library of third-party middleware and plugins that can add additional functionality to an application.
- Simple and flexible: Express.js is designed to be simple and flexible, allowing developers to create custom solutions that fit their specific needs.

# Example

Here is a simple example of how to use Express.js to create a basic web application:

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello, World!');
});

app.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

In this example, we create a new Express.js application and define a route for the root URL ("/"). When a user visits the root URL, the server sends a "Hello, World!" message in response. We then start the server and listen for incoming requests on port 3000.

# Pros and Cons

## Pros

- Simple and flexible: Express.js is designed to be simple and flexible, allowing developers to create custom solutions that fit their specific needs.
- Large community: Express.js has a large and active community of developers, which means there are plenty of resources and support available.
- Large library of third-party middleware and plugins: Express.js has a large library of third-party middleware and plugins that can add additional functionality to an application.
- Fast: Express.js is known for its speed and performance.

## Cons

- Lack of structure: Express.js is a minimalist framework, which means it doesn't provide much structure or guidance for organizing code. This can lead to messy and hard-to-maintain code.
- Steep learning curve: While Express.js is designed to be simple, it can still have a steep learning curve for developers who are new to Node.js or web development in general.
- Limited out-of-the-box functionality: Express.js is designed to be lightweight, which means it doesn't include many built-in features or functionality. Developers will need to rely on third-party middleware and plugins to add additional functionality to their application.

# Related Technology

Express.js is closely related to Node.js, as it is built on top of the Node.js runtime. Other related technologies include:

- MongoDB: A popular NoSQL database that is often used in conjunction with Express.js.
- Socket.io: A library that allows for real-time communication between the server and client.
- React: A popular frontend library that is often used with Express.js to build full-stack web applications.

# Digression

One of the strengths of Express.js is its flexibility. Because it is a minimalist framework, developers have a lot of freedom to create custom solutions that fit their specific needs. However, this flexibility can also be a weakness, as it can lead to messy and hard-to-maintain code.

To avoid this, it's important to follow best practices for organizing code and using middleware. It's also important to take advantage of the many third-party plugins and middleware that are available for Express.js.

# Others

Overall, Express.js is a powerful and flexible web framework that is well-suited for building web applications with Node.js. While it can have a steep learning curve and may require additional plugins and middleware to add functionality, it is a popular choice for developers of all skill levels.