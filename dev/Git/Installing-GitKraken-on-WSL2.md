---
title: WSL2에 GitKraken 설치하기
description: 
published: true
date: 2023-02-26T10:40:07.933Z
tags: git, gitkraken, wsl2
editor: markdown
dateCreated: 2023-02-26T10:40:06.640Z
---

# Install

```bash
wget https://release.gitkraken.com/linux/gitkraken-amd64.deb
sudo apt install ./gitkraken-amd64.deb
```

> 의존성 체크 실패날 경우
> 
> ```bash
> wget https://release.gitkraken.com/linux/gitkraken-amd64.deb
> ```

# 실행

```
gitkraken
```

> - OAuth 로그인 시 실패나는 경우가 있는데, GitKraken의 OAuth Token을 직접 입력해줘야함. 
>   - WSL2 환경에서 OAuth 토큰을 어떻게 획득해야하는지는 개인기로 돌파 필요


# 추가 설치

한글 폰트와 이모지 안나올 수 있음

```bash
sudo apt install fonts-noto-color-emoji fonts-noto
```