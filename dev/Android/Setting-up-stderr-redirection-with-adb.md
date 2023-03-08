---
title: adb로 stderr 리다이렉션 설정하기
description: 
published: true
date: 2023-02-17T17:58:39.180Z
tags: android, adb
editor: markdown
dateCreated: 2022-11-24T04:40:18.327Z
---

```bash
adb shell stop                           
adb shell setprop log.redirect-stdio true
adb shell start
```

기본적으로 안드로이드는 stderr을 `/dev/null`로 라다이렉트한다. 에러 로그를 리다이렉트 하지 않고 출력시켜서 `adb logcat`으로 확인할 수 있도록 하는 설정이다.

참고 : https://developer.android.com/studio/command-line/logcat.html?hl=ko
