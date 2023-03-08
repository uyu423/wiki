---
title: 코틀린 람다 표현식으로 살펴보는 함수형 프로그래밍의 클로져(Closure)
description: 
published: true
date: 2023-02-17T18:00:05.319Z
tags: kotlin, lambda, closure
editor: markdown
dateCreated: 2022-12-22T14:18:13.961Z
---

- [Closures in Functional Programming with Kotlin Lambda Expressions***English** version of this document is available*](/en/dev/Kotlin/Kotlin-labmda-functional-programming-closures)
{.links-list}

---

- 함수형 프로그래밍에서 **클로저는 본문에서 자유 변수(현재 범위에 바인딩되지 않은 변수)를 참조하는 함수**입니다. 클로저는 함수가 실행되는 스코프 밖에서 실행되는 경우에도 실행된 스코프에 있던 변수에 액세스하고 수정할 수 있는 기능을 유지하는 함수입니다.

- Kotlin에서 람다는 다른 객체처럼 생성하고 전달할 수 있는 익명 함수입니다. **람다는 주변 범위의 변수를 캡처**할 수 있으며 이러한 변수는 클로저의 자유 변수로 알려져 있습니다.

- 다음은 자유 변수를 캡처하는 Kotlin 람다의 예제입니다.

```kt
val greeting = "Hello"
val sayHello = { name: String ->
    println("$greeting, $name!")
}

sayHello("John")  // prints "Hello, John!"
```

- 위의 예에서 람다 `sayHello`는 외부의 변수 `greeting`을 캡처합니다. 람다는 실행 스코프 외부에 정의된 경우에도 `greeting`의 값에 액세스하고 수정할 수 있습니다.

- **클로저는 다른 객체와 마찬가지로 함수를 생성하고 값으로 전달**할 수 있기 때문에 함수형 프로그래밍에 유용합니다. 이를 통해 고차 함수(High-order function, 다른 함수를 파라미터로 사용하는 함수) 및 Partial Application(일부 파라미터를 함수에 고정하여 새로운 함수 생성)과 같은 광범위한 프로그래밍 패턴을 사용할 수 있습니다.

- 예를 들어 Kotlin에서 다음과 같은 고차 함수를 작성할 수 있습니다.

```kt
fun repeat(times: Int, action: (Int) -> Unit) {
    for (i in 1..times) {
        action(i)
    }
}
```

- 이 함수는 `Int` 타입의 반복 횟수와 람다 표현식을 인자로 받아 반복 횟수를 인자로 전달하여 함수를 호출합니다. 람다 표현식의 함수는 정수를 파라미터로 사용하고 아무 것도 반환하지 않는 모든 함수가 파라미터로 넘어올 수 있습니다.

- 다음은 이 고차 함수를 람다와 함께 사용할 수 있는 실제 방법의 예제입니다.

```kt
repeat(5) { i ->
    println("Iteration $i")
}
```

- 위의 코드는 다음과 같이 출력됩니다.

```text
Iteration 1
Iteration 2
Iteration 3
Iteration 4
Iteration 5
```

- 이 예제에서 `lambda { i -> println("Iteration $i") }`는 자유 변수를 캡처하지 않으므로 순수 함수입니다. 그러나 람다가 자유 변수를 캡처하면 클로저가 되고 자유 변수의 값은 람다 내에서 액세스하고 수정할 수 있습니다.

### 요약

- 함수형 프로그래밍에서 클로저는 본체에서 자유 변수를 참조하는 함수입니다. **자유 변수는 현재 스코프에 바인딩되지 않고 대신 실행되는 스코프 외부에 정의된 변수**입니다.
- Kotlin에서 람다는 주변 범위에서 변수를 캡처하여 자유 변수로 사용할 수 있는 익명 함수입니다.
- 클로저는 함수를 생성하고 값으로 전달하여 `High-order Function` 및 `Partial Application`과 같은 함수형 프로그래밍 패턴을 가능하게 합니다.
- `High-order Function`(고차함수)는 다른 함수를 인자로 받아 함수를 반환하는 함수이다. 부분 적용은 일부 파라미터를 함수에 고정하여 새 함수를 만드는 프로세스입니다.
- `Partial Application`은 일부 파라미터를 함수에 고정하여 새로운 함수를 만드는 과정입니다. 이렇게 하면 함수가 호출될 때마다 모든 파라미터를 지정하지 않고도 일부 파라미터가 이미 설정된 함수의 특수 버전을 만들 수 있습니다.
- 클로저는 순수 함수(자유 변수를 캡처하지 않는 함수)이거나 자유 변수를 캡처하고 해당 값에 액세스하고 수정할 수 있는 함수일 수 있습니다.

> **부록: Partial Application vs Currying**
> 
> Partial Application과 Currying 모두 함수에 대한 일부 파라미터를 수정하여 새로운 함수를 생성하는 것을 의미합니다. 그러나 Partial Application은 모든 파라미터를 지정하지 않고 일부 파라미터를 함수에 고정하여 새로운 함수를 생성하는 것과 관련되며 Currying은 함수를 각각 파라미터를 사용하는 함수 체인으로 분해하는 것과 관련됩니다.
>
> *Partial Application 예시:*
> ```kt
> fun add(x: Int, y: Int): Int {
>     return x + y
> }
> 
> val addFive = { x: Int -> add(5, x) }
> 
> println(addFive(3))  // prints 8
> println(addFive(10))  // prints 15
> ```
> 이 예제에서 함수 `add`는 두 개의 Int 파라미터를 사용하고 그 합계를 반환합니다. `addFive` 람다 표현식은 첫 번째 파라미터를 5로 고정하고 두 번째 파라미터를 람다로 전달되는 파라미터로 사용하는 Partial Application 함수입니다. `addFive`가 x와 함께 호출되면 첫 번째 파라미터로 5, 두 번째 파라미터로 x를 사용하여 함수 `add`를 호출하고 결과를 반환합니다.
>
> *커링 예시:*
> ```kt
> fun add(x: Int): (Int) -> (Int) -> Int {
>    return { y: Int -> { z: Int -> x + y + z } }
> }
>
> val addThreeNumbers = add(1)(2)(3)  // addThreeNumbers is 6
> ```
> 이 예제에서 함수 `add`는 Int 파라미터 x를 사용하고 Int 파라미터 y를 사용하는 새로운 함수를 반환합니다. 이 새로운 함수는 Int 파라미터 z를 사용하는 또 다른 함수를 반환합니다. 가장 안쪽의 함수가 파라미터 z와 함께 호출되면 x, y 및 z를 더하고 결과를 반환합니다.
> 
> `addThreeNumbers` 람다 표현식은 첫 번째 파라미터를 1로, 두 번째 파라미터를 2로, 세 번째 파라미터를 3으로 고정하는 부분 적용 함수입니다. `addThreeNumbers`가 호출되면 1, 2, 3을 더한 6을 반환합니다. 매 번 파라미터를 1개씩 고정하는 연속적인 `Partial Application`으로 볼 수도 있습니다.


![kotlin.jpeg](/kotlin.jpeg =500x){.align-center}
