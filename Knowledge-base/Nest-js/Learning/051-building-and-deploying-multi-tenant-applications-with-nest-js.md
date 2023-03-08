---
title: 051: Nest.js로 다중 테넌트 애플리케이션 구축 및 배포
description: 
published: true
date: 2023-02-02T01:17:44.943Z
tags: 
editor: markdown
dateCreated: 2023-02-02T01:17:40.780Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [051: Building and deploying multi-tenant applications with Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/051-building-and-deploying-multi-tenant-applications-with-nest-js)
{.links-list}


# 소개

Nest.js는 확장 가능한 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. JavaScript의 상위 집합인 TypeScript를 사용하고 Node.js와 TypeScript의 이점을 결합하여 애플리케이션을 개발합니다.

Nest.js는 효율적이고 확장 가능한 Node.js 서버 측 애플리케이션을 구축하는 데 도움이 되는 프레임워크입니다. 이 프레임워크는 JavaScript의 상위 집합인 TypeScript를 사용하고 Node.js와 TypeScript의 이점을 결합하여 애플리케이션을 개발합니다.

Nest.js는 효율적이고 확장 가능한 Node.js 서버 측 애플리케이션을 구축하기 위한 프레임워크입니다. JavaScript의 상위 집합인 TypeScript를 사용하고 Node.js와 TypeScript의 이점을 결합합니다. Nest.js를 사용하면 일반 Node.js로 작성된 애플리케이션보다 유지 관리, 확장 및 테스트가 더 쉬운 애플리케이션을 개발할 수 있습니다.

# 멀티 테넌트 애플리케이션이란 무엇입니까?

다중 테넌트 애플리케이션은 여러 테넌트에 서비스를 제공하도록 설계된 애플리케이션입니다. 테넌트는 애플리케이션에 대한 공통 액세스를 공유하는 사용자 그룹입니다.

다중 테넌트 애플리케이션은 여러 테넌트에 서비스를 제공하도록 설계되었습니다. 테넌트는 애플리케이션에 대한 공통 액세스를 공유하는 사용자 그룹입니다.

다중 테넌트 애플리케이션에는 기존 애플리케이션과 다른 몇 가지 주요 기능이 있습니다.

- 각 임차인은 전용 응용 프로그램 인스턴스를 가집니다.
- 임차인은 서로 격리될 수 있습니다.
- 테넌트는 애플리케이션에 대한 다양한 수준의 액세스 권한을 부여받을 수 있습니다.

# 다중 테넌트 애플리케이션을 사용하는 이유는 무엇입니까?

다중 테넌트 애플리케이션에는 기존 애플리케이션에 비해 몇 가지 주요 이점이 있습니다.

- 격리: 세입자는 서로 격리됩니다. 이는 한 테넌트의 데이터에 다른 테넌트가 액세스할 수 없음을 의미합니다.
- 보안: 테넌트에게 애플리케이션에 대한 다양한 수준의 액세스 권한을 부여할 수 있습니다. 즉, 누가 어떤 데이터에 액세스할 수 있는지 제어할 수 있습니다.
- 확장성: 각 테넌트에는 전용 애플리케이션 인스턴스가 있습니다. 이는 응용 프로그램이 각 테넌트의 요구 사항에 맞게 확장될 수 있음을 의미합니다.

# Nest.js로 다중 테넌트 애플리케이션을 구축하는 방법

Nest.js로 다중 테넌트 애플리케이션을 구축하는 것은 쉽습니다. Nest.js는 테넌트를 서로 격리하는 데 사용할 수 있는 TenantModule을 제공합니다.

TenantModule을 사용하려면 테넌트별로 TenantModule을 생성해야 합니다. TenantModule에는 테넌트에 대한 구성이 포함되어 있습니다.

```javascript
import { Module } from '@nestjs/common';
import { TenantModule } from '@nestjs/tenant';

@Module({
  imports: [
    TenantModule.forRoot({
      tenants: [
        {
          id: 'tenant-1',
          name: 'Tenant 1',
          database: 'tenant1'
        },
        {
          id: 'tenant-2',
          name: 'Tenant 2',
          database: 'tenant2'
        }
      ]
    })
  ]
})
export class AppModule {}
```

forRoot() 메서드는 테넌트 배열이 포함된 옵션 개체를 사용합니다. tenants 배열에는 ID, 이름 및 데이터베이스 속성이 있는 객체가 포함됩니다.

id 속성은 테넌트의 고유 식별자입니다. 이름 속성은 테넌트의 이름입니다. 데이터베이스 속성은 테넌트가 사용할 데이터베이스의 이름입니다.

# 다중 테넌트 애플리케이션을 배포하는 방법

다중 테넌트 애플리케이션을 배포하는 것은 쉽습니다. Nest.js는 애플리케이션을 여러 테넌트에 배포하는 데 사용할 수 있는 TenantModule을 제공합니다.

TenantModule을 사용하려면 테넌트별로 TenantModule을 생성해야 합니다. TenantModule에는 테넌트에 대한 구성이 포함되어 있습니다.

```javascript
import { Module } from '@nestjs/common';
import { TenantModule } from '@nestjs/tenant';

@Module({
  imports: [
    TenantModule.forRoot({
      tenants: [
        {
          id: 'tenant-1',
          name: 'Tenant 1',
          database: 'tenant1'
        },
        {
          id: 'tenant-2',
          name: 'Tenant 2',
          database: 'tenant2'
        }
      ]
    })
  ]
})
export class AppModule {}
```

forRoot() 메서드는 테넌트 배열이 포함된 옵션 개체를 사용합니다. tenants 배열에는 ID, 이름 및 데이터베이스 속성이 있는 객체가 포함됩니다.

id 속성은 테넌트의 고유 식별자입니다. 이름 속성은 테넌트의 이름입니다. 데이터베이스 속성은 테넌트가 사용할 데이터베이스의 이름입니다.

# 결론

이 게시물에서는 다중 테넌트 애플리케이션과 이를 Nest.js로 빌드하고 배포하는 방법에 대해 배웠습니다. 다중 테넌트 애플리케이션에는 격리, 보안 및 확장성을 포함하여 기존 애플리케이션에 비해 몇 가지 주요 이점이 있습니다.