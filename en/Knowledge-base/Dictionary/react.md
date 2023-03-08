---
title: React
description: 
published: true
date: 2023-01-31T13:57:56.446Z
tags: 
editor: markdown
dateCreated: 2023-01-31T13:57:52.912Z
---

- [React***Korean** version of this document is available*](/ko/Knowledge-base/Dictionary/react)
{.links-list}
- [React***Japanese** version of this document is available*](/ja/Knowledge-base/Dictionary/react)
{.links-list}
- [React***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Dictionary/react)
{.links-list}


# Overview
React is a JavaScript library for building user interfaces. It is maintained by Facebook and a community of individual developers and companies. React can be used as a base in the development of single-page or mobile applications.

# History
React was created by Jordan Walke, a software engineer at Facebook. He first released an early prototype of React called "FaxJS" in 2011. The first public release of React was on May 29, 2013. Since then, React has become one of the most popular JavaScript libraries for building user interfaces.

# Description
React is a JavaScript library for building user interfaces. It is used for creating reusable components that can be used in web applications. React is designed to be simple, efficient, and flexible. It uses a declarative programming style, which makes it easier to read and understand.

# Features
React has several features that make it a popular choice for web development. These include:

- **Virtual DOM:** React uses a virtual DOM to efficiently update the UI. This allows React to make changes to the UI without having to re-render the entire page.

- **JSX:** React uses a syntax extension called JSX, which allows developers to write HTML-like syntax in their JavaScript code.

- **React Native:** React Native is a mobile development framework that allows developers to create native apps for iOS and Android using React.

- **Flux:** Flux is an application architecture for React that helps manage data flow within an application.

- **Server-side Rendering:** React supports server-side rendering, which allows developers to render React components on the server before sending them to the client.

# Example
Here is an example of a React component that displays a list of items:

```javascript
import React from 'react';

class List extends React.Component {
  render() {
    return (
      <ul>
        {this.props.items.map(item => (
          <li key={item.id}>{item.name}</li>
        ))}
      </ul>
    );
  }
}
```

# Pros and Cons
React has several advantages, including:

- **Easy to learn:** React is easy to learn and use, making it a great choice for developers of all skill levels.

- **Performance:** React's virtual DOM and server-side rendering make it fast and efficient.

- **Reusable components:** React components are reusable, which makes it easy to create complex user interfaces.

However, there are also some drawbacks to using React, such as:

- **Steep learning curve:** React can be difficult to learn for developers who are new to the library.

- **Lack of documentation:** React's documentation can be difficult to understand, which can make it difficult for developers to get started.

# Controversy
React has been the subject of some controversy due to its use of the JSX syntax. Some developers have argued that JSX is not a "real" programming language and should not be used for web development. Others have argued that JSX is a powerful tool that makes it easier to write complex user interfaces.

# Related Technology
React is often used in conjunction with other technologies, such as:

- **Redux:** Redux is a state management library for React that helps manage data flow within an application.

- **GraphQL:** GraphQL is a query language for APIs that makes it easier to fetch data from a server.

- **TypeScript:** TypeScript is a typed superset of JavaScript that adds type safety to React applications.

# Digression
React has become one of the most popular JavaScript libraries for building user interfaces. It is used by many large companies, such as Facebook, Airbnb, and Netflix. React has also been used to create some of the most popular mobile apps, such as Instagram and Uber.

# Others
React is an open source project and is released under the MIT license. This means that anyone can use React for free, without having to pay any fees or royalties. React is also actively maintained and supported by a large community of developers.