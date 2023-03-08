---
title: Angular
description: 
published: true
date: 2023-02-10T11:17:58.896Z
tags: 
editor: markdown
dateCreated: 2023-02-10T11:17:56.948Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Angular***English** document is available*](/en/Knowledge-base/Dictionary/angular)
{.links-list}


# 角度

## 概述
Angular 是由 Google 创建和维护的开源 Web 应用程序框架。它用于开发单页 Web 应用程序和移动应用程序。它是用 TypeScript 编写的，基于模型-视图-控制器 (MVC) 设计模式。

## 描述
Angular 是一个用于开发 Web 应用程序的框架，它基于模型-视图-控制器 (MVC) 设计模式。它是用 TypeScript 编写的，由谷歌维护。它旨在用于开发单页应用程序以及移动应用程序。

Angular 由几个组件组成，包括 Angular CLI（命令行界面）、Angular 编译器和 Angular 核心。 Angular CLI 用于创建和管理 Angular 项目，而 Angular Compiler 用于编译 TypeScript 代码。 Angular 核心是包含用于创建应用程序的核心组件和服务的主要框架。

Angular 还包括其他几个库和工具，例如用于管理应用程序中的路由的 Angular Router 和用于创建和管理表单的 Angular Forms 库。

## 特征
Angular 包含几个特性，使其成为 Web 和移动应用程序开发的有吸引力的选择。这些功能包括：

- 支持 TypeScript：Angular 是用 TypeScript 编写的，它是 JavaScript 的超集。这允许开发人员使用该语言的最新功能，同时仍然可以访问 JavaScript 的功能。

- 基于组件的架构：Angular 使用基于组件的架构，允许开发人员创建模块化和可重用的组件。这使得维护和扩展应用程序变得更加容易。

- 模块化：Angular 允许开发人员模块化他们的代码，这使得管理和维护应用程序变得更加容易。

- 反应式编程：Angular 使用反应式编程模型，允许开发人员创建对用户输入响应更快的应用程序。

- 工具：Angular 包括几个使开发应用程序更容易的工具，例如用于创建和管理项目的 Angular CLI，以及用于编译 TypeScript 代码的 Angular Compiler。

## 例子
以下是显示用户列表的 Angular 应用程序示例。该应用程序使用 Angular CLI 创建项目，使用 Angular Router 管理路由，使用 Angular Forms 库创建和管理表单。

```
import { Component, OnInit } from '@angular/core';
import { Router } from '@angular/router';
import { FormGroup, FormControl, Validators } from '@angular/forms';

@Component({
  selector: 'app-user-list',
  templateUrl: './user-list.component.html',
  styleUrls: ['./user-list.component.css']
})
export class UserListComponent implements OnInit {
  users: any[];
  userForm: FormGroup;

  constructor(private router: Router) { }

  ngOnInit() {
    this.userForm = new FormGroup({
      name: new FormControl('', Validators.required),
      email: new FormControl('', [Validators.required, Validators.email])
    });
  }

  onSubmit() {
    this.users.push(this.userForm.value);
    this.router.navigate(['/users']);
  }

}
```

## 优点和缺点
Angular 有几个优点和缺点，在选择框架时应该考虑这些优点和缺点。

**优点：**

- 易于使用：Angular 相对易于使用，并且拥有庞大的开发人员社区，可以提供支持和资源。

- 模块化：Angular 允许开发人员模块化他们的代码，这使得维护和扩展应用程序变得更加容易。

- 反应式编程：Angular 使用反应式编程模型，允许开发人员创建对用户输入响应更快的应用程序。

**缺点：**

- 陡峭的学习曲线：Angular 的学习曲线陡峭，可能需要一些时间才能精通该框架。

- 复杂性：Angular 可能非常复杂，并且很难对应用程序进行调试和故障排除。

- 性能：由于框架的复杂性，Angular 应用程序可能比使用其他框架构建的应用程序慢。

## 相关技术
Angular 与其他几种技术相关，例如 TypeScript、React 和 Vue.js。 TypeScript 是 Angular 所使用的语言，它是 JavaScript 的超集。 React 和 Vue.js 都是用于构建 Web 应用程序的流行 JavaScript 框架。

## 题外话
Angular 是一个开源框架，许多公司和组织都使用它来开发 Web 和移动应用程序。由于其易用性以及对 TypeScript 和其他技术的支持，它对开发人员来说是一个有吸引力的选择。

## 其他的
Angular 自 2010 年首次发布以来越来越受欢迎，现在它是最流行的 Web 应用程序框架之一。它被许多公司使用，包括谷歌、微软和苹果。