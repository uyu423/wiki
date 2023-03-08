---
title: 우분투에서 윈도우 원격데스크톱 사용
description: 
published: true
date: 2023-02-17T17:59:20.648Z
tags: ubuntu, windows, rdesktop
editor: markdown
dateCreated: 2022-11-24T04:41:22.118Z
---

## Installation
```bash
sudo apt install rdesktop
```

## Recommand Usage
```bash
rdesktop -bg 800x920 hostname.com -r disk:share=/home/directory/share
```

- -b : 비트맵 캐시 활성화
- -g : 해상도 설정
- -r : 공유 디렉토리 설정
