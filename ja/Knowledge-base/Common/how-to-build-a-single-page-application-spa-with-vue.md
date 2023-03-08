---
title: Vue でシングルページ アプリケーション (SPA) を構築する方法
description: 
published: true
date: 2023-02-17T18:17:02.514Z
tags: 
editor: markdown
dateCreated: 2023-01-31T02:04:33.896Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [How to Build a Single-Page Application (SPA) with Vue***English** version of this document is available*](/en/Knowledge-base/Common/how-to-build-a-single-page-application-spa-with-vue)
{.links-list}


# Vueでシングルページアプリケーション（SPA）を構築する方法

SPA（シングルページアプリケーション）開発は、最新のWebアプリケーションを構築するために広く使用されているアプローチです。 SPAは、迅速で応答性が高く、豊富なユーザーエクスペリエンス（UX）を提供する傾向があります。

この記事では、VueでSPAを構築する方法を説明します。 Vue CLIを使用して新しいVueプロジェクトをスキャフォールディングすることから始めましょう。次に、単純なコンポーネントを作成してVueルーターに接続します。最後に、アプリケーションをNetlifyにデプロイします。

## 新しいプロジェクト足場

最初にすべきことは、新しいVueプロジェクトをスキャフォールディングすることです。 Vue CLIを使用してこれを行うことができます。

Vue CLI がインストールされていない場合は、npm を使用してインストールできます。

```bash
npm install -g @vue/cli
```

Vue CLIがインストールされたら、 `vue create`コマンドを使用して新しいプロジェクトを作成できます。

```bash
vue create my-app
```

Vue CLI はプリセットを選択するように求められます。 Babelおよびeslint-plugin-vueに付属のデフォルトプリセットを選択するか、「手動で機能を選択」オプションを選択して目的の機能を選択できます。

この資料では、デフォルトプリセットを選択します。

##コンポーネントの作成

これで新しいVueプロジェクトがあるので、最初のコンポーネントを作成できます。 `src/components/Hello.vue`というファイルを生成することから始めましょう。

「vue
<template>
  <div>
    <h1>Hello、World！</h1>
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

タイトルのみを表示する非常に単純なコンポーネントです。

## Vueルータ接続

コンポーネントがあるので、Vueルーターに接続する必要があります。 Vueルータは、Vueアプリケーションでルーティングを設定するために使用できるライブラリです。

まず、Vueルーターをインストールする必要があります。

```bash
npm install --save vue-router
```

Vueルータがインストールされたら、 `src/router.js`というファイルを作成し、次のコードを追加できます。

```javascript
import Vue from "vue";
import VueRouter from "vue-router";
import Hello from "./components/Hello";

Vue.use（VueRouter）;

export default new VueRouter({
  routes: [
    {
      path: "/",
      name: "Hello",
      component: Hello
    }
  ]
}）;
```

このファイルから以前に作成した `Hello` コンポーネントを取得します。次に、新しい `VueRouter` インスタンスを作成し、パスを指定します。この場合、 `/` パスに移動して `Hello` コンポーネントをレンダリングする 1 つのパスしかありません。

これでルートを設定したので、Vueインスタンスにルーターを使用するように指示する必要があります。 `src/main.js`を修正するだけです。

```javascript
import Vue from 'vue'
import App from './App.vue'
import router from './router'

Vue.config.productionTip = false

new Vue({
  ルーター、
  render: h => h(App)
}).$mount('#app')
```

まず、以前に作成した `router`インスタンスを取得します。次に、 `new Vue`インスタンスにルーターを使用するように指示します。

## Netlifyにデプロイ

これでアプリケーションが完成したので、Netlifyにデプロイできます。 Netlifyは、静的Webアプリケーションを簡単にデプロイできるようにするサービスです。

まず、プロジェクトのルートに `netlify.toml`というファイルを作成する必要があります。

```toml
[build]
  command = "npm run build"
  functions="functions"
```

このファイルは Netlify にアプリケーションを構築するために実行するコマンドを伝えます。この場合、 `npm run build`コマンドのみを実行しています。

次に、プロジェクトのルートに `.gitignore`というファイルを作成し、次の行を追加する必要があります。

```
/node_modules
/functions
/.netlify
```

このファイルはGitに`node_modules`、`functions`、そして`.netlify`ディレクトリを無視するように指示します。 Gitリポジトリにこれらのディレクトリを含めたくないので、これは重要です。

最後に、Netlifyアカウントを作成してアプリケーションを展開できます。

##結論

この記事では、VueでSPAを構築する方法を紹介しました。私たちは新しいVueプロジェクトを足場として始めました。その後、簡単なコンポーネントを作成してVueルーターに接続しました。最後に、アプリケーションをNetlifyにデプロイしました。