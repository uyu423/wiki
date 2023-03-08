---
title: 032: TypeScript의 구별된 공용체: 판별자를 사용하여 유형을 만드는 방법
description: 
published: true
date: 2023-03-07T07:33:00.674Z
tags: 
editor: markdown
dateCreated: 2023-03-07T07:32:59.298Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [032: Discriminated Unions in TypeScript: How to Create Types with Discriminators***English** document is available*](/en/Knowledge-base/TypeScript/Learning/032-discriminated-unions-in-typescript-how-to-create-types-with-discriminators)
{.links-list}



TypeScript의 식별된 공용체: 식별기로 유형을 생성하는 방법

TypeScript는 JavaScript에 유형 주석을 추가하는 널리 사용되는 프로그래밍 언어입니다. 인터페이스, 클래스 및 열거형을 포함하여 개발자가 더 나은 코드를 작성하는 데 도움이 되는 많은 기능을 제공합니다. TypeScript의 가장 강력한 기능 중 하나는 Discriminated Unions입니다. 이 게시물에서는 Discriminated Union이 무엇인지, 작동 방식 및 TypeScript에서 생성하는 방법을 살펴봅니다.

## 차별적 노동 조합이란 무엇입니까?

식별 유니온은 판별자라고 하는 공통 속성이 있는 유형을 생성할 수 있게 해주는 TypeScript의 패턴입니다. 판별자는 공용체의 각 유형에 대해 특정 값을 갖는 속성입니다. 판별자를 사용하여 TypeScript는 런타임에 변수의 유형을 결정할 수 있습니다.

예를 들어 `Square`와 `Rectangle`의 두 가지 유형이 있다고 가정해 보겠습니다. 두 유형 모두 `type` 속성이 있지만 `type` 속성의 값은 유형마다 다릅니다.

```typescript
interface Square {
  type: 'square';
  size: number;
}

interface Rectangle {
  type: 'rectangle';
  width: number;
  height: number;
}
```

이 예에서 판별자는 `type` 속성입니다. `type` 속성의 값은 `Square` 유형의 경우 `'square'`이고 `Rectangle` 유형의 경우 `'rectangle'`입니다. 이는 TypeScript가 `type` 속성 값을 기반으로 변수의 유형을 결정할 수 있음을 의미합니다.

## 차별적 조합은 어떻게 작동합니까?

식별된 공용체를 만들 때 다른 여러 유형의 공용체인 유형을 정의합니다. 공용체의 각 형식에는 판별자 역할을 하는 공통 속성이 있어야 합니다. Union 유형의 변수를 만들 때 discriminator 속성 값을 특정 값으로 설정해야 합니다.

예를 들어 `Square | 직사각형` 유형:

```typescript
let shape: Square | Rectangle;
```

discriminator 속성의 값을 설정하기 위해 type assertion 또는 type guard를 사용할 수 있습니다. 타입 어설션은 TypeScript가 자체적으로 타입을 결정할 수 없더라도 TypeScript에 변수의 타입을 알려주는 방법입니다. 유형 가드는 변수가 특정 유형인지 확인하는 기능입니다.

다음은 형식 어설션을 사용하여 discriminator 속성 값을 설정하는 예입니다.

```typescript
shape = {
  type: 'square',
  size: 10
} as Square;
```

이 예제에서는 개체가 `Square` 유형임을 TypeScript에 알리기 위해 유형 어설션을 사용하여 판별자 속성 값을 `'square'`로 설정합니다.

다음은 유형 가드를 사용하여 판별자 속성 값을 설정하는 예입니다.

```typescript
function isSquare(shape: Square | Rectangle): shape is Square {
  return shape.type === 'square';
}

if (isSquare(shape)) {
  console.log(shape.size);
} else {
  console.log(shape.width, shape.height);
}
```

이 예제에서는 `isSquare` 함수를 타입 가드로 사용하여 변수가 `Square` 유형인지 확인합니다. 변수가 `Square` 유형인 경우 `size` 속성에 액세스할 수 있습니다. 변수가 `Rectangle` 유형인 경우 `width` 및 `height` 속성에 액세스할 수 있습니다.

## 판별자로 유형을 만드는 방법

판별자가 있는 유형을 작성하려면 판별자 속성이 있는 인터페이스를 정의해야 합니다. 그런 다음 기본 인터페이스를 확장하고 추가 속성을 추가하는 다른 인터페이스를 만들 수 있습니다.

다음은 서로 다른 모양에 대해 구별된 합집합을 만드는 예입니다.

```typescript
interface Shape {
  kind: 'circle' | 'square' | 'rectangle';
}

interface Circle extends Shape {
  kind: 'circle';
  radius: number;
}

interface Square extends Shape {
  kind: 'square';
  size: number;
}

interface Rectangle extends Shape {
  kind: 'rectangle';
  width: number;
  height: number;
}
```

이 예제에서는 구분자 속성 `kind`가 있는 기본 인터페이스 `Shape`를 정의합니다. 그런 다음 `Shape` 인터페이스를 확장하고 추가 속성을 추가하는 세 가지 인터페이스 `Circle`, `Square` 및 `Rectangle`을 만듭니다.

그런 다음 `Circle | 광장 | Rectangle` 유형을 지정하고 판별자 속성 값을 설정합니다.

```typescript
let shape: Circle | Square | Rectangle;

shape = {
  kind: 'circle',
  radius: 10
};

shape = {
  kind: 'square',
  size: 10
};

shape = {
  kind: 'rectangle',
  width: 10,
  height: 20
};
```

## 추가 정보

식별 유니온은 TypeScript의 강력한 기능으로, 보다 안전한 형식의 코드를 작성하는 데 도움이 됩니다. 식별 공용체를 사용하면 공통 속성이 있는 형식을 만들고 해당 속성을 사용하여 런타임에 변수의 형식을 결정할 수 있습니다.

## 외부 리소스

- [TypeScript 핸드북: 식별 유니온](https://www.typescriptlang.org/docs/handbook/advanced-types.html# discriminated-unions)
- [TypeScript 심층 분석: 식별된 공용체](https://basarat.gitbook.io/typescript/type-system/discriminated-unions)