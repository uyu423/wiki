---
title: 040: Augmenting Types in TypeScript: How to Add Properties and Methods to Existing Types
description: 
published: true
date: 2023-03-08T15:32:46.949Z
tags: 
editor: markdown
dateCreated: 2023-03-08T15:32:46.949Z
---

- [040: TypeScript의 유형 보강: 기존 유형에 속성 및 메서드를 추가하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/040-augmenting-types-in-typescript-how-to-add-properties-and-methods-to-existing-types)
{.links-list}



Augmenting Types in TypeScript: How to Add Properties and Methods to Existing Types

TypeScript is a popular language for front-end and back-end development that provides static typing to JavaScript. It offers a way to define and use types that are not natively available in JavaScript. One of the most useful features of TypeScript is the ability to augment existing types with new properties and methods. In this post, we will explore how to augment types in TypeScript.

## Why Augment Types?

Augmenting types in TypeScript enables developers to extend the capabilities of existing types without modifying their original definitions. This approach allows developers to add new methods and properties to existing types, which can be useful in many scenarios. For instance, you may want to add new methods to the `Array` type or add new properties to the `Window` type.

## Augmenting Types in TypeScript

To augment a type in TypeScript, you need to declare a new interface with the same name as the type you want to augment. The new interface should include the additional properties and methods you want to add to the existing type. Let's consider an example where we want to add a new method called `shuffle` to the `Array` type.

```typescript
interface Array<T> {
  shuffle(): T[];
}
```

In the above code, we declare a new interface called `Array` that takes a type parameter `T`. We then declare a new method called `shuffle` that returns an array of type `T[]`. This interface declaration augments the existing `Array` type with the new `shuffle` method.

To use the new `shuffle` method in our code, we simply need to call it on an instance of an array, as shown below:

```typescript
const myArray = [1, 2, 3, 4, 5];
const shuffledArray = myArray.shuffle();
```

In the above code, we create an instance of an array called `myArray` and call the new `shuffle` method on it. The method returns a shuffled array, which we store in a new variable called `shuffledArray`.

## Augmenting Third-Party Libraries

In addition to augmenting built-in types, we can also augment types from third-party libraries. This approach can be useful when we want to add new properties or methods to types that are not included in the library's definition files.

To augment a third-party library, we first need to install the corresponding `@types` package. For instance, if we want to augment the `lodash` library, we need to install the `@types/lodash` package.

Once we have installed the `@types` package, we can declare a new interface with the same name as the type we want to augment. The new interface should include the additional properties and methods we want to add to the existing type. For instance, let's consider an example where we want to add a new method called `chunkBy` to the `_.Array` type in the `lodash` library.

```typescript
declare module 'lodash' {
  interface Array<T> {
    chunkBy(size: number): T[][];
  }
}
```

In the above code, we declare a new module with the name `lodash`. We then declare a new interface called `Array` that takes a type parameter `T`. We then declare a new method called `chunkBy` that takes a number parameter `size` and returns a two-dimensional array of type `T[][]`. This interface declaration augments the existing `_.Array` type in the `lodash` library with the new `chunkBy` method.

To use the new `chunkBy` method in our code, we simply need to call it on an instance of an array, as shown below:

```typescript
import _ from 'lodash';

const myArray = [1, 2, 3, 4, 5];
const chunkedArray = _.chunkBy(myArray, 2);
```

In the above code, we import the `lodash` library and create an instance of an array called `myArray`. We then call the new `chunkBy` method on the `lodash` object and pass in the `myArray` array and the chunk size of `2`. The method returns a chunked array, which we store in a new variable called `chunkedArray`.

## Additional Information

- Augmenting types in TypeScript is a powerful feature that can be used to extend the capabilities of existing types.
- Augmenting third-party libraries can be useful when we want to add new properties or methods to types that are not included in the library's definition files.
- When augmenting types, it is important to avoid naming conflicts with existing properties and methods.

## Conclusion

In this post, we explored how to augment types in TypeScript. We saw how to add new properties and methods to existing types, both built-in and third-party. Augmenting types is a powerful feature that enables developers to extend the capabilities of existing types without modifying their original definitions. By using this feature, developers can write more expressive and maintainable code.

## Further Reading

- [TypeScript Handbook: Declaration Merging](https://www.typescriptlang.org/docs/handbook/declaration-merging.html)
- [TypeScript Deep Dive: Declaration Merging](https://basarat.gitbook.io/typescript/type-system/declaration-merging)