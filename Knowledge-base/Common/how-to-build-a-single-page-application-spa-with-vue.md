---
title: Vue로 단일 페이지 애플리케이션(SPA)을 구축하는 방법
description: 
published: true
date: 2023-02-17T18:17:01.130Z
tags: 
editor: markdown
dateCreated: 2023-01-31T02:04:33.896Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [How to Build a Single-Page Application (SPA) with Vue***English** version of this document is available*](/en/Knowledge-base/Common/how-to-build-a-single-page-application-spa-with-vue)
{.links-list}


# Vue로 단일 페이지 애플리케이션(SPA)을 구축하는 방법

SPA(단일 페이지 애플리케이션) 개발은 최신 웹 애플리케이션을 구축하는 데 널리 사용되는 접근 방식입니다. SPA는 빠르고 반응이 빠르고 풍부한 사용자 경험(UX)을 제공하는 경향이 있습니다.

이 기사에서는 Vue로 SPA를 구축하는 방법을 보여줍니다. Vue CLI를 사용하여 새 Vue 프로젝트를 스캐폴딩하는 것으로 시작하겠습니다. 그런 다음 간단한 구성 요소를 만들어 Vue 라우터에 연결합니다. 마지막으로 애플리케이션을 Netlify에 배포합니다.

## 새 프로젝트 비계

가장 먼저 해야 할 일은 새로운 Vue 프로젝트를 스캐폴딩하는 것입니다. Vue CLI를 사용하여 이 작업을 수행할 수 있습니다.

Vue CLI가 설치되어 있지 않은 경우 npm을 사용하여 설치할 수 있습니다.

```bash
npm install -g @vue/cli
```

Vue CLI가 설치되면 `vue create` 명령을 사용하여 새 프로젝트를 만들 수 있습니다.

```bash
vue create my-app
```

Vue CLI는 사전 설정을 선택하라는 메시지를 표시합니다. Babel 및 eslint-plugin-vue와 함께 제공되는 기본 사전 설정을 선택하거나 "수동으로 기능 선택" 옵션을 선택하고 원하는 기능을 선택할 수 있습니다.

이 문서에서는 기본 사전 설정을 선택합니다.

##구성 요소 만들기

이제 새 Vue 프로젝트가 있으므로 첫 번째 구성 요소를 만들 수 있습니다. `src/components/Hello.vue`라는 파일을 생성하여 시작하겠습니다.

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

제목만 표시하는 매우 간단한 구성 요소입니다.

## Vue 라우터 연결

이제 구성 요소가 있으므로 Vue 라우터에 연결해야 합니다. Vue 라우터는 Vue 애플리케이션에서 라우팅을 설정하는 데 사용할 수 있는 라이브러리입니다.

먼저 Vue 라우터를 설치해야 합니다.

```bash
npm install --save vue-router
```

Vue 라우터가 설치되면 `src/router.js`라는 파일을 만들고 다음 코드를 추가할 수 있습니다.

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

이 파일에서 이전에 생성한 `Hello` 구성 요소를 가져옵니다. 그런 다음 새로운 `VueRouter` 인스턴스를 생성하고 경로를 지정합니다. 이 경우에는 `/` 경로로 이동하고 `Hello` 구성 요소를 렌더링하는 하나의 경로만 있습니다.

이제 경로를 설정했으므로 Vue 인스턴스에 라우터를 사용하도록 지시해야 합니다. `src/main.js`를 수정하면 됩니다.

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

먼저 이전에 생성한 `router` 인스턴스를 가져옵니다. 그런 다음 `new Vue` 인스턴스에 라우터를 사용하도록 지시합니다.

## Netlify에 배포

이제 애플리케이션이 완성되었으므로 Netlify에 배포할 수 있습니다. Netlify는 정적 웹 애플리케이션을 쉽게 배포할 수 있게 해주는 서비스입니다.

먼저 프로젝트의 루트에 `netlify.toml`이라는 파일을 만들어야 합니다.

```toml
[build]
  command = "npm run build"
  functions = "functions"
```

이 파일은 Netlify에게 애플리케이션을 빌드하기 위해 실행할 명령을 알려줍니다. 이 경우에는 `npm run build` 명령만 실행하고 있습니다.

다음으로 프로젝트의 루트에 `.gitignore`라는 파일을 만들고 다음 줄을 추가해야 합니다.

```
/node_modules
/functions
/.netlify
```

이 파일은 Git에게 `node_modules`, `functions` 및 `.netlify` 디렉토리를 무시하도록 지시합니다. Git 리포지토리에 이러한 디렉터리를 포함하고 싶지 않기 때문에 이는 중요합니다.

마지막으로 Netlify 계정을 만들고 애플리케이션을 배포할 수 있습니다.

## 결론

이 기사에서는 Vue로 SPA를 구축하는 방법을 보여주었습니다. 우리는 새로운 Vue 프로젝트를 스캐폴딩하는 것으로 시작했습니다. 그런 다음 간단한 구성 요소를 만들어 Vue 라우터에 연결했습니다. 마지막으로 애플리케이션을 Netlify에 배포했습니다.