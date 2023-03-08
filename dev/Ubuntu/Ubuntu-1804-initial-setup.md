---
title: 우분투 개인 초기 설정 (17.10, 18.04 기준)
description: 
published: true
date: 2023-02-17T17:59:19.358Z
tags: ubuntu
editor: markdown
dateCreated: 2022-11-24T04:41:19.854Z
---

### root 비번 설정
```bash
sudo -i
passwd root
```

### upstream repository 변경
  - 우분투 기본 패키지 저장소보다 국내에 있는 미러 서버를 사용하면 조금 더 쾌적하다.
  - `sed` 명령어는 잘 못써서 vim replace 로: `sudo vim /etc/api/sources.list`, `:%s/kr.archive.ubuntu.com/mirror.kakao.com `
  - `sudo apt update`

### 업데이트
```bash
sudo apt update && sudo apt upgrade -y && sudo apt autoremove -y
```

### (가상머신의 경우) 게스트 서비스 설치

### 필요 프로그램 설치
  - zsh
    - https://github.com/uyu423/TIL/blob/master/Bash/zsh-%EC%84%A4%EC%B9%98-%ED%9B%84-%EC%9C%A0%EC%9A%A9%ED%95%9C-%ED%94%8C%EB%9F%AC%EA%B7%B8%EC%9D%B8.md
  - Powerline Font
    - https://github.com/powerline/fonts/tree/master/
  - Chrome
  - htop, curl, git, vim, net-tools
  - Node.js
  ```bash
  curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
  sudo apt install nodejs
  ```
  - Atom
    - Plugins: https://github.com/uyu423/TIL/tree/master/Atom
  - GitKraken
    - Ubuntu 18.04 에서부터 gitkraken deb 의존성 문제로 다음 lib 설치가 필요하다: `sudo apt install libgnome-keyring0`
  - Themes, etc. (gnome shell)
    - http://luckyyowu.tistory.com/281 or Arc Theme (https://github.com/horst3180/arc-theme)
    - Gnome Shell Chrome Plugin: `sudo apt install chrome-gnome-shell`
    - Gnome Shell Extenstions: `sudo apt install gnome-shell-extensions`

### SSH Keygen
```bash
ssh-keygen -t rsa -b 4096 -C "your@e.mail"
```
  - Github와 GitKraken에 등록

### 기타
  - (VirtualBox) Shared Folder Permission
  ```bash
  sudo adduser $USERNAME vboxsf
  ```
