---
title: 코틀린 인 액션: 5장. 람다로 프로그래밍
description: 
published: true
date: 2022-12-22T17:12:15.378Z
tags: kotlin, study
editor: markdown
dateCreated: 2022-11-23T23:27:11.789Z
---

> [Kotlin in Action](http://www.yes24.com/Product/Goods/55148593) ~(드미트리\ 제메로프,\ 스베트라나\ 이사코바\ /\ 에이콘)~ **5장. 람다로 프로그래밍** 개인 요약본입니다.

---

# 5.1 람다 식과 멤버 참조

- 람다는 기본적으로 다른 함수에 넘길 수 있는 작은 코드 조각을 뜻한다.
- 코틀린에서의 람다식 역시 자바와 마찬가지로 1급 객체다. 다만 Java에서는 `@FunctionalInterface` 라던지 SAM Interface 라던지 좀 더 장황하고 불편하게 사용했어야했는데, 코틀린은 그런거 없다.

> Kotlin과 Java는 모두 익명 함수를 만드는 방법으로 람다 식을 지원하며 두 언어 모두에서 람다 식은 일급 객체로 취급됩니다. 그러나 람다 표현식이 Kotlin과 Java에서 구현되는 방식에는 몇 가지 주요 차이점이 있습니다.
> <small>Kotlin and Java both support lambda expressions as a way to create anonymous functions, and in both languages, lambda expressions are treated as first-class objects. However, there are some key differences between the way lambda expressions are implemented in Kotlin and Java:</small>
> - Kotlin에서 람다 표현식은 함수 유형의 인스턴스로 표현되는 일급 객체입니다. 즉, 다른 개체와 마찬가지로 변수에 저장하고, 함수에 인수로 전달하고, 함수에서 값으로 반환할 수 있습니다.
>   - <small>In Kotlin, lambda expressions are first-class objects that are represented as instances of function types. This means that they can be stored in variables, passed as arguments to functions, and returned as values from functions, just like any other object.</small>
> - Java에서 람다 식은 익명의 내부 클래스를 사용하여 구현됩니다. 즉, 함수 인터페이스를 확장하는 클래스의 인스턴스로 표현됩니다. 즉, 객체로 취급되지만 내부 클래스로 구현되기 때문에 일반 객체에 비해 약간의 추가 오버헤드가 있습니다.
>   - <small>In Java, lambda expressions are implemented using anonymous inner classes, which means that they are represented as instances of a class that extends a functional interface. This means that they are treated as objects, but they have some additional overhead compared to regular objects due to the fact that they are implemented as inner classes.</small>
> - Kotlin의 람다 표현식은 더 간결한 구문을 사용하고 유형 추론 및 단순화된 반환 구문과 같은 기능을 지원하기 때문에 Java보다 더 간결하고 표현력이 뛰어납니다. 이렇게 하면 더 쉽게 읽고 쓸 수 있으며 필요한 상용구 코드의 양이 줄어듭니다.
>   - <small>Kotlin's lambda expressions are more concise and expressive than Java's because they use a more concise syntax and support features such as type inference and simplified return syntax. This makes them easier to read and write, and it reduces the amount of boilerplate code that is required.</small>
> - Kotlin의 람다 표현식은 함수 유형을 지원하므로 함수 유형을 값으로 전달하고 다양한 방식으로 사용할 수 있습니다. 이를 통해 Java에서 쉽게 표현되지 않는 고차 함수 및 부분 응용 프로그램과 같은 프로그래밍 패턴을 사용할 수 있습니다.
>   - <small>Kotlin's lambda expressions support function types, which allows them to be passed around as values and used in a variety of ways. This enables programming patterns such as higher-order functions and partial application, which are not as easily expressed in Java.</small>
> - 전반적으로 Kotlin의 람다 표현식은 더 간결하고 표현력이 풍부한 구문, 더 나은 함수 유형 지원, 더 적은 상용구 코드 등 Java보다 많은 이점을 제공합니다.
>   - <small>Overall, Kotlin's lambda expressions offer a number of advantages over Java's, including a more concise and expressive syntax, better support for function types, and less boilerplate code.</small>

## 5.1.1 람다 소개: 코드 블록을 함수 인자로 넘기기

- 람다 표현식의 기본적인 문법은 다음과 같다.

```kt
button.setOnClickListener { /* lambda expression */ }
```


## 5.1.2 람다와 컬렉션

```kt
data class Person(val name: String, val world: Int);

val people = listOf(
    Person("hello", 10),
    Person("world", 20),
);

println(people.maxBy { it.age }); // 나이 프로퍼티를 비교해서 값이 가장 큰 원소를 찾는다.
// Person(name=world, age=20);
```

- 위의 `people.maxBy` 는 아래와 같이 표현할 수도 있다.

```kt
people.maxBy(Person::age);
people.maxBy({ p: Person -> p.age});
people.maxBy() { p: Person -> p.age }
people.maxBy { p: Person -> p.age }
```

- 그치만 가급적 마자막 표현식과 같이 쓰는 것에 익숙해지자 `people.maxBy { p: Person -> p.age }`


## 5.1.3 람다 식의 문법

```kt
{ x: Int, y: Int -> x + y }
// Java: (Integer x, Integer y) -> { return x + y; }
```

- 코틀린에서의 모든 람다 표현식은 중괄호 사이에 위치한다.
  - `x: Int, y: Int` 는 파라미터다.
  - `x + y` 는 본문이다.
  - `->` 가 인자 목록과 람다 본문을 구분한다.
- 람다를 변수에 저장할 수 있다.
```kt
val sum = { x: Int, y: Int -> x + y }
```
- 다음과 같이 람다식을 다이렉트로 바로 호출 할 수도 있다.
```kt
{ println(42) }();
```
- 근데 굳이 이렇게 쓰는 것보다 코틀린에서는 `run` 이라는 키워드를 제공한다.
```kt
run { println(42) }
// 사실 이건 `run({ println(42)})` 와 동일하다.
```
- 실행 시점에서 코틀린 람다 호출은 아무런 부가 비용이 들지 않는다.
- 이름 붙인 인자를 통해 람다를 넘기는 방법도 있다.

```kt
val names = people.joinToString(separator = " ", transform = { p: Person -> p.name });
```

- 파라미터로 넘어가는 람다 표현식은 외부로 뺄 수 있으므로, 아래와 같이 사용할 수 있다.

```kt
val names = people.joinToString(" ") { p: Person -> p.name };
```

- 컴파일러가 파라미터의 타입을 추론할 수 있으므로, 아래와 같이 사용해도 문제가 없다.

```kt
val names = people.joinToString(" ") { p -> p.name };
// 람다 자체를 변수에 저장할 때는 타입을 추론할 방법이 없기 때문에 타입을 명시해야한다.
// val getAge = { p: Person -> p.age }
```

- 람다의 파라미터가 하나 뿐이고, 타입을 컴파일러가 추론할 수 있다면 `it`을 사용할 수 있다.

```kt
val names = people.joinToString(" ") { it.name };
// 람다 파라미터의 이름을 따로 지정하지 않은 경우에만 it 네이밍으로 자동 생성된다.
// 하지만, 여러개의 람다가 중첩되는 경우 it 을 남발하게 되면 가독성이 떨어져서 필요에 따라서는 사용을 지양해야할 필요도 있다.
```

- 멀티 라인의 람다의 경우 가장 마지막에 있는 식이 람다의 return 값이 된다.

```kt
val sum = { x: Int, y: Int -> 
  println("something...");
  x + y;
};
```

## 5.1.4 현재 영역에 있는 변수에 접근

- 람다를 함수 안에서 정의하면 함수의 파라미터 뿐 아니라 람다 정의의 앞에 선언된 로컬 변수까지 람다에서 모두 사용할 수 있다.

```kt
val errors = listOf("403 Forbidden", "404 Not Found");

fun printMessagesWithPrefix(messages: Collection<String>, prefix: String) {
    messages.forEach {  // 각 원소에 대해 수행할 작업을 람다로 받는다
      println("$prefix $it")  // 람다 안에서 함수의 "prefix" 파라미터를 사용한다.
    }
}

printMessagesWithPrefix(errors, "Error:");
// Error: 403 Forbidden
// Error: 404 Not Found
```

- 중요한 점은 코틀린 람다 안에서는 파이널 변수가 아닌 외부 변수에도 접근할 수 있교, 변경까지 할 수 있다 (포획).
  - 자바의 람다에서는 파이널 변수에만 접근이 가능했다.
  - 어떤 함수의 자신의 로컬 변수를 포함한 람다를 반환하거나 다른 변수에 저장할 경우 로컬 변수의 생명주기와 함수의 생명주기가 달라질 수 있다.
  
```kt
// closure
val makeCounter = {
    var count = 0; // 람다 외부의 변수 (람다에게 포획 capture 된 변수)
    {
        count += 1; // 람다 외부의 변수를 변경
        count;
    }
}

val counter1 = makeCounter();
println(counter1());
println(counter1());
println(counter1());

val counter2 = makeCounter();
println(counter2());
println(counter2());

// 1
// 2
// 3
// 1
// 2
```

추가로 정리한 것

- [코틀린 람다 표현식으로 살펴보는 함수형 프로그래밍의 클로져(Closure)*WIKI.YOWU.DEV*](/dev/Kotlin/Kotlin-labmda-functional-programming-closures)
{.links-list}


## 5.1.5 멤버 참조

- 위의 일부 예제에서 표현했지만 멤버 참조로 람다를 사용할 수 있다.

```kt
val getAge = Person::age
val getAge2 = { person: Person -> person.age } // 같은 동작을 한다다
```

- 아래 역시 같은 동작을 하는 코드다.

```kt
val people = listOf(Person(...), Person(...));
people.maxBy(Person::age);
people.maxBy { p -> p.age };
people.maxBy { it.age };
```

- 특이한 점은 최상위에 선언된 함수나 프로퍼티를 참조할 수도 있다.
  - 그러나 212p 를 참고하면 안되는 케이스들이 있고, 사용을 지양해야할 패턴처럼 보인다.

```kt
val maxAge4 = people.maxBy(Person::age).age;
fun salute() = println("Salute!");
run(::salute);
```

- 위 케이스외에 생성자 참조로 사용할 수 있다. 그러냐 역시 어디에 써먹어야할지는 감이 잘 안온다. (factory?)
 
```kt
val createPserson = ::Person;
val p = createPerson("Alice", 29);
println(p)
// Person(name=Alice, age=29)
```

- 확장 함수도 멤버 함수와 같은 방식으로 참조할 수 있다.

```kt
fun Person.isAdult() = age > 19;
val p = Person("foo", 21);
val predicate = Person::isAdult; // 확장 함수도 됨

println(predicate(p));
println(run (p::isAdult)); // 이렇게 써두 되긴 함
println(p.isAdult()); // 근데 차라리 이렇게 쓰고 말지
```


# 5.2 컬렉션 함수형 API

- 우리가 Stream API 혹은 seq 를 사용해서 줄창 사용했던 바로 그것

## 5.2.1 필수적인 함수: filter와 map

- `Collection` 에서 바로 사용 가능한 filter 와 map 이 생겼다.

```kt
val numList = listOf(1,2,3,4,5,6,7,8,9,10);

println(numList.filter { it > 5 });
// [6, 7, 8, 9, 10]

println(numList.map { n -> n + 100 });
// [101, 102, 103, 104, 105, 106, 107, 108, 109, 110]

println(numList
    .map { n -> n * n}
    .filter { it > 50 }
);
// [64, 81, 100]

```

- `Map` 에서도 된다.
  - `mapValues`, `mapKeys`, `filterValues`, `filterKeys` 등

```kt
val strmap = mapOf("hello" to "world", "foo" to "bar");

println(strmap.mapValues { it.value.uppercase(Locale.getDefault()) });
// {hello=WORLD, foo=BAR}
```

- 코틀린에서는 체이닝을 걸면 아래와 같은 코드가 된다. 표현이 낯설긴한데, 빨리 익숙해지라고 한다.

```kt
people.filter { it.age > 30 }.map(Person::name);
```

## 5.2.2 all, any, count, find: 컬렉션에 술어 적용

```kt
// 모든 원소가 특정 식을 만족하는지 확인하려면 all 을 사용한다.
println(people.all { it.age > 1 }); 

// 특정 식을 만족하는 원소가 하나라도 있는지 확인하려면 any 를 사용한다.
println(people.any { it.age > 40 }); 

// 특정 식을 만족하는 원소의 갯수를 구하려면 count 를 사용한다.
println(people.count { it.age > 20 });

// 특정식을 만족하는 원소를 하나 찾고 싶으면 find 를 사용한다. (가장 먼저 찾은 원소를 반환)
// find 는 firstOrNull 과 같다.
println(people.find { it.age > 20 });
```

> `!all` 을 수행한 결과와 그 조건의 부정에 대해 `any` 를 수행한 결과는 같다. (드 모르강의 법칙)
> 또한 어떤 조건에 대해 `!any` 를 수행한 결과와 그 조건의 부정에 대해 `all`을 수행한 결과도 같다.
> 그러므로 코드의 가독성을 높이려면 `any` 와 `all` 앞에 `!` 를 붙이지 않는 편이 낫다. (p.218)
> ```kt
> val list = listOf(1, 2, 3);
> println(!list.all { it == 3 });
> // true
> println(list.any { it != 3 });
> // true
> ```

> Java 에서의 경험을 통해 코틀린에 count가 있다는 사실을 망각하고 size를 사용할 수 있다.
> ```kt
> println(people.filter { it.age > 20 }.size);
> ```
> 이런 경우에는 filter 의 결과 값을 결과 값을 가지는 중간 컬렉션이 생성된다.
> count 는 조건을 만족하는 원소 갯수만을 추적하고, 중간 컬렉션을 따로 생성하지 않으므로 count 가 더 효율적이다. (p.219)

## 5.2.3 groupBy: 리스트를 여러 그룹으로 이뤄진 맵으로 변경

```kt
val people = listOf(
    Person("hello", 10),
    Person("world", 20),
    Person("foo", 30),
    Person("bar", 40),
    Person("yu", 32),
    Person("ryu", 30),
    Person("kim", 30),
    Person("lee", 29),
    Person("hwang", 36),
    Person("kim", 36),
);

println(people.groupBy { it.age });
// {10=[Person(name=hello, age=10)], 
//  20=[Person(name=world, age=20)], 
//  30=[Person(name=foo, age=30), Person(name=ryu, age=30), Person(name=kim, age=30)], 
//  40=[Person(name=bar, age=40)],
//  32=[Person(name=yu, age=32)],
//  29=[Person(name=lee, age=29)], 
//  36=[Person(name=kim, age=36)]}, Person(name=hwang, age=38)]
```

- 위 예제의 `groupBy`의 결과 타입은 `Map<Int, List<Person>>` 이다.
- 필요에 따라 `mapKeys`, `mapValues` 를 사용해서 반환 타입을 변경할 수 있다.

## 5.2.4 flatMap과 flatten: 중첩된 컬렉션 안의 원소 처리

```kt
val books = listOf(
    Book("네이버 쇼핑라이브의 이해", listOf("kim")),
    Book("Shortclip 의 모든 것", listOf("yu")),
    Book("Spring Boot 초기 구성 가이드북", listOf("ryu", "lee")),
    Book("Notification 그 너머로", listOf("eom", "kim")),
    Book("Linux Mint 활용하기", listOf("hwang")),
);
println("authors: ${books.flatMap { it.authors }}");
// authors: [kim, yu, ryu, lee, eom, kim, hwang]
```

- flatten 은 단순 이중 컬렉션 처리에 사용하기 좋아보인다.

```kt
val nestedNumbers = listOf(listOf(1, 2), listOf(3, 4));
println("flatten: ${nestedNumbers.flatten()}");
// flatten: [1, 2, 3, 4]
```


# 5.3 지연 계산 lazy 컬렉션 연산

- d

## 5.3.1 시퀀스 연산 실행: 중간 연산과 최종 연산
## 5.3.2 시퀀스 만들기
# 5.4 자바 함수형 인터페이스 활용
## 5.4.1 자바 메소드에 람다를 인자로 전달
## 5.4.2 SAM 생성자: 람다를 함수형 인터페이스로 명시적으로 변경
# 5.5 수신 객체 지정 람다: with와 apply
## 5.5.1 with함수
## 5.5.2 apply함수
# 5.6 요약
# 기타 참고