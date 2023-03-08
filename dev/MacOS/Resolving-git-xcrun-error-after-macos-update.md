---
title: MacOS 업데이트 이후 xcrun: error 이슈 해결
description: 이 에러는 뭔데 MacOS 업데이트 할 때마다 높은 확률로 발생하냐...
published: true
date: 2023-02-17T18:00:01.013Z
tags: git, macos
editor: markdown
dateCreated: 2022-12-19T14:50:03.519Z
---


## 이슈

- MacOS 업데이트 이후 `git` CLI 명령어 실행시 아래와 같은 에러가 발생한다.

> xcrun: error: invalid active developer path (/Library/Developer/CommandLineTools), missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun
{.is-danger}

## 해결

- `명렁어 라인 도구`를 다시 설치하면 해결된다. (Xcode Command Line tools)
- 터미널에서 다음을 입력

```bash
xcode-select --install
```

## 스크린샷

![스크린샷_2022-12-19_오후_11.46.48.png](/스크린샷_2022-12-19_오후_11.46.48.png){.align-center}
![스크린샷_2022-12-19_오후_11.46.50.png](/스크린샷_2022-12-19_오후_11.46.50.png){.align-center}
![스크린샷_2022-12-19_오후_11.48.03.png](/스크린샷_2022-12-19_오후_11.48.03.png){.align-center}