---
title: ES6 clsss로 싱글톤 패턴을 구현해보자
description: 
published: true
date: 2023-02-17T17:59:00.603Z
tags: nodejs, singleton
editor: markdown
dateCreated: 2022-11-24T04:40:51.154Z
---

- 기존에 es6를 사용해 singleton 패턴을 구현하는 여러 포스트들이 있었지만 내가 궁금했던 것은 `require` 나 `import` 를 통해 외부 파일을 불러왔을 때 해당 `Singleton.js` 가 같은 메모리 공간을 사용하느냐를 확인해 보고 싶었다.
- 미리 결론부터 뱉자면 `require` 나 `import` 를 사용하더라도 싱글톤은 유지가 된다.  

  - Singleton.js
    ```javascript
    class Singleton {
      constructor(str) {
        this.str = str;
      }
    }

    let instance = null;
    module.exports = (str) => {
      if (!instance) instance = new Singleton(str);
      return instance;
    };
    ```

  - callSingletonA.js
    ```javascript
    const fac = require('./Singleton');

    function a() {
      const s = fac('A');
      console.log(s.str);
    }

    module.exports = a;
    ```

  - callSingletonB.js
    ```javascript
    const fac = require('./Singleton');

    function b() {
      const s = fac('B');
      console.log(s.str);
    }

    module.exports = b;
    ```

  - test.js
    ```javascript
    const a = require('./callSingletonA');
    const b = require('./callSingletonB');

    a();
    b();
    ```
  - output
    ```bash
    $ node test.js
    A
    A
    ```
