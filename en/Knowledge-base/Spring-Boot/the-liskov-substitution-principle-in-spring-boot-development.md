---
title: The Liskov Substitution Principle in Spring Boot Development
description: 
published: true
date: 2023-02-08T10:32:34.907Z
tags: 
editor: markdown
dateCreated: 2023-02-08T10:32:28.995Z
---

- [El principio de sustitución de Liskov en el desarrollo de Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/the-liskov-substitution-principle-in-spring-boot-development)
{.links-list}
- [Spring Boot开发中的里氏替换原则***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/the-liskov-substitution-principle-in-spring-boot-development)
{.links-list}
- [Spring Boot 개발의 Liskov 대체 원칙***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/the-liskov-substitution-principle-in-spring-boot-development)
{.links-list}


## Introduction

The Liskov Substitution Principle is a fundamental principle of Object-Oriented Programming which states that derived classes should be substitutable for their base classes. In other words, any method that uses a reference to a base class should work equally well with a reference to any derived class without the need for the programmer to make any changes.

The principle is named after Barbara Liskov, who first formalized it in a 1987 paper entitled "Data Abstraction and Hierarchy".

## What is the Liskov Substitution Principle?

Simply put, the Liskov Substitution Principle states that derived classes should be substitutable for their base classes. In other words, any method that uses a reference to a base class should work equally well with a reference to any derived class without the need for the programmer to make any changes.

The principle is named after Barbara Liskov, who first formalized it in a 1987 paper entitled "Data Abstraction and Hierarchy".

Liskov's paper was inspired by a paper written by David Parnas in 1972 entitled "On the Criteria To Be Used in Decomposing Systems into Modules". In that paper, Parnas presents the "substitution principle", which states that "any module M1 that uses a module M2 can be replaced with another module M3 that uses M2 provided that M3 provides the same abstract interface as M1 to M2".

Liskov's paper generalizes this principle to inheritance, showing that it applies not just to modules but to any hierarchy. She formalizes the principle as follows:

"Let q(x) be a property provable about objects x of type T. Then q(y) should be provable about objects y of type S where S is a subtype of T."

In other words, if a property is true for a base class, it should also be true for all derived classes.

## The Liskov Substitution Principle in Practice

The Liskov Substitution Principle is often violated in practice, especially in legacy code. A common violation is the "brittle base class" problem, where a change to a base class breaks all derived classes.

Another common violation is the "fragile hierarchy" problem, where a change to a derived class breaks the base class.

To avoid these problems, it is important to design your classes in such a way that they adhere to the Liskov Substitution Principle.

One way to do this is to use abstract classes or interfaces instead of concrete classes. This allows you to change the implementation of a class without breaking any code that uses it.

Another way to adhere to the Liskov Substitution Principle is to use composition instead of inheritance. This allows you to change the implementation of a class without breaking any code that uses it.

## The Liskov Substitution Principle in Spring Boot Development

Spring Boot is a popular Java framework that makes it easy to create stand-alone, production-grade Spring-based applications.

The Liskov Substitution Principle is an important principle of Object-Oriented Programming, and Spring Boot adheres to this principle.

For example, Spring Boot uses abstract classes and interfaces instead of concrete classes. This allows you to change the implementation of a class without breaking any code that uses it.

In addition, Spring Boot uses composition instead of inheritance. This allows you to change the implementation of a class without breaking any code that uses it.

## Conclusion

The Liskov Substitution Principle is a fundamental principle of Object-Oriented Programming which states that derived classes should be substitutable for their base classes. In other words, any method that uses a reference to a base class should work equally well with a reference to any derived class without the need for the programmer to make any changes.

The principle is named after Barbara Liskov, who first formalized it in a 1987 paper entitled "Data Abstraction and Hierarchy".

The Liskov Substitution Principle is often violated in practice, especially in legacy code. A common violation is the "brittle base class" problem, where a change to a base class breaks all derived classes.

Another common violation is the "fragile hierarchy" problem, where a change to a derived class breaks the base class.

To avoid these problems, it is important to design your classes in such a way that they adhere to the Liskov Substitution Principle.

One way to do this is to use abstract classes or interfaces instead of concrete classes. This allows you to change the implementation of a class without breaking any code that uses it.

Another way to adhere to the Liskov Substitution Principle is to use composition instead of inheritance. This allows you to change the implementation of a class without breaking any code that uses it.

Spring Boot is a popular Java framework that makes it easy to create stand-alone, production-grade Spring-based applications.

The Liskov Substitution Principle is an important principle of Object-Oriented Programming, and Spring Boot adheres to this principle.

For example, Spring Boot uses abstract classes and interfaces instead of concrete classes. This allows you to change the implementation of a class without breaking any code that uses it.

In addition, Spring Boot uses composition instead of inheritance. This allows you to change the implementation of a class without breaking any code that uses it.