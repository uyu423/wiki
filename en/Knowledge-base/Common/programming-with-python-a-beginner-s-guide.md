---
title: Programming with Python: A Beginner's Guide
description: 
published: true
date: 2023-02-01T14:25:10.608Z
tags: 
editor: markdown
dateCreated: 2023-02-01T14:25:07.046Z
---

- [Python 프로그래밍: 초보자 가이드***Korean** version of this document is available*](/ko/Knowledge-base/Common/programming-with-python-a-beginner-s-guide)
{.links-list}
- [使用 Python 编程：初学者指南***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Common/programming-with-python-a-beginner-s-guide)
{.links-list}



# Programming with Python: A Beginner's Guide

Python is a versatile language that you can use on the backend, frontend, or full stack of a web application. In this guide, we'll show you how to get started with Python programming.

## Why Python?

Python is a popular language for web development, scientific computing, artificial intelligence, and more. It's easy to learn for beginners and has many modules and libraries that allow for robust development.

## Installing Python

Before you can start programming in Python, you need to install it on your computer. You can download Python from the [official Python website](https://www.python.org/).

Once you have downloaded and installed Python, you can check if it is working by opening your command line interface and typing `python`. If Python is installed, you should see something like this:

```
Python 3.7.4 (default, Aug 13 2019, 15:17:50) 
[Clang 4.0.1 (tags/RELEASE_401/final)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

If you see this, you are ready to start programming in Python. If you don't see this, make sure that you have installed Python correctly and that it is added to your system path.

## Python Syntax

Python is a high-level, interpreted language. This means that it is abstracted from the details of the hardware and operating system. Python code is organized into modules and packages. A module is a file that contains Python code. A package is a collection of modules.

Python code is read by the interpreter and executed line by line. The interpreter can be invoked from the command line by typing `python`. This will open the Python interpreter in interactive mode. In interactive mode, you can type Python code and the interpreter will execute it immediately.

To exit the Python interpreter, type `exit()`.

Python code can also be executed from a Python file. A Python file is a text file with the extension `.py`. To execute a Python file, type `python` followed by the path to the file. For example, if you have a file `hello.py` in your current directory, you can execute it by typing `python hello.py`.

## Hello, World!

Now that you know how to install and run Python, let's write our first program. We'll start with the classic "Hello, World!" program.

Open your favorite text editor and create a new file called `hello.py`. Add the following code to the file:

```python
print("Hello, World!")
```

Save the file and close the text editor. Then, open your command line interface and navigate to the directory where `hello.py` is saved. Type `python hello.py` to execute the program. You should see the following output:

```
Hello, World!
```

Congratulations! You've just written your first Python program.

## Variables

In Python, variables are used to store values. A value can be a string, a number, a list, or any other data type. To create a variable, you just need to specify the name of the variable and the value you want to store in it. For example:

```python
message = "Hello, World!"
```

In the example above, we create a variable called `message` and store the string `"Hello, World!"` in it. We can then access the value of the variable by using the variable name:

```python
print(message)
```

will print `Hello, World!`.

You can also change the value of a variable by reassigning it:

```python
message = "Hello, Python!"
```

Now, if we print `message`, we will see `Hello, Python!`.

It's important to choose variable names that are descriptive and easy to remember. For example, `message` is a good name for a variable that stores a string. A variable called `x` is not a good name because it doesn't tell us anything about what the variable is used for.

## Data Types

In Python, there are several built-in data types:

* `int`: Integer values. For example: `1`, `-5`, `0`.
* `float`: Floating point values. For example: `1.0`, `-5.0`, `0.0`.
* `str`: String values. For example: `"Hello, World!"`, `"Python"`.
* `bool`: Boolean values. For example: `True`, `False`.
* `list`: A list of values. For example: `[1, 2, 3]`, `["a", "b", "c"]`.
* `dict`: A dictionary of values. For example: `{"a": 1, "b": 2, "c": 3}`.

You can find out the type of a value using the `type()` function:

```python
>>> type(1)
<class 'int'>
>>> type(1.0)
<class 'float'>
>>> type("Hello, World!")
<class 'str'>
>>> type(True)
<class 'bool'>
>>> type([1, 2, 3])
<class 'list'>
>>> type({"a": 1, "b": 2, "c": 3})
<class 'dict'>
```

It's important to know the data type of a value because different data types have different properties and functions. For example, `int` values have mathematical functions like `abs()` and `pow()` that can be used on them, while `str` values have string functions like `upper()` and `lower()`.

## Lists

Lists are a type of data structure that allows you to store multiple values in a single variable. A list is created by putting values inside square brackets `[]`. For example:

```python
>>> my_list = [1, 2, 3]
>>> my_list
[1, 2, 3]
```

You can access the values in a list by using their index. An index is a number that specifies the position of a value in a list. The first value in a list has an index of `0`, the second value has an index of `1`, and so on. For example:

```python
>>> my_list[0]
1
>>> my_list[1]
2
>>> my_list[2]
3
```

You can also use negative indices to access values from the end of the list. For example, the index `-1` refers to the last value in the list, `-2` refers to the second to last value, and so on. For example:

```python
>>> my_list[-1]
3
>>> my_list[-2]
2
>>> my_list[-3]
1
```

You can add values to a list using the `append()` function:

```python
>>> my_list.append(4)
>>> my_list
[1, 2, 3, 4]
```

You can remove values from a list using the `remove()` function:

```python
>>> my_list.remove(2)
>>> my_list
[1, 3, 4]
```

You can also sort a list using the `sort()` function:

```python
>>> my_list.sort()
>>> my_list
[1, 3, 4]
```

There are many other functions that you can use on lists. You can find a full list of them in the [Python documentation](https://docs.python.org/3/tutorial/datastructures.html).

## Loops

A loop is a type of control flow statement that allows you to execute a block of code multiple times. In Python, there are two types of loops: `for` loops and `while` loops.

A `for` loop is used to iterate over a sequence of values. For example, you can use a `for` loop to print each value in a list:

```python
>>> my_list = [1, 2, 3, 4]
>>> for value in my_list:
...     print(value)
... 
1
2
3
4
```

The code above will print `1`, `2`, `3`, and `4` on separate lines.

A `while` loop is used to execute a block of code until a condition is met. For example, you can use a `while` loop to print a list of numbers until a certain number is reached:

```python
>>> num = 1
>>> while num <= 10:
...     print(num)
...     num = num + 1
... 
1
2
3
4
5
6
7
8
9
10
```

The code above will print the numbers `1` through `10` on separate lines.

## Conditionals

A conditional is a type of control flow statement that allows you to execute a block of code only if a certain condition is met. In Python, there are three types of conditionals: `if` statements, `elif` statements, and `else` statements.

An `if` statement is used to execute a block of code only if a certain condition is `True`. For example, you can use an `if` statement to print a message only if a certain number is positive:

```python
>>> num = 1
>>> if num > 0:
...     print("The number is positive.")
... 
The number is positive.
```

An `elif` statement is used to execute a block of code only if a certain condition is `True` and the previous `if` statement was `False`. For example, you can use an `elif` statement to print a different message if the number is negative:

```python
>>> num = -1
>>> if num > 0:
...     print("The number is positive.")
... elif num < 0:
...     print("The number is negative.")
... 
The number is negative.
```

An `else` statement is used to execute a block of code only if all of the previous `if` and `elif` statements were `False`. For example, you can use an `else` statement to print a message if the number is `0`:

```python
>>> num = 0
>>> if num > 0:
...     print("The number is positive.")
... elif num < 0:
...     print("The number is negative.")
... else:
...     print("The number is zero.")
... 
The number is zero.
```

## Functions

A function is a block of code that can be executed multiple times. In Python, you can define your own functions using the `def` keyword. For example, you can define a function to print a message:

```python
>>> def print_message():
...     print("Hello, World!")
... 
>>> print_message()
Hello, World!
```

You can also pass arguments to a function. Arguments are values that are passed to a function when it is called. For example, you can define a function to print a message with a custom string:

```python
>>> def print_message(message):
...     print(message)
... 
>>> print_message("Hello, World!")
Hello, World!
```

You can also return values from a function. A return value is a value that is passed back to the code that called the function. For example, you can define a function to calculate the sum of two numbers:

```python
>>> def add(num1, num2):
...     return num1 + num2
... 
>>> add(1, 2)
3
```

## Classes

A class is a template for creating objects. An object is a data structure that has its own variables and functions. In Python, you can define your own classes using the `class` keyword. For example, you can define a class to represent a point in two-dimensional space:

```python
>>> class Point:
...     def __init__(self, x, y):
...         self.x = x
...         self.y = y
... 
>>> point = Point(1, 2)
>>> print(point.x)
1
>>> print(point.y)
2
```

In the code above, we define a class called `Point`. The `__init__()` function is a special function that is used to initialize the object. The `self` keyword is used to refer to the object itself. The `x` and `y` variables are called attributes of the object.

We then create an object called `point` and print its `x` and `y` attributes.

You can also define functions inside a class. These functions are called methods of the class. For example, you can define a method to calculate the distance between two points:

```python
>>> class Point:
...     def __init__(self, x, y):
...         self.x = x
...         self.y = y
... 
...     def distance(self, other):
...         return ((self.x - other.x)**2 + (self.y - other.y)**2)**0.5
... 
>>> point1 = Point(1, 2)
>>> point2 = Point(4, 6)
>>> print(point1.distance(point2))
5.0
```

In the code above, we define a method called `distance()` that calculates the distance between two points. We then create two objects and print the distance between them.

## Resources

This guide has only covered the basics of Python programming. To learn more about Python, check out the following resources:

* [The official Python tutorial](https://docs.python.org/3/tutorial/)
* [The official Python documentation](https://docs.python.org/3/)
* [Learn Python the Hard Way](https://learnpythonthehardway.org/python3/)
* [A Byte of Python](https://python.swaroopch.com/)
* [Python for You](https://pythonyou.com/)