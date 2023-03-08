---
title: 004: Kotlin의 제어 흐름: if-else 문, 루프 및 When 표현식
description: 
published: true
date: 2023-02-16T01:33:00.820Z
tags: 
editor: markdown
dateCreated: 2023-02-16T01:32:59.166Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [004: Control Flow in Kotlin: if-else Statements, Loops, and When Expressions***English** document is available*](/en/Knowledge-base/Kotlin/Learning/004-control-flow-in-kotlin-if-else-statements-loops-and-when-expressions)
{.links-list}


# Kotlin의 제어 흐름: if-else 문, 루프 및 When 표현식

Kotlin은 포괄적인 제어 흐름 구조 세트를 제공합니다. 이 게시물에서는 Kotlin에서 if-else 문, 루프 및 when 표현식을 사용하는 방법을 살펴보겠습니다.

## if-else 문

If-else 문은 특정 조건이 충족되는 경우에만 특정 코드 블록을 실행하는 데 사용됩니다. Kotlin에서 if-else 문의 일반적인 형식은 다음과 같습니다.

```kotlin
if (condition) {
    // Execute this block if the condition is true
} else {
    // Execute this block if the condition is false
}
```

Kotlin에서 if-else 문을 사용하는 방법에 대한 몇 가지 예를 살펴보겠습니다.

### 예 1

이 예에서는 if-else 문을 사용하여 숫자가 양수인지 음수인지 출력합니다.

```kotlin
fun main(args: Array<String>) {
    val num = 5

    if (num > 0) {
        println("$num is positive")
    } else {
        println("$num is negative")
    }
}
```

산출:

```
5 is positive
```

### 예 2

이 예에서는 if-else 문을 사용하여 두 숫자 중 더 큰 숫자를 출력합니다.

```kotlin
fun main(args: Array<String>) {
    val num1 = 5
    val num2 = 10

    if (num1 > num2) {
        println("$num1 is larger than $num2")
    } else {
        println("$num2 is larger than $num1")
    }
}
```

산출:

```
10 is larger than 5
```

## 루프

루프는 특정 코드 블록을 여러 번 실행하는 데 사용됩니다. Kotlin은 for 루프, while 루프 및 do-while 루프의 세 가지 유형의 루프를 제공합니다.

### for 루프

For 루프는 값 범위 또는 값 배열을 반복하는 데 사용됩니다. Kotlin에서 for 루프의 일반적인 형식은 다음과 같습니다.

```kotlin
for (variable in range) {
    // Execute this block for each value in the range
}
```

Kotlin에서 for 루프를 사용하는 방법에 대한 몇 가지 예를 살펴보겠습니다.

### 예 1

이 예에서는 for 루프를 사용하여 처음 10개의 자연수를 출력합니다.

```kotlin
fun main(args: Array<String>) {
    for (i in 1..10) {
        println(i)
    }
}
```

산출:

```
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

### 예 2

이 예제에서는 for 루프를 사용하여 배열의 요소를 출력합니다.

```kotlin
fun main(args: Array<String>) {
    val array = arrayOf(1, 2, 3, 4, 5)

    for (element in array) {
        println(element)
    }
}
```

산출:

```
1
2
3
4
5
```

### while 루프

While 루프는 특정 조건이 충족될 때까지 특정 코드 블록을 여러 번 실행하는 데 사용됩니다. Kotlin에서 while 루프의 일반적인 형식은 다음과 같습니다.

```kotlin
while (condition) {
    // Execute this block while the condition is true
}
```

Kotlin에서 while 루프를 사용하는 방법에 대한 몇 가지 예를 살펴보겠습니다.

### 예 1

이 예에서는 while 루프를 사용하여 처음 10개의 자연수를 출력합니다.

```kotlin
fun main(args: Array<String>) {
    var i = 1

    while (i <= 10) {
        println(i)
        i++
    }
}
```

산출:

```
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

### 예 2

이 예에서는 while 루프를 사용하여 처음 10개의 자연수를 합산합니다.

```kotlin
fun main(args: Array<String>) {
    var i = 1
    var sum = 0

    while (i <= 10) {
        sum += i
        i++
    }

    println("The sum of the first 10 natural numbers is $sum")
}
```

산출:

```
The sum of the first 10 natural numbers is 55
```

### do-while 루프

Do-while 루프는 특정 조건이 충족될 때까지 특정 코드 블록을 여러 번 실행하는 데 사용됩니다. Kotlin에서 do-while 루프의 일반적인 형식은 다음과 같습니다.

```kotlin
do {
    // Execute this block at least once
} while (condition)
```

Kotlin에서 do-while 루프를 사용하는 방법에 대한 몇 가지 예를 살펴보겠습니다.

### 예 1

이 예에서는 do-while 루프를 사용하여 처음 10개의 자연수를 출력합니다.

```kotlin
fun main(args: Array<String>) {
    var i = 1

    do {
        println(i)
        i++
    } while (i <= 10)
}
```

산출:

```
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

### 예 2

이 예에서는 do-while 루프를 사용하여 처음 10개의 자연수를 합산합니다.

```kotlin
fun main(args: Array<String>) {
    var i = 1
    var sum = 0

    do {
        sum += i
        i++
    } while (i <= 10)

    println("The sum of the first 10 natural numbers is $sum")
}
```

산출:

```
The sum of the first 10 natural numbers is 55
```

## 언제 표현식

특정 값을 기반으로 특정 코드 블록을 실행하기 위해 표현식을 사용하는 경우. Kotlin에서 when 표현식의 일반적인 형식은 다음과 같습니다.

```kotlin
when (value) {
    value1 -> {
        // Execute this block when the value is value1
    }
    value2 -> {
        // Execute this block when the value is value2
    }
    // ...
    else -> {
        // Execute this block when the value is none of the above
    }
}
```

Kotlin에서 when 표현식을 사용하는 방법에 대한 몇 가지 예를 살펴보겠습니다.

### 예 1

이 예제에서는 when 표현식을 사용하여 특정 색상의 의미를 출력합니다.

```kotlin
fun main(args: Array<String>) {
    val color = "red"

    when (color) {
        "red" -> println("Red is the color of blood")
        "blue" -> println("Blue is the color of the sky")
        "green" -> println("Green is the color of grass")
        else -> println("I don't know the meaning of that color")
    }
}
```

산출:

```
Red is the color of blood
```

### 예 2

이 예제에서는 when 식을 사용하여 학생의 점수를 기준으로 학생의 성적을 출력합니다.

```kotlin
fun main(args: Array<String>) {
    val score = 95

    when (score) {
        in 90..100 -> println("You got an A!")
        in 80..89 -> println("You got a B!")
        in 70..79 -> println("You got a C!")
        in 60..69 -> println("You got a D!")
        else -> println("You got an F!")
    }
}
```

산출:

```
You got an A!
```

## 결론

이 게시물에서는 Kotlin에서 if-else 문, 루프 및 when 표현식을 사용하는 방법을 살펴보았습니다. 이들은 모두 Kotlin 프로그램을 작성하기 위해 알아야 하는 중요한 제어 흐름 구조입니다.