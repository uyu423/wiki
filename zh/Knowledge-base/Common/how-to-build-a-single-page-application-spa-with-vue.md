---
title: 如何使用 Vue 构建单页应用程序 (SPA)
description: 
published: true
date: 2023-02-17T18:17:03.859Z
tags: 
editor: markdown
dateCreated: 2023-01-31T02:04:33.897Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [How to Build a Single-Page Application (SPA) with Vue***English** version of this document is available*](/en/Knowledge-base/Common/how-to-build-a-single-page-application-spa-with-vue)
{.links-list}


# 如何使用 Vue 构建单页应用程序 (SPA)

开发单页应用程序 (SPA) 是构建现代 Web 应用程序的一种流行方法。 SPA 往往速度快、响应迅速，并提供丰富的用户体验 (UX)。

在本文中，我们将向您展示如何使用 Vue 构建 SPA。我们将从使用 Vue CLI 构建一个新的 Vue 项目开始。然后，我们将创建一个简单的组件并将其连接到 Vue 路由器。最后，我们将把我们的应用程序部署到 Netlify。

## 搭建一个新项目

我们需要做的第一件事是搭建一个新的 Vue 项目。我们可以使用 Vue CLI 来做到这一点。

如果你没有安装 Vue CLI，你可以使用 npm 安装它：

```bash
npm install -g @vue/cli
```

安装 Vue CLI 后，我们可以使用 `vue create` 命令创建一个新项目：

```bash
vue create my-app
```

Vue CLI 会提示我们选择一个预设。我们可以选择 Babel 和 eslint-plugin-vue 自带的默认预设，也可以选择“Manually select features”选项，选择我们想要的功能。

对于本文，我们将选择默认预设。

##创建一个组件

现在我们有了一个新的 Vue 项目，我们可以创建我们的第一个组件了。我们将从创建一个名为 `src/components/Hello.vue` 的文件开始：

```vue
<template>
  <div>
    <h1>Hello, World!</h1>
  </div>
</template>

<script>
export default {
  name: "Hello"
};
</script>

<style>
div {
  text-align: center;
}
</style>
```

这是一个非常简单的组件，只显示一个标题。

## 连接 Vue 路由器

现在我们有了我们的组件，我们需要将它连接到 Vue 路由器。 Vue 路由器是一个库，我们可以使用它在 Vue 应用程序中设置路由。

首先，我们需要安装 Vue 路由器：

```bash
npm install --save vue-router
```

安装 Vue 路由器后，我们可以创建一个名为 src/router.js 的文件并添加以下代码：

```javascript
import Vue from "vue";
import VueRouter from "vue-router";
import Hello from "./components/Hello";

Vue.use(VueRouter);

export default new VueRouter({
  routes: [
    {
      path: "/",
      name: "Hello",
      component: Hello
    }
  ]
});
```

在此文件中，我们导入之前创建的“Hello”组件。然后我们创建一个新的 VueRouter 实例并指定我们的路由。在这种情况下，我们只有一个路由可以转到“/”路径并呈现“Hello”组件。

现在我们已经设置了路由，我们需要告诉我们的 Vue 实例使用路由器。我们可以通过修改 src/main.js 来做到这一点：

```javascript
import Vue from 'vue'
import App from './App.vue'
import router from './router'

Vue.config.productionTip = false

new Vue({
  router,
  render: h => h(App)
}).$mount('#app')
```

首先，我们导入我们之前创建的 `router` 实例。然后，我们告诉我们的“新 Vue”实例使用路由器。

## 部署到 Netlify

现在我们的应用程序已经完成，我们可以将它部署到 Netlify。 Netlify 是一种可以轻松部署静态 Web 应用程序的服务。

首先，我们需要在项目的根目录中创建一个名为 netlify.toml 的文件：

```toml
[build]
  command = "npm run build"
  functions = "functions"
```

该文件告诉 Netlify 要运行什么命令来构建我们的应用程序。在这种情况下，我们只是运行“npm run build”命令。

接下来，我们需要在项目的根目录中创建一个名为 .gitignore 的文件并添加以下行：

```
/node_modules
/functions
/.netlify
```

该文件告诉 Git 忽略 `node_modules`、`functions` 和 `.netlify` 目录。这很重要，因为我们不想将这些目录包含在我们的 Git 存储库中。

最后，我们可以创建一个 Netlify 帐户并部署我们的应用程序。

## 结论

在本文中，我们向您展示了如何使用 Vue 构建 SPA。我们从搭建一个新的 Vue 项目开始。然后，我们创建了一个简单的组件并将其连接到 Vue 路由器。最后，我们将应用程序部署到 Netlify。