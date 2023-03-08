---
title: 007: Implementing a functional programming approach in JavaScript frameworks (e.g. React, Angular, Vue)
description: 
published: true
date: 2023-02-17T10:06:38.147Z
tags: 
editor: markdown
dateCreated: 2023-02-17T10:06:31.410Z
---

- [007: JavaScript 프레임워크(예: React, Angular, Vue)에서 함수형 프로그래밍 접근 방식 구현***Korean** document is available*](/ko/Knowledge-base/Functional_JavaScript/Learning/007-implementing-a-functional-programming-approach-in-javascript-frameworks-e-g-react-angular-vue)
{.links-list}


## Introduction

JavaScript is a versatile language that can be used for both functional and object-oriented programming. In recent years, there has been a shift towards functional programming in JavaScript frameworks such as React, Angular, and Vue.

Functional programming is a programming paradigm that emphasizes the use of functions, and the avoidance of side effects. This can make code easier to reason about and debug.

There are many benefits to using a functional programming approach in JavaScript frameworks. In this post, we will take a look at some of these benefits and how to implement a functional programming approach in React, Angular, and Vue.

## Benefits of functional programming

There are many benefits to using a functional programming approach in JavaScript frameworks. Some of these benefits include:

- improved code readability and maintainability;
- easier to reason about and debug;
- better performance;
- more declarative.

## Implementing a functional programming approach in React

React is a popular JavaScript framework for building user interfaces. It uses a declarative syntax that makes code easy to read and understand.

React components are typically written in a functional style. This means that they take props and return React elements.

Here is an example of a functional React component that takes an name prop and returns a React element:

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

This component can be used like this:

```javascript
<Welcome name="Sara" />
```

## Implementing a functional programming approach in Angular

Angular is a popular JavaScript framework for building single-page applications. It uses an imperative syntax that can be challenging to read and understand.

Angular components can be written in a functional style. This means that they take an input and return an output.

Here is an example of a functional Angular component that takes an name input and returns a greeting output:

```javascript
@Component({
  selector: 'app-welcome',
  template: '<h1>Hello, {{name}}</h1>'
})
export class WelcomeComponent {
  @Input() name: string;

  getGreeting() {
    return `Hello, ${this.name}`;
  }
}
```

This component can be used like this:

```javascript
<app-welcome [name]="'Sara'"></app-welcome>
```

## Implementing a functional programming approach in Vue

Vue is a popular JavaScript framework for building user interfaces. It uses a declarative syntax that makes code easy to read and understand.

Vue components are typically written in a functional style. This means that they take props and return a Vue instance.

Here is an example of a functional Vue component that takes a name prop and returns a Vue instance:

```javascript
const Welcome = {
  props: ['name'],
  template: '<h1>Hello, {{name}}</h1>'
};
```

This component can be used like this:

```javascript
<welcome :name="'Sara'"></welcome>
```

## Conclusion

Functional programming is a powerful programming paradigm that can be used to build robust and scalable applications. React, Angular, and Vue are all popular JavaScript frameworks that support functional programming.

If you're interested in learning more about functional programming, check out the resources below.

## Resources

- [Functional Programming in JavaScript](https://medium.com/@cscalfani/functional-programming-in-js-with-es6-pt-i-87d7b8e8e0db)
- [Getting Started with Functional Programming](https://www.sitepoint.com/getting-started-functional-programming/)
- [Why You Should Use Functional Programming in JavaScript](https://medium.com/@mariusc23/why-you-should-use-functional-programming-in-javascript-5b6fe37eecb5)