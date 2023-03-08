---
title: 008: Using the Observer pattern in functional programming in JavaScript
description: 
published: true
date: 2023-02-17T10:32:34.512Z
tags: 
editor: markdown
dateCreated: 2023-02-17T10:32:33.139Z
---

- [008: 자바스크립트 함수형 프로그래밍에서 옵저버 패턴 사용하기***Korean** document is available*](/ko/Knowledge-base/Functional_JavaScript/Learning/008-using-the-observer-pattern-in-functional-programming-in-javascript)
{.links-list}


# Introduction

JavaScript is a programming language that is widely used in web development. It is also increasingly being used for server-side programming, game development, and mobile development.

Functional programming is a programming paradigm that is based on the mathematical concept of functions. In functional programming, a function is a self-contained piece of code that takes one or more input values and produces an output value.

The Observer pattern is a software design pattern in which an object, called the subject, maintains a list of its observers and notifies them when its state changes.

In this post, we will learn how to use the Observer pattern in functional programming in JavaScript.

# What is the Observer Pattern?

The Observer pattern is a software design pattern in which an object, called the subject, maintains a list of its observers and notifies them when its state changes.

The Observer pattern is also known as the Publish/Subscribe pattern.

The Observer pattern is used in many software applications, including web applications, game applications, and mobile applications.

# How does the Observer Pattern work?

The Observer pattern has three main components: the subject, the observers, and the observer's callback functions.

The subject is an object that maintains a list of its observers. The subject also has a method for attaching observers to its list, and a method for detaching observers from its list.

The observers are objects that register themselves with the subject. The observers also have a method for updating their state, which is called by the subject when the subject's state changes.

The observer's callback functions are functions that are called by the observers when the subject's state changes. The callback functions can be used to update the observers' state.

# How can the Observer Pattern be used in Functional Programming?

The Observer pattern can be used in functional programming to make code more modular and easier to understand.

In functional programming, a function is a self-contained piece of code that takes one or more input values and produces an output value.

By using the Observer pattern, we can create functions that are only concerned with a specific task. For example, we can create a function that calculates the average of a list of numbers, and another function that prints the average to the console.

Both of these functions would be observers of the list of numbers. The list of numbers would be the subject, and it would notify the observers (the average function and the print function) when its state changes (when a new number is added to the list).

# What are the benefits of using the Observer Pattern in Functional Programming?

There are many benefits to using the Observer pattern in functional programming.

Some of the benefits include:

- Modularity: The Observer pattern can be used to create modular code. This means that code can be divided into small, self-contained pieces that can be easily understood and maintained.

- Encapsulation: The Observer pattern can be used to encapsulate code. This means that code can be hidden from the rest of the program, which can make the code easier to understand and maintain.

- Loose coupling: The Observer pattern can be used to create loosely coupled code. This means that code can be written in a way that minimizes the dependencies between different parts of the code. This can make the code easier to understand and maintain.

# Conclusion

In this post, we have learned how to use the Observer pattern in functional programming in JavaScript. We have also seen some of the benefits of using the Observer pattern in functional programming.