---
title: 024: 함수형 자바스크립트에서 Maybe 모나드를 사용하는 실용 가이드
description: 
published: true
date: 2023-02-17T18:33:29.991Z
tags: 
editor: markdown
dateCreated: 2023-02-17T18:33:28.563Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [024: A practical guide to using the Maybe monad in functional JavaScript***English** document is available*](/en/Knowledge-base/Functional_JavaScript/Learning/024-a-practical-guide-to-using-the-maybe-monad-in-functional-javascript)
{.links-list}




함수형 프로그래밍은 함수의 평가를 강조하는 프로그래밍 패러다임입니다. 함수형 프로그래밍에서 함수는 일급 시민으로 간주됩니다. 즉, 다른 함수에 인수로 전달되고 다른 함수에서 반환될 수 있습니다.

자바스크립트에서는 함수를 만드는 방법이 많습니다. 한 가지 방법은 다음과 같이 function 키워드를 사용하는 것입니다.

함수 myFunction() {
 // 뭔가를
}

또 다른 방법은 다음과 같이 =>(굵은 화살표) 구문을 사용하는 것입니다.

const myFunction = () => {
 // 뭔가를
}

=> 구문은 function 키워드의 줄임말입니다. 다음과 같이 익명 함수를 만들 때 종종 function 키워드 대신 사용됩니다.

const myArray = [1, 2, 3, 4, 5];

myArray.map(x => x * 2); // [2, 4, 6, 8, 10]

위의 예에서 myArray.map() 메서드는 함수를 인수로 사용합니다. map() 메서드에 전달되는 함수는 배열의 각 요소에 2를 곱하는 익명 함수입니다.

다른 함수에 인수로 전달되는 것 외에도 함수는 다른 함수에서 반환될 수도 있습니다. 예를 들어 다음 함수는 함수를 반환합니다.

함수 createMultiplier(x) {
 반환 y => y * x;
}

const multiplier = createMultiplier(2);

승수(5); // 10

위의 예에서 createMultiplier() 함수는 숫자를 인수로 사용하고 함수를 반환합니다. 반환되는 함수는 숫자를 인수로 사용하고 숫자에 createMultiplier() 함수에 전달된 숫자를 곱한 결과를 반환합니다.

다른 함수에서 함수를 반환하는 기능은 함수형 프로그래밍의 강력한 기능입니다. 다른 함수를 인수 및/또는 반환 함수로 사용하는 함수인 고차 함수를 생성할 수 있습니다.

함수형 프로그래밍에서 가장 인기 있는 고차 함수 중 하나는 map() 함수입니다. map() 함수는 함수를 인수로 사용하고 해당 함수를 배열의 각 요소에 적용합니다. 예를 들어:

const myArray = [1, 2, 3, 4, 5];

myArray.map(x => x * 2); // [2, 4, 6, 8, 10]

위의 예에서 map() 함수는 익명 함수를 인수로 사용합니다. 익명 함수는 숫자를 인수로 사용하고 숫자에 2를 곱한 결과를 반환합니다. map() 함수는 익명 함수를 myArray 배열의 각 요소에 적용하고 결과와 함께 새 배열을 반환합니다.

map() 함수 외에도 함수형 프로그래밍에는 다른 많은 고차 함수가 있습니다. 다른 유명한 고차 함수는 다음과 같습니다.

- filter(): 함수를 인수로 취하고 함수가 true를 반환하는 요소만 포함하는 새 배열을 반환합니다.
- reduce(): 함수를 인수로 받아 배열의 요소에 함수를 적용한 결과인 단일 값을 반환합니다.
- forEach(): 함수를 인수로 받아 배열의 각 요소에 함수를 적용합니다.

함수형 프로그래밍은 함수의 평가를 강조하는 프로그래밍 패러다임입니다. 함수형 프로그래밍에서 함수는 일급 시민으로 간주됩니다. 즉, 다른 함수에 인수로 전달되고 다른 함수에서 반환될 수 있습니다.

자바스크립트에서는 함수를 만드는 방법이 많습니다. 한 가지 방법은 다음과 같이 function 키워드를 사용하는 것입니다.

함수 myFunction() {
 // 뭔가를
}

또 다른 방법은 다음과 같이 =>(굵은 화살표) 구문을 사용하는 것입니다.

