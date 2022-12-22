---
title: 코틀린 인 액션: 5장. 람다로 프로그래밍
description: 
published: true
date: 2022-12-22T15:59:30.326Z
tags: kotlin, study
editor: markdown
dateCreated: 2022-11-23T23:27:11.789Z
---

> [Kotlin in Action](http://www.yes24.com/Product/Goods/55148593) ~(드미트리\ 제메로프,\ 스베트라나\ 이사코바\ /\ 에이콘)~ **5장. 람다로 프로그래밍** 개인 요약본입니다.

---

# 5.1 람다 식과 멤버 참조

- 람다는 기본적으로 다른 함수에 넘길 수 있는 작은 코드 조각을 뜻한다.

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

- ㅂ


## 5.1.5 멤버 참조
# 5.2 컬렉션 함수형 API
## 5.2.1 필수적인 함수: filter와 map
## 5.2.2 all, any, count, find: 컬렉션에 술어 적용
## 5.2.3 groupBy: 리스트를 여러 그룹으로 이뤄진 맵으로 변경
## 5.2.4 flatMap과 flatten: 중첩된 컬렉션 안의 원소 처리
# 5.3 지연 계산 lazy 컬렉션 연산
## 5.3.1 시퀀스 연산 실행: 중간 연산과 최종 연산
## 5.3.2 시퀀스 만들기
# 5.4 자바 함수형 인터페이스 활용
## 5.4.1 자바 메소드에 람다를 인자로 전달
## 5.4.2 SAM 생성자: 람다를 함수형 인터페이스로 명시적으로 변경
# 5.5 수신 객체 지정 람다: with와 apply
## 5.5.1 with함수
## 5.5.2 apply함수
# 5.6 요약