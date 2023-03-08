---
title: 003: Kotlin Basics: Variables, Data Types, and Operators
description: 
published: true
date: 2023-02-07T19:55:58.773Z
tags: 
editor: markdown
dateCreated: 2023-02-07T19:55:57.051Z
---

- [003: Conceptos básicos de Kotlin: variables, tipos de datos y operadores***Spanish** document is available*](/es/Knowledge-base/Kotlin/Learning/003-kotlin-basics-variables-data-types-and-operators)
{.links-list}
- [003：Kotlin 基础知识：变量、数据类型和运算符***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/Learning/003-kotlin-basics-variables-data-types-and-operators)
{.links-list}
- [003: Kotlin 기초: 변수, 데이터 유형 및 연산자***Korean** document is available*](/ko/Knowledge-base/Kotlin/Learning/003-kotlin-basics-variables-data-types-and-operators)
{.links-list}


# Kotlin Basics: Variables, Data Types, and Operators

Kotlin is a statically typed programming language that runs on the JVM. It is a concise, safe, interoperable, and tool-friendly language.

Kotlin is an object-oriented language, and thus, variables must be declared before they can be used. In Kotlin, there are two types of variables:

* Mutable variables: These variables can be changed after they have been initialized. To declare a mutable variable, use the ```var``` keyword.
```kotlin
var name = "John"
name = "Jane" // Valid
```

* Immutable variables: These variables cannot be changed after they have been initialized. To declare an immutable variable, use the ```val``` keyword.
```kotlin
val name = "John"
name = "Jane" // Invalid
```

Kotlin has a null safety feature which eliminates the risk of null pointer exceptions. To allow a variable to hold a null value, you need to declare it as nullable by using the ```?``` symbol.

```kotlin
var name: String? = null
```

Kotlin also has a rich set of operators that can be used on variables. These include:

* Arithmetic operators: ```+```, ```-```, ```*```, ```/```, ```%```
* Assignment operators: ```=```, ```+=```, ```-=```, ```*=```, ```/=```, ```%=```
* Comparison operators: ```==```, ```!=```, ```>```, ```<```, ```>=```, ```<=```
* Logical operators: ```&&```, ```||```, ```!```

Now that you know the basics of Kotlin variables and operators, let's move on to data types.

## Kotlin Data Types

Kotlin has the following data types:

* Numbers: Kotlin has support for both integer and floating-point numbers.
* Characters: Kotlin characters are represented by the ```Char``` type.
* Booleans: Kotlin booleans are represented by the ```Boolean``` type.
* Arrays: Kotlin arrays are represented by the ```Array``` type.
* Strings: Kotlin strings are represented by the ```String``` type.

In addition to the above data types, Kotlin also has a special type called ```Unit```. This type is used to represent a void value.

Now that you know the basics of Kotlin data types, let's move on to Kotlin operators.

## Kotlin Operators

Kotlin has a rich set of operators that can be used on variables. These include:

* Arithmetic operators: ```+```, ```-```, ```*```, ```/```, ```%```
* Assignment operators: ```=```, ```+=```, ```-=```, ```*=```, ```/=```, ```%=```
* Comparison operators: ```==```, ```!=```, ```>```, ```<```, ```>=```, ```<=```
* Logical operators: ```&&```, ```||```, ```!```

Now that you know the basics of Kotlin operators, let's move on to Kotlin control flow.

## Kotlin Control Flow

Kotlin has the following control flow constructs:

* ```if``` expression: Used to evaluate a boolean expression and execute a block of code if the expression is ```true```.
* ```if-else``` expression: Used to evaluate a boolean expression and execute one of two blocks of code, depending on whether the expression is ```true``` or ```false```.
* ```when``` expression: Used to evaluate an expression and execute one of several blocks of code, depending on the value of the expression.
* ```for``` loop: Used to execute a block of code a fixed number of times.
* ```while``` loop: Used to execute a block of code multiple times, until a condition is met.
* ```do-while``` loop: Used to execute a block of code multiple times, until a condition is met. The difference between a ```while``` loop and a ```do-while``` loop is that a ```do-while``` loop will always execute the code block at least once.

Now that you know the basics of Kotlin control flow, let's move on to Kotlin functions.

## Kotlin Functions

A function is a block of code that takes one or more input parameters and produces an output. In Kotlin, functions are declared using the ```fun``` keyword.

Here is a simple function that takes two input parameters and returns the sum of those parameters:

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}
```

If a function does not return a value, its return type should be declared as ```Unit```.

Here is a simple function that takes two input parameters and prints the sum of those parameters:

```kotlin
fun sum(a: Int, b: Int): Unit {
    println(a + b)
}
```

Kotlin also supports higher-order functions, which are functions that take other functions as input parameters. Higher-order functions can be used to create concise and readable code.

Here is a simple higher-order function that takes a function as input and executes that function:

```kotlin
fun execute(f: () -> Unit) {
    f()
}
```

The ```execute``` function above can be used to execute any function that does not take any input parameters and does not return a value.

Now that you know the basics of Kotlin functions, let's move on to Kotlin classes and objects.

## Kotlin Classes and Objects

In Kotlin, a class is a template for creating objects. A class can have properties and methods.

Here is a simple ```Person``` class with two properties: ```name``` and ```age```.

```kotlin
class Person(val name: String, val age: Int)
```

To create an object from a class, you need to use the ```new``` keyword.

```kotlin
val person = new Person("John", 30)
```

Kotlin also supports object-oriented programming. In Kotlin, an object is a singleton - there can only be one instance of an object.

Here is a simple ```Logger``` object with a ```log()``` method.

```kotlin
object Logger {
    fun log(message: String) {
        println(message)
    }
}
```

To use the ```Logger``` object, you do not need to create an instance of it. You can simply call the ```log()``` method directly.

```kotlin
Logger.log("This is a log message")
```

Now that you know the basics of Kotlin classes and objects, you are ready to start programming in Kotlin!