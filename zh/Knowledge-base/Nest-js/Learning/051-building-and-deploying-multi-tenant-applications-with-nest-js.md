---
title: 051：使用 Nest.js 构建和部署多租户应用程序
description: 
published: true
date: 2023-02-02T01:17:44.943Z
tags: 
editor: markdown
dateCreated: 2023-02-02T01:17:40.780Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [051: Building and deploying multi-tenant applications with Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/051-building-and-deploying-multi-tenant-applications-with-nest-js)
{.links-list}


# 介绍

Nest.js 是一个用于构建可扩展的服务器端应用程序的 Node.js 框架。它使用 JavaScript 的超集 TypeScript，并结合了 Node.js 和 TypeScript 的优点来开发应用程序。

Nest.js 是一个框架，可帮助您构建高效、可扩展的 Node.js 服务器端应用程序。该框架使用 JavaScript 的超集 TypeScript，并结合了 Node.js 和 TypeScript 的优点来开发应用程序。

Nest.js 是一个用于构建高效、可扩展的 Node.js 服务器端应用程序的框架。它使用 TypeScript（JavaScript 的超集），并结合了 Node.js 和 TypeScript 的优点。使用 Nest.js，您可以开发比使用 vanilla Node.js 编写的应用程序更易于维护、更易于扩展且更易于测试的应用程序。

# 什么是多租户应用程序？

多租户应用程序是旨在为多个租户提供服务的应用程序。租户是共享对应用程序的公共访问权限的一组用户。

多租户应用程序旨在为多个租户提供服务。租户是共享对应用程序的公共访问权限的一组用户。

多租户应用程序具有一些与传统应用程序不同的关键特性：

- 每个租户都有自己的专用应用程序实例。
- 租户可以相互隔离。
- 可以为租户提供不同级别的应用程序访问权限。

# 为什么要使用多租户应用程序？

与传统应用程序相比，多租户应用程序具有几个关键优势：

- 隔离：租户彼此隔离。这意味着一个租户的数据不能被另一个租户访问。
- 安全性：可以为租户提供不同级别的应用程序访问权限。这意味着您可以控制谁可以访问哪些数据。
- 可扩展性：每个租户都有自己的专用应用程序实例。这意味着应用程序可以扩展以满足每个租户的需求。

# 如何使用 Nest.js 构建多租户应用程序

使用 Nest.js 构建多租户应用程序很容易。 Nest.js 提供了一个 TenantModule，您可以使用它来将租户彼此隔离。

要使用 TenantModule，您需要为每个租户创建一个 TenantModule。 TenantModule 包含租户的配置。

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

forRoot() 方法采用包含租户数组的选项对象。租户数组包含具有 ID、名称和数据库属性的对象。

id 属性是租户的唯一标识符。 name 属性是租户的名字。 database 属性是租户将使用的数据库的名称。

# 如何部署多租户应用程序

部署多租户应用程序很容易。 Nest.js 提供了一个 TenantModule，您可以使用它来将您的应用程序部署到多个租户。

要使用 TenantModule，您需要为每个租户创建一个 TenantModule。 TenantModule 包含租户的配置。

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

forRoot() 方法采用包含租户数组的选项对象。租户数组包含具有 ID、名称和数据库属性的对象。

id 属性是租户的唯一标识符。 name 属性是租户的名字。 database 属性是租户将使用的数据库的名称。

# 结论

在本文中，我们了解了多租户应用程序以及如何使用 Nest.js 构建和部署它们。与传统应用程序相比，多租户应用程序具有一些关键优势，包括隔离、安全性和可伸缩性。