const myFunction = () => {
 // 뭔가를
}

=> 구문은 function 키워드의 줄임말입니다. 다음과 같이 익명 함수를 만들 때 종종 function 키워드 대신 사용됩니다.

const myArray = [1, 2, 3, 4, 5];

myArray.map(x => x * 2); // [2, 4, 6, 8, 10]

위의 예에서 myArray.map() 메서드는 함수를 인수로 사용합니다. map() 메서드에 전달되는 함수는 배열의 각 요소에 2를 곱하는 익명 함수입니다.

다른 함수에 인수로 전달되는 것 외에도 함수는 다른 함수에서 반환될 수도 있습니다. 예를 들어 다음 함수는 함수를 반환합니다.

함수 createMultiplier(x) {
 반환 y => y * x;
}

const multiplier = createMultiplier(2);

승수(5); // 10

위의 예에서 createMultiplier() 함수는 숫자를 인수로 사용하고 함수를 반환합니다. 반환되는 함수는 숫자를 인수로 사용하고 숫자에 createMultiplier() 함수에 전달된 숫자를 곱한 결과를 반환합니다.

다른 함수에서 함수를 반환하는 기능은 함수형 프로그래밍의 강력한 기능입니다. 다른 함수를 인수 및/또는 반환 함수로 사용하는 함수인 고차 함수를 생성할 수 있습니다.

함수형 프로그래밍에서 가장 인기 있는 고차 함수 중 하나는 map() 함수입니다. map() 함수는 함수를 인수로 사용하고 해당 함수를 배열의 각 요소에 적용합니다. 예를 들어:

const myArray = [1, 2, 3, 4, 5];

myArray.map(x => x * 2); // [2, 4, 6, 8, 10]

위의 예에서 map() 함수는 익명 함수를 인수로 사용합니다. 익명 함수는 숫자를 인수로 사용하고 숫자에 2를 곱한 결과를 반환합니다. map() 함수는 익명 함수를 myArray 배열의 각 요소에 적용하고 결과와 함께 새 배열을 반환합니다.

map() 함수 외에도 함수형 프로그래밍에는 다른 많은 고차 함수가 있습니다. 다른 유명한 고차 함수는 다음과 같습니다.

- filter(): 함수를 인수로 취하고 함수가 true를 반환하는 요소만 포함하는 새 배열을 반환합니다.
- reduce(): 함수를 인수로 받아 배열의 요소에 함수를 적용한 결과인 단일 값을 반환합니다.
- forEach(): 함수를 인수로 받아 배열의 각 요소에 함수를 적용합니다.

함수를 인수로 전달하고 다른 함수에서 함수를 반환하는 기능은 함수형 프로그래밍의 강력한 기능입니다. 그러나 패러다임을 처음 접하는 개발자에게는 혼란의 원인이 될 수도 있습니다. 이 게시물에서는 기능적 JavaScript에서 Maybe 모나드를 사용하는 방법에 대한 실용적인 가이드를 살펴보겠습니다.

모나드 란 무엇입니까?

함수형 프로그래밍의 맥락에서 모나드는 함수의 구성을 허용하는 구조입니다. 모나드는 종종 일련의 함수를 함께 연결하는 방법을 제공하는 데 사용됩니다. 체인의 각 함수는 값을 입력으로 사용하고 값을 출력으로 반환합니다. 그런 다음 체인에 있는 한 함수의 출력이 체인의 다음 함수에 대한 입력으로 전달됩니다.

모나드는 체인의 기능이 구현되는 방법에 대한 세부 정보를 추상화하는 방법입니다. 이를 통해 체인의 기능을 쉽게 교체하고 다른 기능으로 교체할 수 있습니다.

Maybe 모나드란?

Maybe 모나드는 존재할 수도 있고 없을 수도 있는 값을 나타내는 모나드입니다. Maybe 모나드는 종종 null 값의 가능성을 처리하는 데 사용됩니다.

JavaScript에서 Maybe 모나드는 설화 라이브러리의 Maybe 클래스를 사용하여 구현할 수 있습니다.

const { 아마도 } = require('전설/아마도');

