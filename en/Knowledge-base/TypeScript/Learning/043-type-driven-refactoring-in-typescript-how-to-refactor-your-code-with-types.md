---
title: 043: Type-Driven Refactoring in TypeScript: How to Refactor Your Code with Types
description: 
published: true
date: 2023-03-06T00:32:47.205Z
tags: 
editor: markdown
dateCreated: 2023-03-06T00:32:45.856Z
---

- [043: TypeScript의 유형 기반 리팩토링: 유형을 사용하여 코드를 리팩토링하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/043-type-driven-refactoring-in-typescript-how-to-refactor-your-code-with-types)
{.links-list}



Type-driven refactoring is a powerful technique that can help you improve the quality of your TypeScript code. By using types to guide your refactoring efforts, you can make your code more robust, easier to maintain, and less error-prone.

In this post, we'll explore the basics of type-driven refactoring in TypeScript. We'll cover how to use types to identify and refactor common code smells, such as duplicated code, long functions, and complex conditionals. We'll also look at how to use types to improve the design of your code, by making it more modular and easier to reason about.

## What is type-driven refactoring?

Type-driven refactoring is an approach to refactoring that uses the type system of a programming language to guide the process. In TypeScript, this means using the type annotations in your code to help you identify areas that need improvement, and to guide your refactoring efforts.

For example, if you have a function that takes an argument of type `string`, but you're passing in a value of type `any`, TypeScript will highlight this as a potential error. By fixing this error, you can make your code more robust and less prone to bugs.

Type-driven refactoring can also help you identify areas of your code that are difficult to understand or maintain. By looking at the types of your functions and variables, you can get a better sense of what they do, and how they're used in your codebase.

## Refactoring duplicated code

One of the most common code smells is duplicated code. Duplicated code can make your codebase difficult to maintain, and can lead to bugs if one copy of the code is changed but the other is not.

Using types, you can identify duplicated code by looking for functions or methods that have similar type signatures. For example, if you have two functions that both take a `string` argument and return a `boolean`, you may be able to refactor them into a single function that takes a generic type parameter.

```typescript
function startsWithA(str: string): boolean {
  return str.startsWith('a');
}

function endsWithA(str: string): boolean {
  return str.endsWith('a');
}
```

In this example, we have two functions that check if a string starts or ends with the letter 'a'. We can refactor these functions into a single function that takes a generic type parameter, like this:

```typescript
function startsOrEndsWith(str: string, letter: string): boolean {
  if (letter === 'a') {
    return str.startsWith(letter) || str.endsWith(letter);
  }
  return false;
}
```

By using a generic type parameter, we can reuse the same code for different types of strings, without duplicating the logic.

## Refactoring long functions

Another common code smell is long functions. Long functions can be difficult to read and understand, and can make it hard to reason about the behavior of your code.

Using types, you can identify long functions by looking for functions that have long type signatures, or that take many arguments. For example, if you have a function that takes five arguments of different types, you may be able to split it into multiple smaller functions that each take fewer arguments.

```typescript
interface Person {
  name: string;
  age: number;
  address: string;
  phone: string;
  email: string;
}

function sendEmailToPerson(
  person: Person,
  subject: string,
  body: string,
  cc?: string[],
  bcc?: string[],
): boolean {
  // Send email logic here
  return true;
}
```

In this example, we have a function that sends an email to a person, with a subject, body, and optional CC and BCC fields. We can split this function into multiple smaller functions, like this:

```typescript
function getEmailRecipients(person: Person, cc?: string[], bcc?: string[]): string[] {
  const recipients = [person.email];
  if (cc) {
    recipients.push(...cc);
  }
  if (bcc) {
    recipients.push(...bcc);
  }
  return recipients;
}

function sendEmail(recipients: string[], subject: string, body: string): boolean {
  // Send email logic here
  return true;
}

function sendEmailToPerson(person: Person, subject: string, body: string, cc?: string[], bcc?: string[]): boolean {
  const recipients = getEmailRecipients(person, cc, bcc);
  return sendEmail(recipients, subject, body);
}
```

By splitting the function into smaller functions, we can make it easier to understand, test, and maintain.

## Refactoring complex conditionals

Complex conditionals can be another source of code complexity and potential bugs. Conditionals that have many branches or nested conditions can be difficult to understand and reason about.

Using types, you can identify complex conditionals by looking for functions that have long or complex type signatures, or that use many conditionals. For example, if you have a function that checks whether a person is eligible for a promotion based on their age, job title, and performance rating, you may be able to simplify the logic by using a type that represents the person's eligibility.

```typescript
interface Person {
  name: string;
  age: number;
  jobTitle: string;
  performanceRating: number;
}

function isEligibleForPromotion(person: Person): boolean {
  if (person.age >= 30 && person.jobTitle === 'Manager' && person.performanceRating >= 4) {
    return true;
  }
  if (person.age >= 25 && person.jobTitle === 'Developer' && person.performanceRating >= 3) {
    return true;
  }
  return false;
}
```

In this example, we have a function that checks whether a person is eligible for a promotion based on their age, job title, and performance rating. We can simplify this logic by creating a type that represents the person's eligibility, like this:

```typescript
interface PromotionEligibility {
  age: number;
  jobTitle: 'Manager' | 'Developer';
  performanceRating: number;
}

function isEligibleForPromotion(person: Person, eligibility: PromotionEligibility): boolean {
  return person.age >= eligibility.age
    && person.jobTitle === eligibility.jobTitle
    && person.performanceRating >= eligibility.performanceRating;
}
```

By using a separate type to represent the person's eligibility, we can simplify the logic of the function and make it easier to understand and maintain.

## Additional information

Type-driven refactoring can be a powerful technique for improving the quality of your TypeScript code. However, it's important to remember that types are not a silver bullet for all code quality issues. There may be cases where refactoring based solely on types may not be the best approach.

It's also worth noting that type-driven refactoring can be a more advanced technique, and may require some familiarity with TypeScript's type system. If you're new to TypeScript, it may be helpful to start with some of the basics before diving into type-driven refactoring.

## Further reading

- [Type-Driven Development with TypeScript](https://www.pluralsight.com/courses/typescript-type-driven-development) - a Pluralsight course on using types to guide development in TypeScript.
- [Refactoring TypeScript Code with Confidence](https://www.sitepen.com/blog/refactoring-typescript-code-with-confidence/) - a blog post on using TypeScript's type system to improve code quality.
- [TypeScript Handbook - Type Inference](https://www.typescriptlang.org/docs/handbook/type-inference.html) - the official TypeScript handbook section on type inference.