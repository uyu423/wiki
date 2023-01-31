---
title: 009：Kotlin 中的高阶函数：了解 Lambda 和匿名函数
description: 
published: true
date: 2023-01-31T05:25:34.381Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:25:34.381Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [009: Higher-Order Functions in Kotlin: Understanding Lambdas and Anonymous Functions***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/009-higher-order-functions-in-kotlin-understanding-lambdas-and-anonymous-functions)
{.links-list}


# Kotlin 高阶函数：了解 Lambda 和匿名函数

在软件开发中，我们武器库中最强大的工具之一是创建和操作函数的能力。函数让我们将代码片段组合在一起以执行特定任务，并且它们可以作为参数传递给其他函数。这使我们能够创建各种有用的抽象。

在 Kotlin 中，函数是一等公民。这意味着我们可以用各种方式操作它们，就像任何其他数据类型一样。特别是，我们可以将函数作为参数传递给其他函数。这被称为高阶函数。

在本文中，我们将了解 Kotlin 中的高阶函数。我们将特别关注两个概念：lambda 和匿名函数。我们将看到如何使用这些概念来创建抽象，使我们的代码更加简洁和可读。

## 什么是 Lambda？

lambda 是一个可以作为参数传递给另一个函数的函数。在 Kotlin 中，lambda 是使用 ```{}``` notation. For example, we can define a lambda that takes two Int arguments and returns the sum of these arguments:

```科特林
val sum: (Int, Int) -> Int = { x, y -> x + y }
```

This lambda can then be passed as an argument to a function:

```科特林
fun process(x: Int, y: Int, f: (Int, Int) -> Int) {
    val 结果 = f(x, y)
    println("结果：$result")
}

process(1, 2, sum) // 打印“结果：3”
```

In the example above, we have a function ```process``` that takes two Int arguments and a function ```f``` as arguments. The function ```f``` is applied to the two Int arguments, and the result is printed.

In the example, we've defined the lambda ```sum``` before passing it to the function ```process```. However, we could also define the lambda inline:

```科特林
process(1, 2, { x, y -> x + y }) // 打印“结果：3”
```

It's often more convenient to define lambdas inline, especially when they're only used once.

Lambdas can be used to create all sorts of useful abstractions. For example, we can use them to define handy functions for working with Collections:

```科特林
val numbers = listOf(1, 2, 3, 4, 5)

// 在单独的行上打印列表的每个元素
numbers.forEach { println(it) }

// 打印列表中的每个元素乘以 2
numbers.forEach { println(it * 2) }

// 打印列表的第一个元素
println(numbers.first())

// 打印列表的最后一个元素
println(numbers.last())

// 打印索引为 2 的元素
打印（数字。得到（2））

// 以相反的顺序打印列表
println(numbers.reversed())

// 打印升序排列的列表
println(numbers.sorted())

// 打印降序排列的列表
println(numbers.sortedDescending())
```

In the example above, we've defined a list of numbers and used various higher-order functions to perform operations on this list. These functions take lambdas as arguments, which allows us to define the behavior of the function. 

For example, the ```forEach``` function takes a lambda that is applied to each element in the list. In the first example, we've defined a lambda that simply prints each element. In the second example, we've defined a lambda that multiplies each element by 2.

Similarly, the ```first```, ```last```, and ```get``` functions take a lambda that is used to select the first, last, or element at a given index. 

The ```reversed```, ```sorted```, and ```sortedDescending``` functions take a lambda that is used to compare two elements. In the first example, we've defined a lambda that simply compares the two elements. In the second example, we've defined a lambda that compares the two elements multiplied by 2.

As we can see, lambdas can be used to create all sorts of useful abstractions. In the next section, we'll take a look at another way of creating functions: anonymous functions.

## What is an Anonymous Function?

An anonymous function is a function that doesn't have a name. In Kotlin, anonymous functions are written using the ```科特林
val sum: (Int, Int) -> Int = fun(x, y) = x + y
``` keyword. For example, we can define an anonymous function that takes two Int arguments and returns the sum of these arguments:

```科特林
fun process(x: Int, y: Int, f: (Int, Int) -> Int) {
    val 结果 = f(x, y)
    println("结果：$result")
}

process(1, 2, sum) // 打印“结果：3”
```

This anonymous function can then be passed as an argument to a function:

```sum```

In the example above, we've defined the anonymous function ```科特林
process(1, 2, fun(x, y) = x + y) // 打印“结果：3”
``` before passing it to the function ```process```. However, we could also define the function inline:

```科特林
val numbers = listOf(1, 2, 3, 4, 5)

// 在单独的行上打印列表的每个元素
numbers.forEach（乐趣（它：Int）{
    打印（它）
})

// 打印列表中的每个元素乘以 2
numbers.forEach（乐趣（它：Int）{
    打印（它* 2）
})

// 打印列表的第一个元素
println(numbers.first(fun(it: Int) {
    它 == 1
}))

// 打印列表的最后一个元素
println(numbers.last(fun(it: Int) {
    它 == 5
}))

// 打印索引为 2 的元素
println(numbers.get(2, fun(it: Int) {
    它 == 3
}))

// 以相反的顺序打印列表
println(numbers.reversed(fun(it: Int, that: Int) {
    它 > 那个
}))

// 打印升序排列的列表
println(numbers.sorted(fun(it: Int, that: Int) {
    它<那个
}))

// 打印降序排列的列表
println(numbers.sortedDescending(fun(it: Int, that: Int) {
    它 > 那个
}))
```

As with lambdas, it's often more convenient to define anonymous functions inline.

Anonymous functions can be used to create all sorts of useful abstractions. For example, we can use them to define handy functions for working with Collections:

```forEach```

In the example above, we've defined a list of numbers and used various higher-order functions to perform operations on this list. These functions take anonymous functions as arguments, which allows us to define the behavior of the function. 

For example, the ```first``` function takes an anonymous function that is applied to each element in the list. In the first example, we've defined a function that simply prints each element. In the second example, we've defined a function that multiplies each element by 2.

Similarly, the ```reversed```、```sorted``` 和 ```sortedDescending``` 函数采用匿名函数来比较两个元素。在第一个示例中，我们定义了一个简单比较两个元素的函数。在第二个示例中，我们定义了一个函数，用于比较乘以 2 的两个元素。

如我们所见，匿名函数可用于创建各种有用的抽象。

## 结论

在本文中，我们了解了 Kotlin 中的高阶函数。我们特别关注两个概念：lambda 和匿名函数。我们已经看到了如何使用这些概念来创建抽象，使我们的代码更加简洁和可读。

如果您想了解有关高阶函数的更多信息，我建议您查看以下资源：

* [面向 Java 开发人员的 Kotlin](https://kotlinlang.org/docs/tutorials/kotlin-for-java-developers.html)
* [高阶函数](https://kotlinlang.org/docs/reference/lambdas.html#higher-order-functions)
* [函数类型](https://kotlinlang.org/docs/reference/functions.html#function-types)
* [Lambdas](https://kotlinlang.org/docs/reference/lambdas.html#lambdas)
* [匿名函数](https://kotlinlang.org/docs/reference/lambdas.html#anonymous-functions)
* [内联函数](https://kotlinlang.org/docs/reference/inline-functions.html)