---
title: 使用 Python 编程：初学者指南
description: 
published: true
date: 2023-02-01T14:25:08.599Z
tags: 
editor: markdown
dateCreated: 2023-02-01T14:25:07.076Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Programming with Python: A Beginner's Guide***English** version of this document is available*](/en/Knowledge-base/Common/programming-with-python-a-beginner-s-guide)
{.links-list}



# 使用 Python 编程：初学者指南

Python 是一种多功能语言，您可以在 Web 应用程序的后端、前端或完整堆栈上使用它。在本指南中，我们将向您展示如何开始使用 Python 编程。

## 为什么选择 Python？

Python 是 Web 开发、科学计算、人工智能等领域的流行语言。它对初学者来说很容易学习，并且有许多模块和库可以进行稳健的开发。

## 安装 Python

在开始使用 Python 编程之前，您需要在计算机上安装它。您可以从 [Python 官方网站](https://www.python.org/) 下载 Python。

下载并安装 Python 后，您可以通过打开命令行界面并输入 `python` 来检查它是否正常工作。如果安装了 Python，您应该会看到如下内容：

```
Python 3.7.4 (default, Aug 13 2019, 15:17:50) 
[Clang 4.0.1 (tags/RELEASE_401/final)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

如果你看到这个，你就可以开始用 Python 编程了。如果您没有看到它，请确保您已正确安装 Python 并将其添加到您的系统路径中。

## Python 语法

Python 是一种高级解释型语言。这意味着它是从硬件和操作系统的细节中抽象出来的。 Python 代码被组织成模块和包。模块是包含 Python 代码的文件。包是模块的集合。

Python 代码由解释器读取并逐行执行。可以通过键入“python”从命令行调用解释器。这将以交互模式打开 Python 解释器。在交互模式下，您可以键入 Python 代码，解释器将立即执行它。

要退出 Python 解释器，请键入 exit() 。

Python 代码也可以从 Python 文件中执行。 Python 文件是扩展名为“.py”的文本文件。要执行 Python 文件，请键入 `python` 后跟文件路径。例如，如果您的当前目录中有一个文件“hello.py”，您可以通过键入“python hello.py”来执行它。

## 你好世界！

现在您已经知道如何安装和运行 Python，让我们来编写我们的第一个程序。我们将从经典的“Hello, World!”开始。程序。

打开您最喜欢的文本编辑器并创建一个名为“hello.py”的新文件。将以下代码添加到文件中：

```python
print("Hello, World!")
```

保存文件并关闭文本编辑器。然后，打开命令行界面并导航到保存“hello.py”的目录。输入 `python hello.py` 来执行程序。您应该看到以下输出：

```
Hello, World!
```

恭喜！您刚刚编写了您的第一个 Python 程序。

## 变量

在 Python 中，变量用于存储值。值可以是字符串、数字、列表或任何其他数据类型。要创建一个变量，您只需要指定变量的名称和要存储在其中的值。例如：

```python
message = "Hello, World!"
```

在上面的示例中，我们创建了一个名为“message”的变量，并将字符串“Hello, World!”存储在其中。然后我们可以使用变量名访问变量的值：

```python
print(message)
```

将打印 `Hello, World!`。

您还可以通过重新分配来更改变量的值：

```python
message = "Hello, Python!"
```

现在，如果我们打印 `message`，我们将看到 `Hello, Python!`。

选择具有描述性且易于记忆的变量名称很重要。例如，“message”是存储字符串的变量的好名称。名为 `x` 的变量不是一个好名字，因为它没有告诉我们任何有关该变量的用途的信息。

## 数据类型

在 Python 中，有几种内置数据类型：

* `int`：整数值。例如：`1`、`-5`、`0`。
* `float`：浮点值。例如：`1.0`、`-5.0`、`0.0`。
* `str`：字符串值。例如：“你好，世界！”，“Python”。
* `bool`: 布尔值。例如：`True`、`False`。
* `list`: 值列表。例如：`[1, 2, 3]`, `["a", "b", "c"]`。
* `dict`：值字典。例如：`{"a": 1, "b": 2, "c": 3}`。

您可以使用 type() 函数找出值的类型：

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

了解值的数据类型很重要，因为不同的数据类型具有不同的属性和功能。例如，“int”值具有可用于它们的数学函数，如“abs()”和“pow()”，而“str”值具有字符串函数，如“upper()”和“lower()”。

## 列表

列表是一种数据结构，允许您将多个值存储在单个变量中。通过将值放在方括号“[]”中来创建列表。例如：

```python
>>> my_list = [1, 2, 3]
>>> my_list
[1, 2, 3]
```

您可以使用索引访问列表中的值。索引是一个数字，它指定值在列表中的位置。列表中的第一个值的索引为“0”，第二个值的索引为“1”，依此类推。例如：

```python
>>> my_list[0]
1
>>> my_list[1]
2
>>> my_list[2]
3
```

您还可以使用负索引从列表末尾访问值。例如，索引“-1”表示列表中的最后一个值，“-2”表示倒数第二个值，依此类推。例如：

```python
>>> my_list[-1]
3
>>> my_list[-2]
2
>>> my_list[-3]
1
```

您可以使用 `append()` 函数将值添加到列表中：

```python
>>> my_list.append(4)
>>> my_list
[1, 2, 3, 4]
```

您可以使用 `remove()` 函数从列表中删除值：

```python
>>> my_list.remove(2)
>>> my_list
[1, 3, 4]
```

您还可以使用 `sort()` 函数对列表进行排序：

```python
>>> my_list.sort()
>>> my_list
[1, 3, 4]
```

您可以在列表上使用许多其他功能。您可以在 [Python 文档](https://docs.python.org/3/tutorial/datastructures.html) 中找到它们的完整列表。

## 循环

循环是一种控制流语句，允许您多次执行一个代码块。在 Python 中，有两种类型的循环：`for` 循环和`while` 循环。

`for` 循环用于迭代一系列值。例如，您可以使用 `for` 循环打印列表中的每个值：

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

上面的代码将在不同的行上打印“1”、“2”、“3”和“4”。

`while` 循环用于执行代码块，直到满足条件。例如，您可以使用 while 循环来打印数字列表，直到达到某个数字：

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

上面的代码将在不同的行上打印数字“1”到“10”。

## 条件

条件是一种控制流语句，它允许您仅在满足特定条件时才执行代码块。在 Python 中，存在三种类型的条件语句：`if` 语句、`elif` 语句和 `else` 语句。

仅当特定条件为“真”时，“if”语句才用于执行代码块。例如，您可以使用 if 语句仅在特定数字为正数时打印消息：

```python
>>> num = 1
>>> if num > 0:
...     print("The number is positive.")
... 
The number is positive.
```

仅当特定条件为“真”且前一个“if”语句为“假”时，“elif”语句才用于执行代码块。例如，如果数字为负数，您可以使用 elif 语句打印不同的消息：

```python
>>> num = -1
>>> if num > 0:
...     print("The number is positive.")
... elif num < 0:
...     print("The number is negative.")
... 
The number is negative.
```

仅当所有先前的 if 和 elif 语句都为 False 时，else 语句才用于执行代码块。例如，如果数字为“0”，您可以使用“else”语句打印一条消息：

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

## 职能

函数是可以多次执行的代码块。在 Python 中，您可以使用 def 关键字定义自己的函数。例如，您可以定义一个函数来打印消息：

```python
>>> def print_message():
...     print("Hello, World!")
... 
>>> print_message()
Hello, World!
```

您还可以将参数传递给函数。参数是调用函数时传递给函数的值。例如，您可以定义一个函数来打印带有自定义字符串的消息：

```python
>>> def print_message(message):
...     print(message)
... 
>>> print_message("Hello, World!")
Hello, World!
```

您还可以从函数返回值。返回值是传递回调用函数的代码的值。例如，您可以定义一个函数来计算两个数字的总和：

```python
>>> def add(num1, num2):
...     return num1 + num2
... 
>>> add(1, 2)
3
```

## 课程

类是创建对象的模板。对象是一种数据结构，它有自己的变量和函数。在 Python 中，您可以使用“class”关键字定义自己的类。例如，您可以定义一个类来表示二维空间中的一个点：

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

在上面的代码中，我们定义了一个名为“Point”的类。 `__init__()` 函数是一个用于初始化对象的特殊函数。 `self` 关键字用于引用对象本身。 `x` 和 `y` 变量称为对象的属性。

然后我们创建一个名为“point”的对象并打印其“x”和“y”属性。

您还可以在类中定义函数。这些函数称为类的方法。例如，您可以定义一个方法来计算两点之间的距离：

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

在上面的代码中，我们定义了一个名为“distance()”的方法来计算两点之间的距离。然后我们创建两个对象并打印它们之间的距离。

## 资源

本指南仅涵盖了 Python 编程的基础知识。要了解有关 Python 的更多信息，请查看以下资源：

* [Python官方教程](https://docs.python.org/3/tutorial/)
* [Python 官方文档](https://docs.python.org/3/)
* [艰难地学习 Python](https://learnpythonthehardway.org/python3/)
* [Python 简介](https://python.swaroopch.com/)
* [为你而设的 Python](https://pythonyou.com/)