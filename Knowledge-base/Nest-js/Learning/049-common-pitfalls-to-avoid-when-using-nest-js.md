---
title: 049: Nest.js를 사용할 때 피해야 할 일반적인 함정
description: 
published: true
date: 2023-02-02T04:17:39.295Z
tags: 
editor: markdown
dateCreated: 2023-02-02T04:17:37.611Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [049: Common pitfalls to avoid when using Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/049-common-pitfalls-to-avoid-when-using-nest-js)
{.links-list}


# 049: Nest.js를 사용할 때 피해야 할 일반적인 함정

Nest.js는 Node.js 애플리케이션을 구축하기 위한 강력한 프레임워크입니다. 그러나 모든 프레임워크와 마찬가지로 Nest를 처음 사용하는 개발자를 걸려 넘어지게 할 수 있는 일반적인 함정이 있습니다. 이 게시물에서는 Nest.js를 사용할 때 저지르는 가장 일반적인 실수와 이를 피하는 방법을 살펴보겠습니다.

## 1. Nest.js를 제대로 초기화하지 않음

Nest.js를 사용할 때 가장 흔히 저지르는 실수 중 하나는 프레임워크를 제대로 초기화하지 못하는 것입니다. Nest.js는 새 프로젝트를 만들 때 `--init` 플래그로 초기화해야 합니다.

```
nest new my-project --init
```

`--init` 플래그를 포함하는 것을 잊어버리면 프로젝트가 제대로 설정되지 않고 오류가 발생합니다.

## 2. @Module 데코레이터를 사용하지 않음

종종 저지르는 또 다른 실수는 모듈을 만들 때 `@Module` 데코레이터를 사용하는 것을 잊는 것입니다. `@Module` 데코레이터는 모든 Nest.js 모듈에 필요합니다.

```javascript
import { Module } from '@nestjs/common';

@Module({})
export class MyModule {}
```

`@Module` 데코레이터를 사용하는 것을 잊은 경우 Nest.js는 모듈을 제대로 식별할 수 없으며 오류가 발생합니다.

## 3. @Controller 데코레이터를 사용하지 않음

마찬가지로 모든 Nest.js 컨트롤러에는 `@Controller` 데코레이터가 필요합니다.

```javascript
import { Controller } from '@nestjs/common';

@Controller('/my-controller')
export class MyController {}
```

`@Controller` 데코레이터를 사용하는 것을 잊은 경우 Nest.js는 컨트롤러를 제대로 식별할 수 없으며 오류가 발생합니다.

## 4. @Injectable 데코레이터를 사용하지 않음

자주 잊혀지는 또 다른 데코레이터는 `@Injectable` 데코레이터입니다. `@Injectable` 데코레이터는 모든 Nest.js 서비스에 필요합니다.

```javascript
import { Injectable } from '@nestjs/common';

@Injectable()
export class MyService {}
```

`@Injectable` 데코레이터를 사용하는 것을 잊은 경우 Nest.js는 서비스를 제대로 식별할 수 없으며 오류가 발생합니다.

## 5. @NestModule 데코레이터를 사용하지 않음

종종 저지르는 또 다른 실수는 모듈을 만들 때 `@NestModule` 데코레이터를 사용하는 것을 잊는 것입니다. `@NestModule` 데코레이터는 모든 Nest.js 모듈에 필요합니다.

```javascript
import { NestModule } from '@nestjs/common';

@NestModule({})
export class MyModule {}
```

`@NestModule` 데코레이터를 사용하는 것을 잊은 경우 Nest.js는 모듈을 제대로 식별할 수 없으며 오류가 발생합니다.

## 6. @NestController 데코레이터를 사용하지 않음

마찬가지로 모든 Nest.js 컨트롤러에는 `@NestController` 데코레이터가 필요합니다.

```javascript
import { NestController } from '@nestjs/common';

@NestController('/my-controller')
export class MyController {}
```

`@NestController` 데코레이터를 사용하는 것을 잊은 경우 Nest.js는 컨트롤러를 제대로 식별할 수 없으며 오류가 발생합니다.

## 7. @NestInjectable 데코레이터를 사용하지 않음

종종 잊혀지는 또 다른 데코레이터는 `@NestInjectable` 데코레이터입니다. `@NestInjectable` 데코레이터는 모든 Nest.js 서비스에 필요합니다.

```javascript
import { NestInjectable } from '@nestjs/common';

@NestInjectable()
export class MyService {}
```

`@NestInjectable` 데코레이터를 사용하는 것을 잊은 경우 Nest.js는 서비스를 제대로 식별할 수 없으며 오류가 발생합니다.

## 8. @Component 데코레이터를 사용하지 않음

종종 저지르는 또 다른 실수는 모듈을 만들 때 `@Component` 데코레이터를 사용하는 것을 잊는 것입니다. `@Component` 데코레이터는 모든 Nest.js 모듈에 필요합니다.

```javascript
import { Component } from '@nestjs/common';

@Component({})
export class MyModule {}
```

`@Component` 데코레이터를 사용하는 것을 잊은 경우 Nest.js는 모듈을 제대로 식별할 수 없으며 오류가 발생합니다.

## 9. @Controller 데코레이터를 사용하지 않음

마찬가지로 모든 Nest.js 컨트롤러에는 `@Controller` 데코레이터가 필요합니다.

```javascript
import { Controller } from '@nestjs/common';

@Controller('/my-controller')
export class MyController {}
```

`@Controller` 데코레이터를 사용하는 것을 잊은 경우 Nest.js는 컨트롤러를 제대로 식별할 수 없으며 오류가 발생합니다.

## 10. @Injectable 데코레이터를 사용하지 않음

자주 잊혀지는 또 다른 데코레이터는 `@Injectable` 데코레이터입니다. `@Injectable` 데코레이터는 모든 Nest.js 서비스에 필요합니다.

```javascript
import { Injectable } from '@nestjs/common';

@Injectable()
export class MyService {}
```

`@Injectable` 데코레이터를 사용하는 것을 잊은 경우 Nest.js는 서비스를 제대로 식별할 수 없으며 오류가 발생합니다.