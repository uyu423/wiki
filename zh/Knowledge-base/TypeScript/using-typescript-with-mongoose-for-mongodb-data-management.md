---
title: 使用 TypeScript 和 Mongoose 进行 MongoDB 数据管理
description: 
published: true
date: 2023-02-01T08:18:10.732Z
tags: 
editor: markdown
dateCreated: 2023-02-01T08:18:09.316Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Using TypeScript with Mongoose for MongoDB Data Management***English** version of this document is available*](/en/Knowledge-base/TypeScript/using-typescript-with-mongoose-for-mongodb-data-management)
{.links-list}


  文章的标题应该是“Using TypeScript with Mongoose for MongoDB Data Management”。

# 使用 TypeScript 和 Mongoose 进行 MongoDB 数据管理

Mongoose 是一个对象数据建模 (ODM) 库，它提供基于模式的解决方案来为 MongoDB 数据建模。它是用 JavaScript 编写的，可用于 Node.js 和 Web 应用程序。

TypeScript 是 JavaScript 的类型化超集，可编译为纯 JavaScript。它提供类、模块和接口来帮助您构建健壮的组件。

在本文中，我们将向您展示如何将 TypeScript 与 Mongoose 结合使用。我们将创建一个简单的示例来演示将 TypeScript 与 Mongoose 结合使用的好处。

## 为什么将 TypeScript 与猫鼬一起使用？

TypeScript 是一种功能强大的语言，可以帮助您编写更好的代码。类型系统可以在代码执行之前的编译时捕获错误。这可以节省您的时间并帮助您避免潜在的错误。

此外，TypeScript 对模块和类的支持可以帮助您更好地组织代码。这可以使您的代码更易于维护且更易于理解。

## 设置 TypeScript 和 Mongoose

在我们开始之前，我们需要设置 TypeScript 和 Mongoose。

首先，使用 npm 安装 TypeScript 和 Mongoose：

```
npm install -g typescript
npm install mongoose
```

接下来，创建一个名为 schema.ts 的文件并添加以下代码：

```typescript
import * as mongoose from 'mongoose';

const Schema = mongoose.Schema;

const userSchema = new Schema({
  name: String,
  age: Number,
  email: String
});

const User = mongoose.model('User', userSchema);

export default User;
```

此代码为“用户”模型创建一个架构。该架构包括“姓名”、“年龄”和“电子邮件”字段。我们将在下一节中使用此架构创建一个“用户”模型。

## 创建用户模型

现在我们有了一个模式，我们可以创建一个模型。模型是我们可以用来查询数据库的模式实例。

要创建模型，我们将以下代码添加到 schema.ts 文件中：

```typescript
import * as mongoose from 'mongoose';

const Schema = mongoose.Schema;

const userSchema = new Schema({
  name: String,
  age: Number,
  email: String
});

const User = mongoose.model('User', userSchema);

const user = new User({
  name: 'John',
  age: 25,
  email: 'john@example.com'
});

user.save((err, user) => {
  if (err) {
    console.log(err);
  } else {
    console.log(user);
  }
});

export default User;
```

在这段代码中，我们创建了一个新的 `User` 模型并将其保存到数据库中。我们可以使用 `save` 方法将模型保存到数据库中。此方法采用在保存模型时调用的回调函数。

回调函数有两个参数：`err` 和 `user`。 `err` 是一个错误对象，在保存模型时出现错误时设置。 `user` 是保存的模型。

## 查询数据库

保存模型后，我们可以查询数据库以获取保存的数据。

要查询数据库，我们将以下代码添加到 schema.ts 文件中：

```typescript
import * as mongoose from 'mongoose';

const Schema = mongoose.Schema;

const userSchema = new Schema({
  name: String,
  age: Number,
  email: String
});

const User = mongoose.model('User', userSchema);

User.find((err, users) => {
  if (err) {
    console.log(err);
  } else {
    console.log(users);
  }
});

export default User;
```

在这段代码中，我们使用 `find` 方法来查询数据库。此方法采用在查询完成时调用的回调函数。

回调函数有两个参数：`err` 和 `users`。 `err` 是一个错误对象，如果查询数据库出错则设置该错误对象。 `users` 是与查询匹配的模型数组。

## 删除用户

我们还可以从数据库中删除用户。为此，我们将以下代码添加到 `schema.ts` 文件中：

```typescript
import * as mongoose from 'mongoose';

const Schema = mongoose.Schema;

const userSchema = new Schema({
  name: String,
  age: Number,
  email: String
});

const User = mongoose.model('User', userSchema);

User.findByIdAndRemove('5b9d7d4f4a6d4e0f1046b82b', (err, user) => {
  if (err) {
    console.log(err);
  } else {
    console.log(user);
  }
});

export default User;
```

在此代码中，我们使用“findByIdAndRemove”方法从数据库中删除用户。此方法采用要删除的用户的“_id”和一个回调函数。

回调函数有两个参数：`err` 和 `user`。 `err` 是一个错误对象，如果删除用户时出错，则设置该对象。 `user` 是被删除的用户。

## 更新用户

我们还可以更新数据库中的用户。为此，我们将以下代码添加到 `schema.ts` 文件中：

```typescript
import * as mongoose from 'mongoose';

const Schema = mongoose.Schema;

const userSchema = new Schema({
  name: String,
  age: Number,
  email: String
});

const User = mongoose.model('User', userSchema);

User.findByIdAndUpdate('5b9d7d4f4a6d4e0f1046b82b', { name: 'Jane' }, { new: true }, (err, user) => {
  if (err) {
    console.log(err);
  } else {
    console.log(user);
  }
});

export default User;
```

在此代码中，我们使用“findByIdAndUpdate”方法更新数据库中的用户。此方法采用要更新的用户的“_id”、要更新的字段和一个回调函数。

回调函数有两个参数：`err` 和 `user`。 `err` 是一个错误对象，如果更新用户时出现错误，则设置该错误对象。 `user` 是更新后的用户。

## 结论

在本文中，我们向您展示了如何将 TypeScript 与 Mongoose 结合使用。我们创建了一个简单的示例来演示将 TypeScript 与 Mongoose 结合使用的好处。

TypeScript 是一种功能强大的语言，可以帮助您编写更好的代码。类型系统可以在代码执行之前的编译时捕获错误。这可以节省您的时间并帮助您避免潜在的错误。

此外，TypeScript 对模块和类的支持可以帮助您更好地组织代码。这可以使您的代码更易于维护且更易于理解。

如果您正在为 MongoDB 寻找类型化解决方案，那么 TypeScript 和 Mongoose 是一个不错的选择。