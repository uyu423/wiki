---
title: 터미널에서 Chrome 으로 JIRA 이슈 바로 띄우기
description: 터미널 성애자가 아니면 쓸 일이 없다.
published: true
date: 2023-02-17T17:58:27.155Z
tags: jira, chrome, terminal
editor: markdown
dateCreated: 2022-11-24T04:01:33.704Z
---

- 사실 Mac에서 알프레도? 알프레드? 그 친구를 쓰면 된다는데 나는 영 맥이랑 안친해서..
- `.zshrc` or `.bashrc` 에 추가
  ```bash
  j() { open -n -a "Google Chrome" --args "--new-tab" "http://jira.yanolja.in/browse/$1" }
  jy() { open -n -a "Google Chrome" --args "--new-tab" "http://jira.yanolja.in/browse/YAJA-$1" }
  js() { open -n -a "Google Chrome" --args "--new-tab" "http://jira.yanolja.in/issues/?jql=text%20~%20\"$@\"" }
  ``` 
- example
  ```bash
  j YAJA-1234
  ```
  ```bash
  jy 1234
  ```
  ```
  js hello\ world
  ```