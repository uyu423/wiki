---
title: 012: 在 Nest.js 中使用守卫进行路由保护
description: 
published: true
date: 2023-02-14T22:32:14.239Z
tags: 
editor: markdown
dateCreated: 2023-02-14T22:32:12.577Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [012: Using guards for route protection in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/012-using-guards-for-route-protection-in-nest-js)
{.links-list}


# 在 Nest.js 中使用 guards 进行路由保护

在这篇文章中，我们将研究如何在 Nest.js 中使用守卫来保护路由。我们将从对守卫是什么以及它们如何工作的基本了解开始，然后我们将研究如何使用它们来保护我们的路线。

## 什么是守卫？

守卫是可用于保护路线的功能。它们可用于检查用户是否已登录、是否具有必要的权限或是否满足任何其他条件。如果不满足标准，守卫将阻止用户访问该路线。

## 守卫是如何工作的？

Guards 在 Nest.js 中注册为中间件。这意味着它们将在路由处理程序之前执行。如果守卫返回 true ，则该路由将是可访问的。如果守卫返回 `false`，则路由将不可访问。

## 如何使用守卫来保护路由？

Guards 可以通过多种方式来保护路由。例如，守卫可用于在允许用户访问路线之前检查用户是否已登录。如果用户未登录，守卫将阻止他们访问该路线。

另一种使用守卫的方法是在允许用户访问路由之前检查用户是否具有必要的权限。例如，如果路由要求用户是管理员，则可以使用守卫来检查用户是否具有 admin 权限。如果他们没有权限，守卫将阻止他们访问该路线。

## 结论

在这篇文章中，我们研究了如何在 Nest.js 中使用守卫来保护路由。守卫是可用于在允许用户访问路由之前检查用户是否满足必要条件的功能。它们可用于检查用户是否已登录、是否具有必要的权限或是否满足任何其他条件。