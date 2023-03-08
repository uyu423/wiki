---
title: How to Build a Single-Page Application (SPA) with Vue
description: 
published: true
date: 2023-02-17T18:16:59.766Z
tags: 
editor: markdown
dateCreated: 2023-01-31T02:04:33.895Z
---

- [Vue로 단일 페이지 애플리케이션(SPA)을 구축하는 방법***Korean** version of this document is available*](/ko/Knowledge-base/Common/how-to-build-a-single-page-application-spa-with-vue)
{.links-list}
- [Vue でシングルページ アプリケーション (SPA) を構築する方法***Japanese** version of this document is available*](/ja/Knowledge-base/Common/how-to-build-a-single-page-application-spa-with-vue)
{.links-list}
- [如何使用 Vue 构建单页应用程序 (SPA)***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Common/how-to-build-a-single-page-application-spa-with-vue)
{.links-list}


# How to Build a Single-Page Application (SPA) with Vue

Developing a single-page application (SPA) is a popular approach for building modern web applications. SPAs tend to be fast, responsive, and provide a rich user experience (UX).

In this article, we'll show you how to build a SPA with Vue. We'll start by scaffolding a new Vue project using the Vue CLI. Then, we'll create a simple component and wire it up to the Vue router. Finally, we'll deploy our application to Netlify.

## Scaffolding a New Project

The first thing we need to do is scaffold a new Vue project. We can do this using the Vue CLI.

If you don't have the Vue CLI installed, you can install it using npm:

```bash
npm install -g @vue/cli
```

Once the Vue CLI is installed, we can create a new project using the `vue create` command:

```bash
vue create my-app
```

The Vue CLI will prompt us to select a preset. We can choose the default preset, which comes with Babel and eslint-plugin-vue, or we can select the "Manually select features" option and choose the features we want.

For this article, we'll choose the default preset.

##Creating a Component

Now that we have a new Vue project, we can create our first component. We'll start by creating a file called `src/components/Hello.vue`:

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

This is a very simple component that just displays a heading.

## Wiring up the Vue Router

Now that we have our component, we need to wire it up to the Vue router. The Vue router is a library that we can use to set up routing in our Vue application.

First, we need to install the Vue router:

```bash
npm install --save vue-router
```

Once the Vue router is installed, we can create a file called `src/router.js` and add the following code:

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

In this file, we import the `Hello` component that we created earlier. We then create a new `VueRouter` instance and specify our routes. In this case, we just have one route that goes to the `/` path and renders the `Hello` component.

Now that we have our routes set up, we need to tell our Vue instance to use the router. We can do this by modifying `src/main.js`:

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

First, we import the `router` instance that we created earlier. Then, we tell our `new Vue` instance to use the router.

## Deploying to Netlify

Now that our application is complete, we can deploy it to Netlify. Netlify is a service that makes it easy to deploy static web applications.

First, we need to create a file called `netlify.toml` in the root of our project:

```toml
[build]
  command = "npm run build"
  functions = "functions"
```

This file tells Netlify what command to run to build our application. In this case, we're just running the `npm run build` command.

Next, we need to create a file called `.gitignore` in the root of our project and add the following lines:

```
/node_modules
/functions
/.netlify
```

This file tells Git to ignore the `node_modules`, `functions`, and `.netlify` directories. This is important because we don't want to include these directories in our Git repository.

Finally, we can create a Netlify account and deploy our application.

## Conclusion

In this article, we showed you how to build a SPA with Vue. We started by scaffolding a new Vue project. Then, we created a simple component and wired it up to the Vue router. Finally, we deployed our application to Netlify.