const myFunction = x =>
 Maybe.of(x) // "of" 메서드는 값에서 Maybe 인스턴스를 생성합니다.
 .map(x => x * 2) // "map" 메서드는 값에 함수를 적용합니다.
 .getOrElse(널); // "getOrElse" 메서드는 값을 반환하거나 값이 없으면 기본값을 반환합니다.

myFunction(10); // 20
myFunction(null); // 없는

위의 예에서 myFunction() 함수는 숫자를 인수로 사용하고 숫자에 2를 곱한 결과를 반환합니다. myFunction() 함수에 전달된 숫자가 null이면 함수는 null을 반환합니다.

Maybe 모나드는 전통적인 if...else 문을 사용하는 것보다 더 우아한 방식으로 null 값의 가능성을 처리하는 데 사용할 수 있습니다.

const myFunction = x =>
 아마도.of(x)
 .map(x => x * 2)
 .getOrElse(널);

myFunction(10); // 20
myFunction(null); // 없는

위의 예에서 myFunction() 함수는 숫자를 인수로 사용하고 숫자에 2를 곱한 결과를 반환합니다. myFunction() 함수에 전달된 숫자가 null이면 함수는 null을 반환합니다.

Maybe 모나드는 정의되지 않은 값의 가능성을 처리하는 데에도 사용할 수 있습니다.

const myFunction = x =>
 아마도.of(x)
 .map(x => x * 2)
 .getOrElse(정의되지 않음);

myFunction(10); // 20
myFunction(정의되지 않음); // 한정되지 않은

위의 예에서 myFunction() 함수는 숫자를 인수로 사용하고 숫자에 2를 곱한 결과를 반환합니다. myFunction() 함수에 전달된 숫자가 정의되지 않은 경우 함수는 정의되지 않은 값을 반환합니다.

Maybe 모나드는 존재하거나 존재하지 않는 객체의 속성에 안전하게 접근하는 데 사용할 수 있습니다.

const myObject = {
 : 10,
 비: 20
};

const myFunction = x =>
 Maybe.of(myObject[x])
 .map(x => x * 2)
 .getOrElse(널);

myFunction('a'); // 20
myFunction('c'); // 없는

위의 예에서 myFunction() 함수는 속성 이름을 인수로 사용하고 속성 값에 2를 곱한 값을 반환합니다. 속성이 존재하지 않으면 함수는 null을 반환합니다.

Maybe 모나드는 존재하거나 존재하지 않는 함수를 호출하는 데에도 사용할 수 있습니다.

const myObject = {
 : 10,
 b: 20,
 myFunction: x => x * 2
};

const myFunction = x =>
 Maybe.of(myObject.myFunction)
 .map(f => f(x))
 .getOrElse(널);

myFunction(10); // 20
myFunction(); // 없는

위의 예에서 myFunction() 함수는 숫자를 인수로 사용하고 숫자로 myObject.myFunction() 함수를 호출한 결과를 반환합니다. myObject.myFunction() 함수가 존재하지 않으면 myFunction() 함수는 null을 반환합니다.

Maybe 모나드는 오류 값의 가능성을 처리하는 데 사용할 수 있습니다.

const myFunction = x =>
 아마도.of(x)
 .map(x => {
  경우 (x === 0) {
   throw new Error('x는 0이 될 수 없습니다!');
  }
  반환 x * 2;
 })
 .getOrElse(널);

myFunction(10); // 20
myFunction(0); // 없는

위의 예에서 myFunction() 함수는 숫자를 인수로 사용하고 숫자에 2를 곱한 결과를 반환합니다. myFunction() 함수에 전달된 숫자가 0이면 함수는 null을 반환합니다.

Maybe 모나드는 예상 유형이 아닌 값의 가능성을 처리하는 데 사용할 수 있습니다.

const myFunction = x =>
 아마도.of(x)
 .map(x => {
  if (typeof x !== '숫자') {
   throw new Error('x는 숫자여야 합니다!');
  }
  반환 x * 2;
 })
 .getOrElse(널);

myFunction(10); // 20
myFunction('10'); // 없는

위의 예에서 myFunction() 함수는 값을 인수로 사용하고 값에 2를 곱한 결과를 반환합니다. myFunction() 함수에 전달된 값이 숫자가 아니면 함수는 null을 반환합니다.

Maybe 모나드는 예상 유형이 아닌 값의 가능성을 처리하는 데 사용할 수 있습니다.

