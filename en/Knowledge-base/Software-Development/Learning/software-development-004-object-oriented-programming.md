---
title: Software Development 004: Object-Oriented Programming
description: 
published: true
date: 2023-02-27T11:32:49.241Z
tags: 
editor: markdown
dateCreated: 2023-02-27T11:32:42.152Z
---

- [소프트웨어 개발 004: 객체 지향 프로그래밍***Korean** document is available*](/ko/Knowledge-base/Software-Development/Learning/software-development-004-object-oriented-programming)
{.links-list}


## Introduction

Object-oriented programming (OOP) is a programming paradigm that organizes code around objects rather than actions and data. In OOP, code is organized into objects that represent data and the actions that can be performed on that data. This paradigm is used in many programming languages, including Java, C++, and Python.

OOP is a powerful programming paradigm that can make code more modular, extensible, and maintainable. It is also often used in large projects where code must be organized in a way that is easy to understand and change.

## What is an Object?

In OOP, an object is a self-contained unit of code that represents data and the actions that can be performed on that data. An object can be thought of as a mini-program that has its own data and code.

 Objects are created from templates called classes. A class is a blueprint for an object. It defines the data and code that will be contained in an object.

## What are the Benefits of Using Objects?

There are several benefits to using objects in your code:

- Objects can make code more modular.
- Objects can make code more extensible.
- Objects can make code more maintainable.
- Objects can make code easier to understand.

## What is Inheritance?

Inheritance is a feature of OOP that allows one object to inherit the data and code of another object. This can be used to create a hierarchy of objects, where each object is a more specialized version of the object above it.

For example, you could have a base class called "Animal" that contains data and code common to all animals. This could include data such as "name" and "weight," and code such as "eat" and "sleep."

You could then create subclasses of "Animal" for specific types of animals, such as "Dog" and "Cat." These subclasses would inherit the data and code of the "Animal" class, but could also contain data and code specific to that type of animal.

## What is Polymorphism?

Polymorphism is a feature of OOP that allows objects to be treated as if they are of a different type. This can be useful when you want to write code that can work with different types of objects without knowing the specific type of object in advance.

For example, you could have a base class called "Shape" that contains data and code common to all shapes. This could include data such as "color" and "size," and code such as "draw" and "resize."

You could then create subclasses of "Shape" for specific types of shapes, such as "Circle" and "Rectangle." These subclasses would inherit the data and code of the "Shape" class, but could also contain data and code specific to that type of shape.

You could then write code that can work with any type of "Shape" object, without knowing the specific type of object in advance. This code would work with "Circle" objects and "Rectangle" objects, as well as any other subclasses of "Shape."

## What is a Class?

A class is a blueprint for an object. It defines the data and code that will be contained in an object.

A class is created using the keyword "class." For example, the following code creates a class called "Animal":

```
class Animal:
    pass
```

## What is an Instance?

An instance is an object that has been created from a class. For example, the following code creates an instance of the "Animal" class:

```
animal = Animal()
```

## What is a Method?

A method is a function that is contained within a class. A method is used to perform an action on the data contained within an object.

A method is created using the keyword "def." For example, the following code creates a method called "eat" that takes one parameter called "food":

```
def eat(self, food):
    pass
```

## What is a Constructor?

A constructor is a special type of method that is used to create an object. A constructor is called when an instance of a class is created.

A constructor is created using the keyword "__init__." For example, the following code creates a constructor for the "Animal" class:

```
def __init__(self, name, weight):
    self.name = name
    self.weight = weight
```

## What is Encapsulation?

Encapsulation is a feature of OOP that allows data to be hidden within an object. This can be used to prevent data from being directly accessed or modified.

Encapsulation is achieved by using the keyword "private." For example, the following code creates a private variable called "__name":

```
class Animal:
    def __init__(self, name, weight):
        self.__name = name
        self.weight = weight
```

## What is a Property?

A property is a special type of variable that is used to access or modify the data within an object. A property is created using the keyword "property." For example, the following code creates a property called "name" that can be used to access or modify the "__name" variable:

```
class Animal:
    def __init__(self, name, weight):
        self.__name = name
        self.weight = weight

    @property
    def name(self):
        return self.__name

    @name.setter
    def name(self, value):
        self.__name = value
```

## What is a Static Method?

A static method is a method that is associated with a class, rather than an object. A static method can be called without creating an instance of the class.

A static method is created using the keyword "staticmethod." For example, the following code creates a static method called "create_animal" that takes two parameters called "name" and "weight":

```
class Animal:
    def __init__(self, name, weight):
        self.__name = name
        self.weight = weight

    @staticmethod
    def create_animal(name, weight):
        return Animal(name, weight)
```

## What is a Class Variable?

A class variable is a variable that is associated with a class, rather than an object. A class variable can be accessed by all instances of the class.

A class variable is created using the keyword "classmethod." For example, the following code creates a class variable called "num_animals" that is incremented each time an "Animal" object is created:

```
class Animal:
    num_animals = 0

    def __init__(self, name, weight):
        self.__name = name
        self.weight = weight
        Animal.num_animals += 1
```

## Conclusion

Object-oriented programming is a powerful programming paradigm that can make code more modular, extensible, and maintainable. It is also often used in large projects where code must be organized in a way that is easy to understand and change.