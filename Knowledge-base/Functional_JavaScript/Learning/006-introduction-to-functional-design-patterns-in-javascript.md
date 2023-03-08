---
title: 006: JavaScript의 기능적 디자인 패턴 소개
description: 
published: true
date: 2023-02-17T09:32:49.338Z
tags: 
editor: markdown
dateCreated: 2023-02-17T09:32:42.512Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [006: Introduction to functional design patterns in JavaScript***English** document is available*](/en/Knowledge-base/Functional_JavaScript/Learning/006-introduction-to-functional-design-patterns-in-javascript)
{.links-list}


# JavaScript의 기능적 디자인 패턴 소개

함수형 프로그래밍은 명령 실행보다는 식의 평가를 강조하는 프로그래밍 패러다임입니다. 보다 간결하고 읽기 쉬운 코드를 작성하는 데 자주 사용되는 선언적 프로그래밍 스타일입니다.

JavaScript에는 보다 기능적인 코드를 작성하는 데 사용할 수 있는 몇 가지 디자인 패턴이 있습니다. 이러한 패턴에는 고차 함수, 클로저 및 커링 사용이 포함됩니다.

## 고차 함수

고차 함수는 하나 이상의 함수를 인수로 받거나 함수를 결과로 반환하는 함수입니다.

JavaScript에서 고차 함수는 기존 함수에서 새 함수를 만드는 데 자주 사용됩니다. 예를 들어, Array.prototype.map() 메서드는 함수를 인수로 취하고 원래 배열의 각 요소에 대해 함수를 호출한 결과와 함께 새 배열을 반환하는 고차 함수입니다.

 코드 반복을 피하기 위해 고차 함수를 사용할 수도 있습니다. 예를 들어 다음 코드는 두 숫자의 평균을 계산하는 함수를 정의합니다.

```javascript
function average(a, b) {
  return (a + b) / 2;
}
```

세 숫자의 평균을 계산하려면 평균 함수를 두 번 호출하는 새 함수를 작성할 수 있습니다.

```javascript
function average3(a, b, c) {
  return average(average(a, b), c);
}
```

또는 고차 함수를 사용하여 새로운 평균화 함수를 만들 수 있습니다.

```javascript
function average(a, b) {
  return (a + b) / 2;
}

function average3(a, b, c) {
  return average(a, average(b, c));
}
```

고차 함수 접근 방식은 더 간결하고 읽기 쉽습니다. 또한 더 확장 가능합니다. 4개 숫자의 평균을 계산하려면 average3 함수를 두 번 호출하면 됩니다.

## 폐쇄

클로저는 정의된 범위의 변수에 액세스할 수 있는 함수입니다.

JavaScript에서 클로저는 개인 변수를 생성하는 데 자주 사용됩니다. 예를 들어 다음 코드는 두 가지 메서드를 사용하여 카운터 개체를 만드는 함수를 정의합니다.

```javascript
function createCounter() {
  let count = 0;

  return {
    increment() {
      count++;
    },
    getCount() {
      return count;
    }
  };
}
```

createCounter 함수는 카운트 변수를 정의하고 count의 값을 증가시키는 increment와 count의 현재 값을 리턴하는 getCount의 두 가지 메소드를 사용하여 객체를 리턴합니다.

count 변수는 createCounter 함수 내에서 정의되기 때문에 함수 외부에서 접근할 수 없습니다. 그러나 increment 및 getCount 메소드는 동일한 범위 내에서 정의되기 때문에 count 변수에 액세스할 수 있습니다.

이를 통해 액세스 권한이 있는 메서드에 의해서만 수정할 수 있는 개인 변수를 만들 수 있습니다.

## 커링

Currying은 인수를 부분적으로 적용하여 기존 함수에서 새 함수를 만드는 기술입니다.

JavaScript에서 커링은 종종 고정된 수의 인수로 새 함수를 만드는 데 사용됩니다. 예를 들어 다음 코드는 두 숫자의 곱을 계산하는 함수를 정의합니다.

```javascript
function product(a, b) {
  return a * b;
}
```

세 숫자의 곱을 계산하는 새 함수를 만들고 싶다면 커링을 사용하여 세 번째 숫자를 인수로 사용하는 새 함수를 만들 수 있습니다.

```javascript
function product3(a, b) {
  return function(c) {
    return a * b * c;
  }
}

const productOf3 = product3(3, 4);
console.log(productOf3(5)); // 60
```

위의 코드에서 커링을 사용하여 두 개의 숫자를 인수로 사용하고 세 번째 숫자를 인수로 사용하는 새 함수를 반환하는 새 함수 product3을 만듭니다. 그런 다음 값 3과 4를 사용하여 product3 함수를 호출하고 결과 함수를 productOf3이라는 변수에 저장합니다.

마지막으로 값 5로 productOf3 함수를 호출하고 결과를 콘솔에 출력합니다.

 Currying은 여러 인수를 사용하여 함수를 만드는 데 사용할 수 있습니다. 예를 들어 다음 코드는 세 숫자의 합을 계산하는 함수를 정의합니다.

```javascript
function sum3(a) {
  return function(b) {
    return function(c) {
      return a + b + c;
    }
  }
}

const sumOf3 = sum3(1);
console.log(sumOf3(2)(3)); // 6
```

위의 코드에서 우리는 커링을 사용하여 단일 숫자를 인수로 사용하고 두 개의 숫자를 인수로 사용하는 새 함수를 반환하는 새 함수 sum3을 만듭니다. 그런 다음 값 1로 sum3 함수를 호출하고 결과 함수를 sumOf3이라는 변수에 저장합니다.

마지막으로 값 2와 3으로 sumOf3 함수를 호출하고 결과를 콘솔에 출력합니다.

## 결론

함수형 프로그래밍은 명령 실행보다는 식의 평가를 강조하는 프로그래밍 패러다임입니다. JavaScript에는 보다 기능적인 코드를 작성하는 데 사용할 수 있는 몇 가지 디자인 패턴이 있습니다. 이러한 패턴에는 고차 함수, 클로저 및 커링 사용이 포함됩니다.