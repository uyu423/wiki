---
title: 013: Nest.js에서 인증 구현
description: 
published: true
date: 2023-02-14T23:32:20.734Z
tags: 
editor: markdown
dateCreated: 2023-02-14T23:32:18.981Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [013: Implementing authorization in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/013-implementing-authorization-in-nest-js)
{.links-list}


# Nest.js에서 인증 구현

Nest.js는 확장 가능한 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. 프로그레시브 JavaScript를 사용하고 TypeScript(순수 JavaScript와의 호환성 유지)로 구축되었으며 객체 지향 프로그래밍, 기능적 프로그래밍 및 기능적 반응 프로그래밍의 요소를 결합합니다.

이 게시물에서는 Nest.js 애플리케이션에서 인증을 구현하는 방법에 중점을 둘 것입니다. Nest.js에서 인증을 구현하는 방법으로 이동하기 전에 인증이 무엇이고 왜 중요한지 살펴보겠습니다.

## 인증이란 무엇입니까?

권한 부여는 사용자가 작업을 수행하거나 리소스에 액세스할 수 있는지 여부를 결정하는 프로세스입니다. 일반적으로 사용자에게 작업을 수행하는 데 필요한 권한이 있는지 확인하는 작업이 포함됩니다.

웹 애플리케이션에서 인증은 일반적으로 사용자의 신원을 확인한 다음 인증된 사용자 목록과 비교하여 수행됩니다. 사용자에게 권한이 있는 경우 리소스에 액세스할 수 있습니다. 권한이 없는 경우 리소스에 액세스할 수 없습니다.

승인에는 두 가지 주요 유형이 있습니다.

- **인증**: 사용자가 본인이 맞는지 확인하는 프로세스입니다. 웹 애플리케이션에서 이는 일반적으로 사용자 데이터베이스에 대해 사용자의 자격 증명(예: 사용자 이름 및 암호)을 확인하여 수행됩니다.

- **인증**: 사용자가 리소스에 액세스하는 데 필요한 권한이 있는지 확인하는 프로세스입니다. 웹 애플리케이션에서 이것은 일반적으로 인증된 사용자 목록에 대해 사용자의 신원을 확인하여 수행됩니다. 사용자에게 권한이 있는 경우 리소스에 액세스할 수 있습니다. 권한이 없는 경우 리소스에 액세스할 수 없습니다.

## 인증이 중요한 이유는 무엇인가요?

인증은 애플리케이션을 안전하게 유지하는 데 도움이 되므로 중요합니다. 승인된 사용자만 리소스에 액세스하도록 허용함으로써 중요한 데이터에 대한 무단 액세스를 방지할 수 있습니다.

## Nest.js에서 인증 구현

Nest.js는 인증을 구현하는 다양한 방법을 제공합니다. 이 섹션에서는 `@Authorized()` 데코레이터와 `CanActivate` 가드를 사용하는 가장 일반적인 두 가지 방법을 살펴보겠습니다.

### `@Authorized()` 데코레이터 사용

`@Authorized()` 데코레이터를 사용하여 컨트롤러 또는 작업에 대한 액세스를 제한할 수 있습니다. 컨트롤러 또는 작업에 액세스할 수 있는 역할 목록인 단일 인수를 사용합니다.

예를 들어 다음 컨트롤러는 'ADMIN' 역할을 가진 사용자만 액세스할 수 있습니다.

```typescript
@Controller('/users')
@Authorized(['ADMIN'])
export class UserController {

}
```

`ADMIN` 역할이 없는 사용자가 `/users` 엔드포인트에 액세스하려고 하면 `authorized` 오류가 표시됩니다.

### `CanActivate` 가드 사용하기

'CanActivate' 가드는 경로에 대한 액세스를 제한하는 데 사용할 수 있습니다. 경로에 액세스할 수 있는 역할 목록인 단일 인수를 사용합니다.

예를 들어 다음 경로는 `ADMIN` 역할을 가진 사용자만 액세스할 수 있습니다.

```typescript
@Get('/users')
@CanActivate(['ADMIN'])
export class UserController {

}
```

`ADMIN` 역할이 없는 사용자가 `/users` 엔드포인트에 액세스하려고 하면 `authorized` 오류가 표시됩니다.

## 추가 정보

- Nest.js 문서: https://docs.nestjs.com/
- TypeScript 문서: https://www.typescriptlang.org/docs/handbook/basic-types.html