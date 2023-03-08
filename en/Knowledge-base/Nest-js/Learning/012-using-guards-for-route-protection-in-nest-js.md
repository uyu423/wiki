---
title: 012: Using guards for route protection in Nest.js
description: 
published: true
date: 2023-02-14T22:32:20.003Z
tags: 
editor: markdown
dateCreated: 2023-02-14T22:32:12.581Z
---

- [012: uso de guardias para la protección de rutas en Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/012-using-guards-for-route-protection-in-nest-js)
{.links-list}
- [012: 在 Nest.js 中使用守卫进行路由保护***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/012-using-guards-for-route-protection-in-nest-js)
{.links-list}
- [012: Nest.js에서 경로 보호를 위해 가드 사용***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/012-using-guards-for-route-protection-in-nest-js)
{.links-list}


# Using guards for route protection in Nest.js

In this post, we'll be looking at how to use guards in Nest.js to protect routes. We'll be starting with a basic understanding of what guards are and how they work, and then we'll look at how to use them to protect our routes.

## What are guards?

Guards are functions that can be used to protect routes. They can be used to check if a user is logged in, if they have the necessary permissions, or if they meet any other criteria. If the criteria are not met, the guard will prevent the user from accessing the route.

## How do guards work?

Guards are registered with Nest.js as middleware. This means that they will be executed before the route handler. If the guard returns `true`, the route will be accessible. If the guard returns `false`, the route will be inaccessible.

## How can guards be used to protect routes?

Guards can be used to protect routes in a number of ways. For example, a guard can be used to check if a user is logged in before allowing them to access a route. If the user is not logged in, the guard will prevent them from accessing the route.

Another way to use guards is to check if a user has the necessary permissions before allowing them to access a route. For example, if a route requires a user to be an administrator, a guard can be used to check if the user has the `admin` permission. If they do not have the permission, the guard will prevent them from accessing the route.

## Conclusion

In this post, we've looked at how to use guards in Nest.js to protect routes. Guards are functions that can be used to check if a user meets the necessary criteria before allowing them to access a route. They can be used to check if a user is logged in, if they have the necessary permissions, or if they meet any other criteria.