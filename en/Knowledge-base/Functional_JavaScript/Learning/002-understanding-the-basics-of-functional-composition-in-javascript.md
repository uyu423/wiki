---
title: 002: Understanding the basics of functional composition in JavaScript
description: 
published: true
date: 2023-02-17T07:32:22.345Z
tags: 
editor: markdown
dateCreated: 2023-02-17T07:32:15.674Z
---

- [002: JavaScript의 기능적 구성의 기본 이해***Korean** document is available*](/ko/Knowledge-base/Functional_JavaScript/Learning/002-understanding-the-basics-of-functional-composition-in-javascript)
{.links-list}


Functional composition is a powerful technique that can help you write more concise, maintainable code. In this post, we'll take a look at what functional composition is and how you can use it in your JavaScript code.

Functional composition is a way of combining two or more functions to create a new function. The resulting function is a composition of the input functions. This is different from function chaining, where each function is called on the result of the previous function.

Composition is a fundamental principle of functional programming. It allows you to build complex functionality by combining simple functions. Composition is often used to create higher-order functions.

To understand how composition works, let's look at a simple example. Say we have a function that converts a string to upper case:

```javascript
function toUpperCase(str) {
  return str.toUpperCase();
}
```

We can use this function to create a new function that converts a string to lower case:

```javascript
function toLowerCase(str) {
  return str.toLowerCase();
}
```

Now we have two functions that perform opposite operations. We can use composition to create a new function that converts a string to title case:

```javascript
function toTitleCase(str) {
  return toUpperCase(toLowerCase(str));
}
```

In this example, we've used composition to create a new function by combining two existing functions. The resulting function is a composition of the input functions.

Composition is a powerful technique that can help you write more concise, maintainable code. In this post, we've looked at what functional composition is and how you can use it in your JavaScript code.