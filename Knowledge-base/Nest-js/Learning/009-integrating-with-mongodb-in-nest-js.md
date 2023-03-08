---
title: 009: Nest.js에서 MongoDB와 통합
description: 
published: true
date: 2023-02-14T20:32:21.563Z
tags: 
editor: markdown
dateCreated: 2023-02-14T20:32:19.961Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [009: Integrating with MongoDB in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/009-integrating-with-mongodb-in-nest-js)
{.links-list}


# 소개
이 게시물에서는 MongoDB를 Nest.js와 통합하는 방법을 살펴보겠습니다. 이를 위해 Mongoose 라이브러리를 사용할 것입니다. Mongoose는 비동기 환경에서 작동하도록 설계된 MongoDB 개체 모델링 도구입니다.

Nest.js는 확장 가능한 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. TypeScript를 사용하며 Angular에서 영감을 받았습니다.

# 시작하기
먼저 몽구스 라이브러리를 설치해야 합니다. npm을 사용하여 이 작업을 수행할 수 있습니다.

```
npm install mongoose
```

다음으로 몽구스 연결을 위한 파일을 만들어야 합니다. 이 파일을 ```mongoose.ts```라고 합니다:

```typescript
import * as mongoose from 'mongoose';

export const databaseProviders = [
  {
    provide: 'DbConnectionToken',
    useFactory: async () => {
      (mongoose as any).Promise = global.Promise;
      return await mongoose.connect('mongodb://localhost/nest');
    },
  },
];
```

파일에서 우리는 ```useFactory``` 함수를 사용하여 Mongoose 연결로 확인되는 약속을 반환합니다. 또한 Mongoose가 Nest.js와 동일한 약속 라이브러리를 사용하도록 전역 ```Promise``` 속성을 Mongoose ```Promise``` 속성으로 설정합니다.

# Nest.js와 함께 몽구스 사용하기
이제 몽구스를 설치하고 연결 파일을 설정했으므로 Nest.js와 함께 몽구스를 사용하는 방법을 살펴보겠습니다.

먼저 Nest.js 모듈을 만들어야 합니다. 우리는 이 모듈을 ```MongooseModule```이라고 부를 것입니다:

```typescript
import { Module } from '@nestjs/common';
import { MongooseModule } from '@nestjs/mongoose';

@Module({
  imports: [MongooseModule.forRoot('mongodb://localhost/nest')],
})
export class MongooseModule {}
```

모듈에서 우리는 ```forRoot``` 함수를 사용하여 MongooseModule 인스턴스를 만듭니다. 이 함수는 MongoDB 연결 문자열을 유일한 매개변수로 사용합니다.

다음으로 Nest.js 서비스를 만들어야 합니다. 이 서비스를 ```MongoService```라고 합니다.

```typescript
import { Injectable } from '@nestjs/common';
import { InjectModel } from '@nestjs/mongoose';
import { Model } from 'mongoose';

@Injectable()
export class MongoService {
  constructor(
    @InjectModel('User') private readonly userModel: Model<any>,
  ) {}

  async findAll(): Promise<any[]> {
    return await this.userModel.find().exec();
  }
}
```

서비스에서 몽구스 모델을 서비스에 주입하기 위해 ```@InjectModel``` 데코레이터를 사용하고 있습니다. 우리는 또한 ```find``` 기능을 사용하여 모든 사용자에 대해 데이터베이스를 쿼리합니다.

마지막으로 Nest.js 컨트롤러를 만들어야 합니다. 우리는 이 컨트롤러를 ```MongoController```라고 부를 것입니다:

```typescript
import { Controller, Get } from '@nestjs/common';
import { MongoService } from './mongo.service';

@Controller('mongo')
export class MongoController {
  constructor(private readonly mongoService: MongoService) {}

  @Get()
  async findAll() {
    return await this.mongoService.findAll();
  }
}
```

컨트롤러에서 ```@Get``` 데코레이터를 사용하여 GET 요청에 응답하는 경로를 만듭니다. 또한 MongoService의 ```findAll``` 기능을 사용하여 데이터베이스를 쿼리하고 모든 사용자를 반환합니다.

# 결론
이 게시물에서는 MongoDB를 Nest.js와 통합하는 방법을 살펴보았습니다. 우리는 Mongoose 라이브러리를 설치하고 이를 사용하여 Nest.js 모듈, 서비스 및 컨트롤러를 생성했습니다.