const myFunction = x =>
 아마도.of(x)
 .map(x => {
  if (typeof x !== '숫자') {
   throw new Error('x는 숫자여야 합니다!');
  }
  반환 x * 2;
 })
 .getOrElse(널);

myFunction(10); // 20
myFunction('10'); // 없는

위의 예에서 myFunction() 함수는 값을 인수로 사용하고 값에 2를 곱한 결과를 반환합니다. myFunction() 함수에 전달된 값이 숫자가 아니면 함수는 null을 반환합니다.

Maybe 모나드는 값을 반환하거나 반환하지 않는 일련의 함수를 구성하는 데 사용할 수 있습니다.

const myFunction = x =>
 아마도.of(x)
 .map(x => x * 2)
 .map(x => x + 1)
 .map(x => x / 2)
 .getOrElse(널);

myFunction(10); // 10.5
myFunction(null); // 없는

위의 예에서 myFunction() 함수는 숫자를 인수로 사용하여 일련의 함수를 구성한 결과를 반환합니다. 시리즈의 함수 중 하나라도 null을 반환하면 myFunction() 함수도 null을 반환합니다.

Maybe 모나드는 존재하거나 존재하지 않는 객체의 속성에 안전하게 접근하는 데 사용할 수 있습니다.

const myObject = {
 : 10,
 비: 20
};

const myFunction = x =>
 Maybe.of(myObject[x])
 .map(x => x * 2)
 .getOrElse(널);

myFunction('a'); // 20
myFunction('c'); // 없는

위의 예에서 myFunction() 함수는 속성 이름을 인수로 사용하고 속성 값에 2를 곱한 값을 반환합니다. 속성이 존재하지 않으면 함수는 null을 반환합니다.

Maybe 모나드는 존재하거나 존재하지 않는 함수를 호출하는 데에도 사용할 수 있습니다.

const myObject = {
 : 10,
 b: 20,
 myFunction: x => x * 2
};

const myFunction = x =>
 Maybe.of(myObject.myFunction)
 .map(f => f(x))
 .getOrElse(널);

myFunction(10); // 20
myFunction(); // 없는

위의 예에서 myFunction() 함수는 숫자를 인수로 사용하고 숫자로 myObject.myFunction() 함수를 호출한 결과를 반환합니다. myObject.myFunction() 함수가 존재하지 않으면 myFunction() 함수는 null을 반환합니다.

Maybe 모나드는 오류 값의 가능성을 처리하는 데 사용할 수 있습니다.

const myFunction = x =>
 아마도.of(x)
 .map(x => {
  경우 (x === 0) {
   throw new Error('x는 0이 될 수 없습니다!');
  }
  반환 x * 2;
 })
 .getOrElse(널);

myFunction(10); // 20
myFunction(0); // 없는

위의 예에서 myFunction() 함수는 숫자를 인수로 사용하고 숫자에 2를 곱한 결과를 반환합니다. myFunction() 함수에 전달된 숫자가 0이면 함수는 null을 반환합니다.

Maybe 모나드는 예상 유형이 아닌 값의 가능성을 처리하는 데 사용할 수 있습니다.

const myFunction = x =>
 아마도.of(x)
 .map(x => {
  if (typeof x !== '숫자') {
   throw new Error('x는 숫자여야 합니다!');
  }
  반환 x * 2;
 })
 .getOrElse(널);

myFunction(10); // 20
myFunction('10'); // 없는

위의 예에서 myFunction() 함수는 값을 인수로 사용하고 값에 2를 곱한 결과를 반환합니다. myFunction() 함수에 전달된 값이 숫자가 아니면 함수는 null을 반환합니다.

Maybe 모나드는 예상 유형이 아닌 값의 가능성을 처리하는 데 사용할 수 있습니다.

const myFunction = x =>
 아마도.of(x)
 .map(x => {
  if (typeof x !== '숫자') {
   throw new Error('x는 숫자여야 합니다!');
  }
  반환 x * 2;
 })
 .getOrElse(널);

myFunction(10); // 20
myFunction('10'); // 없는

위의 예에서 myFunction() 함수는 값을 인수로 사용하고 값에 2를 곱한 결과를 반환합니다. myFunction() 함수에 전달된 값이 숫자가 아니면 함수는 null을 반환합니다.

어쩌면 모나드